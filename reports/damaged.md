# Glucose data check

Not a medical device. No treatment advice.

Window: 2020-05-01T10:30:00+00:00 to 2020-05-15T10:30:00+00:00 (end excluded).
Expected interval: 1 minutes. No missing values filled.
Coverage: 11729 / 20160 readings (58.18%).

DELIBERATELY DAMAGED COPY: removed a block of rows, changed some declared units with values converted, and injected duplicates and a conflicting timestamp. Source: public CGMacros version 1.0.0, series 001, first glucose column. These are published processed minute-resolution values. Coverage means available rows, not verified original sensor wear; upstream filling cannot be audited. Dates are publisher-shifted. UTC is an explicit placeholder because the source timezone is unknown. This example does not establish clinical data sufficiency.

| Metric | Value | Supporting readings | Coverage |
| --- | --- | --- | --- |
| Time in range (70 to 180 mg/dL) | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |
| Time below range (below 70 mg/dL) | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |
| Time above range (above 180 mg/dL) | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |
| Low band (54 to below 70 mg/dL) | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |
| Very low band (below 54 mg/dL) | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |
| High band (above 180 to 250 mg/dL) | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |
| Very high band (above 250 mg/dL) | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |
| Mean glucose | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |
| Glucose management indicator (GMI) | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |
| Coefficient of variation (CV) | REFUSED: coverage below 70% of expected readings | 11729 / 20160 | 58.18% |

Time percentages describe accepted readings only. Missing readings are not assumed in range.
GMI is a glucose-based estimate, not a laboratory A1C result. CV uses population standard deviation.

## Quality checks

- Mixed declared units: yes.
- Extra duplicate rows: 41.
- Conflicting timestamps excluded: 1.
- Rows outside window: 0.
- Missing runs: 3. Longest: 5430 minutes.

## Coverage by UTC date

| Date | Supporting readings | Coverage |
| --- | --- | --- |
| 2020-05-01 | 809 / 810 | 99.88% |
| 2020-05-02 | 1440 / 1440 | 100.00% |
| 2020-05-03 | 750 / 1440 | 52.08% |
| 2020-05-04 | 0 / 1440 | 0.00% |
| 2020-05-05 | 570 / 1440 | 39.58% |
| 2020-05-06 | 1440 / 1440 | 100.00% |
| 2020-05-07 | 1440 / 1440 | 100.00% |
| 2020-05-08 | 1440 / 1440 | 100.00% |
| 2020-05-09 | 1440 / 1440 | 100.00% |
| 2020-05-10 | 1440 / 1440 | 100.00% |
| 2020-05-11 | 960 / 1440 | 66.67% |
| 2020-05-12 | 0 / 1440 | 0.00% |
| 2020-05-13 | 0 / 1440 | 0.00% |
| 2020-05-14 | 0 / 1440 | 0.00% |
| 2020-05-15 | 0 / 630 | 0.00% |

## Missing runs

| Start | End (excluded) | Missing readings | Minutes |
| --- | --- | --- | --- |
| 2020-05-01T11:10:00+00:00 | 2020-05-01T11:11:00+00:00 | 1 | 1 |
| 2020-05-03T12:30:00+00:00 | 2020-05-05T14:30:00+00:00 | 3000 | 3000 |
| 2020-05-11T16:00:00+00:00 | 2020-05-15T10:30:00+00:00 | 5430 | 5430 |
