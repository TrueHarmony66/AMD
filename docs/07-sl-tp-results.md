# Historical SL × TP backtest: reported results and actual uploaded summaries

**Scope:** 3 detectors × 2 structural SL models × 3 causal H4/D1/combined swing-target models = 18 tested combinations. All results below are **historical**, with provisional 12h pending-order TTL and 72h holding horizon, zero commission, independently evaluated potentially overlapping entries. Full 18-row source outcome ledger and full detailed summary remain local/not yet imported.

## Selected H4 target outcomes at 72h, as reported

| Detector | Stop | Trades | TP | SL | TP-hit share | Avg realized R | Gross PF | Reported max DD |
|---|---|---:|---:|---:|---:|---:|---:|---:|
| A | SL1 intermediate | 141 | 101 | 40 | 71.6% | 0.009 | 1.028 | −8.91R |
| A | SL2 beyond swing | 141 | 132 | 9 | 93.6% | 0.210 | 4.209 | −2.00R |
| B | SL1 | 190 | 142 | 48 | 74.7% | 0.037 | 1.128 | −14.09R |
| B | SL2 | 189 | 177 | 12 | 93.7% | 0.169 | 3.610 | −2.81R |
| C | SL1 | 301 | 200 | 101 | 66.4% | 0.000 | 1.001 | −27.96R |
| C | SL2 | 299 | 277 | 22 | 92.6% | 0.195 | 3.612 | −3.76R |

**Caution:** H4 results show TP+SL=trade count without any time exits in these selections; exact expiry/time-exit and no-future test must be independently reviewed against source ledger. SL1 and SL2 H4 counts differ for B (190 vs 189) and C (301 vs 299); a **strict paired same-event subset** is needed to attribute all outcome changes to the stops themselves.

The reported averages are rounded. Exact total realized R from the uploaded **yearly** CSV, H4/SL2, is A **+29.5461R**, B **+32.0223R**, C **+58.1666R**. These are **sums of independent per-trade risk-normalized results**, not guaranteed realizable simultaneous portfolio equity.

## Frequency across 59 represented months, February 2021–December 2025

| H4/SL2 detector | Trades | Mean calendar-month trades | Median | Min | Max | Zero months | Months with ≥5 |
|---|---:|---:|---:|---:|---:|---:|---:|
| A | 141 | 2.39 | 2 | 0 | 7 | 8 | 4 |
| B | 189 | 3.20 | 3 | 0 | 8 | 4 | 11 |
| C | 299 | 5.07 | 5 | 0 | 12 | 1 | 34 |

Source: attached `ABC_SL_TP_MONTHLY.csv` provided by the trader. An identical second attached copy was checked. The CSV contained 996 nonempty rows (some detector-month-method combinations absent), distinct 59 month keys; absent combo counts in this represented span were set to zero. January 2021 was outside represented monthly keys and not imputed as zero.

For C, zero month was **2022-09**, maximum 12 in **2024-04 and 2025-06**; 18 months had precisely 5–6 trades, 34/59 had at least 5. These counts refer to **modeled entered trades with H4 target and SL2**, not all raw setups.

## Annual H4/SL2 results (uploaded yearly CSV)

| Year | A trades | A sum R | B trades | B sum R | C trades | C sum R |
|---|---:|---:|---:|---:|---:|---:|
| 2021 | 28 | +3.189 | 25 | +4.273 | 57 | +15.428 |
| 2022 | 20 | +2.039 | 37 | +7.288 | 48 | +0.387 |
| 2023 | 35 | +5.320 | 34 | +6.278 | 52 | +11.860 |
| 2024 | 36 | +16.501 | 44 | +4.154 | 68 | +20.926 |
| 2025 | 22 | +2.497 | 49 | +10.029 | 74 | +9.565 |

A and B also have positive **reported** year-level gross sums throughout; low positive C 2022 (+0.387R) highlights vulnerability to small trading cost changes. This is not yet a net or independent holdout evaluation.

## Stop-hit-only study (72h, 655 paired)

| Detector | SL1 hits | SL2 hits | SL1-only stopouts | Median risk SL1 | Median risk SL2 |
|---|---:|---:|---:|---:|---:|
| A (n=152) | 88 | 63 | 25 | 27.39 pips | 41.13 pips |
| B (n=195) | 103 | 84 | 19 | 27.28 pips | 50.16 pips |
| C (n=308) | 191 | 132 | 59 | 23.45 pips | 45.91 pips |

These 72h counts were from a stand-alone **SL-only** study. They are not incompatible with much smaller SL2 stopout counts after explicit TP exit (a position already closed at TP is no longer exposed to later stop hits). But they make source-ledger and expiry audit essential.

## Why high SL2 TP-hit ratio is not enough

Many outer-stop targets are substantially less than 1R above entry because they select the nearest H4 wick rather than scale TP to risk. A strategy winning +0.2R on most trades can be unprofitable after standard costs even at a 90% TP-hit share. Need win-size/loss-size distribution, commissions, swaps, slippage, competing order suppression, time exit accounting and forward validation.

## Still required to publish the complete 18-case results

Import exact `ABC_SL_TP_SUMMARY.csv`, trade ledger Parquet, `ABC_SL1_VS_SL2_PAIRED.csv`, cost-sensitivity CSV and complete D1/combined results. **Do not invent D1/combined performance from the selected H4 rows**. Preserve non-H4 results as presently *run but not accessible for independent documentation*.
