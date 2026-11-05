# cgm-metrics-check

I built a glucose-data checker because I wanted to know how much missing data could hide behind a neat-looking average. It reads a continuous glucose monitoring (CGM) file, checks the timestamps and units, and calculates a summary only when enough readings are available.

I can see time in range, the share of readings inside a defined glucose band, alongside the average and measures of variation. Every result shows its supporting reading count and coverage. Missing readings, duplicate timestamps and mixed declared units stay visible. When coverage is too low, the report explains why it withheld the numbers.

**This is not a medical device and gives no treatment advice.** I use public research data, not private records.

To see it without installing anything, open the saved [public-data report](reports/public.md), [deliberately damaged example](reports/damaged.md), or [hand-calculated example](reports/hand.md). The public example uses a published processed series, so its coverage measures available rows, not verified original sensor wear. It does not establish clinical data sufficiency.

To run it locally, install [uv](https://docs.astral.sh/uv/getting-started/installation/), which creates the Python environment, then run:

```sh
uv venv --seed --python 3.12
source .venv/bin/activate
python -m pip install -e '.[test]'
python scripts/reproduce.py
```

## What the public example shows

I downloaded one anonymized glucose series from CGMacros, kept its publisher-shifted timestamps and glucose values, and added its documented unit. I did not retain demographics, meals or photos. No substitute dataset was needed.

These rounded results come from `python scripts/reproduce.py`; JSON metric values retain ten decimal places for reproducibility across Python versions:

| Example | Accepted / expected readings | Coverage | Time in range |
| --- | --- | --- | --- |
| Published processed series | 14,730 / 20,160 | 73.07% | 99.13% |
| Deliberately damaged copy | 11,729 / 20,160 | 58.18% | Refused |

I made the damaged copy by removing a block, converting some values to a different declared unit, adding repeated rows and adding a conflicting value at an existing timestamp. It is a demonstration of the checker, not a finding about the study. The original extract stays unchanged.

## Check another file

Use one sensor series at a time, with a regular sampling interval and an explicit analysis window. The CSV header is `timestamp,glucose,unit`. Timestamps need a timezone offset; units must be `mg/dL` or `mmol/L`. I never guess units from a number's size.

For the included extract:

```sh
cgm-check data/cgmacros_001.csv \
  --start 2020-05-01T10:30:00+00:00 \
  --end 2020-05-15T10:30:00+00:00 \
  --cadence-minutes 1 --out out
```

The output folder contains `report.md`, `report.json` and `observations.ndjson`. The last file has one FHIR R4 Observation per source row. FHIR is a standard format for exchanging health measurements. I preserve each original quantity, unit and timestamp offset, and I do not invent a patient identity. Exported source rows include duplicates; the metric report separately explains which timestamps were excluded. The small [FHIR example](reports/fhir-example.ndjson) is readable as text.

The command returns success when metrics are reported, a distinct refusal status when coverage or duration is insufficient, and an input-error status for invalid files. Exact exit codes are documented in [the CLI](src/cgm_metrics_check/cli.py).

## How I calculate the summary

I count expected timestamps across the requested window, including missing time before the first reading and after the last. The start is included and the end is excluded. Each timestamp counts at most once. Identical duplicate values count once; conflicting values exclude the entire timestamp. Off-grid readings are rejected instead of silently resampled. I never fill gaps.

The normal report requires at least fourteen days and the consensus minimum of 70% available readings. The explicitly named `--allow-short-window` option exists for exploratory examples; it never lowers the coverage requirement. Daily coverage and every missing run are included because an overall percentage can hide uneven collection.

The report includes these calculations:

- Time in range: 70 through 180 mg/dL, including both boundaries.
- Time below and above range, with separate low bands split at 54 mg/dL and high bands split at 250 mg/dL.
- Mean glucose, the arithmetic average of accepted readings in mg/dL.
- Glucose management indicator (GMI), an estimate calculated as `3.31 + 0.02392 × mean glucose`. It is not a laboratory A1C result.
- Coefficient of variation (CV), the population standard deviation divided by the mean, expressed as a percentage.

Time percentages describe accepted readings on the fixed sampling grid. They do not assume missing time was in range. Explicit mixed units are flagged and converted for calculation, while exports retain the source units. A mislabeled value cannot reliably be detected from its magnitude alone. The policy and formula constants are printed by `python scripts/reproduce.py`; [design notes](docs/design.md) explain the choices and limitations.

## Data and references

- Gutierrez-Osuna, Kerr, Mortazavi and Das: [CGMacros on PhysioNet](https://physionet.org/content/cgmacros/1.0.0/), [dataset DOI](https://doi.org/10.13026/3z8q-x658). The source provides processed minute-resolution values; upstream filling and original sensor outages cannot be audited from this file. Its timezone is unspecified. I attach a disclosed UTC placeholder to the shifted dates to preserve relative intervals, not to claim actual UTC collection times.
- Goldberger et al.: [PhysioBank, PhysioToolkit, and PhysioNet](https://doi.org/10.1161/01.CIR.101.23.e215), the source platform's requested citation.
- Battelino et al.: [International Consensus on Time in Range](https://pmc.ncbi.nlm.nih.gov/articles/PMC6973648/), for ranges, coverage and collection duration. I implement the general glucose bands, without setting individual clinical targets.
- Bergenstal et al.: [Glucose Management Indicator](https://pmc.ncbi.nlm.nih.gov/articles/PMC6196826/), for the GMI equation.
- HL7: [FHIR R4 Observation](https://hl7.org/fhir/R4/observation.html) and [Quantity units](https://hl7.org/fhir/R4/datatypes.html#Quantity). Exports use the core resource structure and UCUM unit codes, not a claim of clinical profile certification.

The [data notes](data/README.md) and [provenance manifest](data/provenance.json) identify the selected archive member, transformations and checksums. Code is MIT licensed. The extract and derived study reports retain [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), including its noncommercial restriction.

To fetch the extract again, install the optional downloader and run:

```sh
python -m pip install -e '.[fetch]'
python scripts/fetch_public_data.py
python scripts/reproduce.py
```

The downloader retrieves just the selected CSV using archive byte ranges and checks its pinned hash. Report generation and tests work offline from the committed extract.

## Package structure and checks

I keep input validation in `model.py` and `io.py`, calculation and coverage rules in `metrics.py`, and original-quantity exports in `fhir.py`. The CLI connects them. The package has no runtime dependencies; the optional test dependencies validate exported resources against the FHIR R4 model.

```sh
python -m pytest -q
python scripts/reproduce.py
# In a clean checkout, this confirms the saved reports were reproduced:
git diff --exit-code -- reports/
python -m pip install build
python -m build
```

The test command currently passes 45 cases, including hand-derived results, the coverage boundary, missing window edges, timezone equivalence, conflicting timestamps, mixed units, invalid input, CLI refusal and validation of every exported public reading. [CI](.github/workflows/ci.yml) runs the full suite, reproduces the saved reports, builds the package and exercises the installed command across its declared Python versions.
