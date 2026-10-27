# Phase 7 — H4-to-D1 liquidity continuation and corrected audit

**Research status:** diagnostic observation, **not** realized runner profit.

After the original Detector C + SL2 H4 exit, historical price movement was observed toward a previously confirmed D1 wick. Original position is **already closed**. Phase 7 subsequently corrected several erroneous counters.

## Cohort and corrected post-H4 horizon counts

- H4-TP portfolio winners inspected: **274**.
- Available confirmed D1 targets by entry: **272**; **2** without targets.
- Correct cumulative post-H4 72-hour tags: **214/272 = 78.68%** among target-eligible trades (214/274 = 78.10% among all examined winners).
- D1 not reached: **58**.
- Quote coverage and eligibility denominators must be interpreted separately; original 2 insufficient-coverage claims were reconciled by the audit.

| Cumulative horizon after H4 | Eligible denominator | D1 tags | Sweeps |
|---|---:|---:|---:|
| 4h | 272 | 155 | 155 |
| 12h | 272 | 187 | 187 |
| 24h | 272 | 200 | 200 |
| 48h | 272 | 206 | 206 |
| 72h | 272 | 214 | 214 |

The earlier nonmonotonic 24h/48h counts resulted from inconsistent horizon flags. Another earlier 214 vs 171 comparison mixed **entry+72h** with **post-H4+72h** observation clocks. The historical executable strategy's 72h **entry** holding limit remains unchanged.

## Sweep, rejection, continuation

- D1 tags / one-tick sweeps: **214** each.
- Subsequent completed H1 rejection within 1h: **88**; 4h: **149**; 12h: **188**.
- Objective post-sweep continuation (possibly overlapping with rejections): **159**.
- Reported mutually exclusive outcome categories: **188 rejected**, **26 continued**, **58 not reached**, **2 no eligible target**, using the audit's classification precedence. **Do not** interpret the 159 overlapping continuation observations as 159 exclusive continued trades.

## Timing and distances

- Median H4-to-D1 tag delay: **0.44h** (~26.4 minutes).
- Median H4-to-D1 target distance: **11.575 pips**.
- Median post-H4 MFE: **51.15 pips**.
- Median post-H4 MAE: **54.90 pips**.

Earlier reported 56–73 pips were MFE, **not** median distance from H4 to D1. Full post-TP MFE/MAE may include excursions after first D1 touch; it cannot establish stop-before-target precedence.

- Diagnostic original SL2 touches before D1 as reported: **138**.
- Diagnostic entry-price stop touches: **271**.
- These require cautious interpretation against eligibility, observation windows and actual event sequencing; they do **not** retroactively alter already closed H4 positions.

**Research lesson:** D1 was frequently reached in the audit, but a profitable 70/30 runner cannot be inferred from endpoint reach counts. Chronological stop amendments, lots and partial fills are necessary.

**Original Windows-only evidence** (not yet uploaded to GitHub):
`research/three_way_detector_benchmark/phase7_h4_d1_continuation/audit/` with `PHASE7_CRITICAL_RESULTS_AUDIT.md`, `C_POST_H4_CONTINUATION_AUDITED.parquet`, `CORRECTED_HORIZON_COUNTS.csv`, `SAMPLE_TRADE_TRACES.csv` and `AUDIT_TIMING_DISTANCE.csv`.
