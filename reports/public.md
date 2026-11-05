# Glucose data check

Not a medical device. No treatment advice.

Window: 2020-05-01T10:30:00+00:00 to 2020-05-15T10:30:00+00:00 (end excluded).
Expected interval: 1 minutes. No missing values filled.
Coverage: 14730 / 20160 readings (73.07%).

Source: public CGMacros version 1.0.0, series 001, first glucose column. These are published processed minute-resolution values. Coverage means available rows, not verified original sensor wear; upstream filling cannot be audited. Dates are publisher-shifted. UTC is an explicit placeholder because the source timezone is unknown. This example does not establish clinical data sufficiency.

| Metric | Value | Supporting readings | Coverage |
| --- | --- | --- | --- |
| Time in range (70 to 180 mg/dL) | 99.13 % | 14730 / 20160 | 73.07% |
| Time below range (below 70 mg/dL) | 0.87 % | 14730 / 20160 | 73.07% |
| Time above range (above 180 mg/dL) | 0.00 % | 14730 / 20160 | 73.07% |
| Low band (54 to below 70 mg/dL) | 0.87 % | 14730 / 20160 | 73.07% |
| Very low band (below 54 mg/dL) | 0.00 % | 14730 / 20160 | 73.07% |
| High band (above 180 to 250 mg/dL) | 0.00 % | 14730 / 20160 | 73.07% |
| Very high band (above 250 mg/dL) | 0.00 % | 14730 / 20160 | 73.07% |
| Mean glucose | 88.52 mg/dL | 14730 / 20160 | 73.07% |
| Glucose management indicator (GMI) | 5.43 % | 14730 / 20160 | 73.07% |
| Coefficient of variation (CV) | 10.27 % | 14730 / 20160 | 73.07% |

Time percentages describe accepted readings only. Missing readings are not assumed in range.
GMI is a glucose-based estimate, not a laboratory A1C result. CV uses population standard deviation.

## Quality checks

- Mixed declared units: no.
- Extra duplicate rows: 0.
- Conflicting timestamps excluded: 0.
- Rows outside window: 0.
- Missing runs: 1. Longest: 5430 minutes.

## Coverage by UTC date

| Date | Supporting readings | Coverage |
| --- | --- | --- |
| 2020-05-01 | 810 / 810 | 100.00% |
| 2020-05-02 | 1440 / 1440 | 100.00% |
| 2020-05-03 | 1440 / 1440 | 100.00% |
| 2020-05-04 | 1440 / 1440 | 100.00% |
| 2020-05-05 | 1440 / 1440 | 100.00% |
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
| 2020-05-11T16:00:00+00:00 | 2020-05-15T10:30:00+00:00 | 5430 | 5430 |
