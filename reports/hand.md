# Glucose data check

Not a medical device. No treatment advice.

Window: 2025-01-01T00:00:00+00:00 to 2025-01-01T00:20:00+00:00 (end excluded).
Expected interval: 5 minutes. No missing values filled.
Coverage: 4 / 4 readings (100.00%).

Exploratory short window: these results do not meet the recommended fourteen-day window.

SYNTHETIC HAND CASE, not study data: 50, 100, 150, 200 mg/dL. Mean = 500/4 = 125. Population variance = 12500/4 = 3125. CV = sqrt(3125)/125*100. GMI = 3.31+0.02392*125 = 6.3. Two of four readings in range, one below, one above.

| Metric | Value | Supporting readings | Coverage |
| --- | --- | --- | --- |
| Time in range (70 to 180 mg/dL) | 50.00 % | 4 / 4 | 100.00% |
| Time below range (below 70 mg/dL) | 25.00 % | 4 / 4 | 100.00% |
| Time above range (above 180 mg/dL) | 25.00 % | 4 / 4 | 100.00% |
| Low band (54 to below 70 mg/dL) | 0.00 % | 4 / 4 | 100.00% |
| Very low band (below 54 mg/dL) | 25.00 % | 4 / 4 | 100.00% |
| High band (above 180 to 250 mg/dL) | 25.00 % | 4 / 4 | 100.00% |
| Very high band (above 250 mg/dL) | 0.00 % | 4 / 4 | 100.00% |
| Mean glucose | 125.00 mg/dL | 4 / 4 | 100.00% |
| Glucose management indicator (GMI) | 6.30 % | 4 / 4 | 100.00% |
| Coefficient of variation (CV) | 44.72 % | 4 / 4 | 100.00% |

Time percentages describe accepted readings only. Missing readings are not assumed in range.
GMI is a glucose-based estimate, not a laboratory A1C result. CV uses population standard deviation.

## Quality checks

- Mixed declared units: no.
- Extra duplicate rows: 0.
- Conflicting timestamps excluded: 0.
- Rows outside window: 0.
- Missing runs: 0. Longest: 0 minutes.

## Coverage by UTC date

| Date | Supporting readings | Coverage |
| --- | --- | --- |
| 2025-01-01 | 4 / 4 | 100.00% |

## Missing runs

| Start | End (excluded) | Missing readings | Minutes |
| --- | --- | --- | --- |
