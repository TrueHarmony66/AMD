# EURUSD 2021 — original AMD T1 M0 first untested-instrument historical holdout

**Reporting date:** 27 October 2026. **Status:** completed, positive **historical modeled** net returns. Local Codex reported that the original-source GBPUSD parity gate passed before EURUSD P&L was inspected. EURUSD 2021 was designated instead of the initial 2025 year *before* checking EURUSD strategy performance.

## Frozen strategy and execution

Original Detector C → Scenario A/B breakout and FVG → 50% midpoint limit → original causal SL2 → prior confirmed H4 wick TP. M0 exits the full position at H4 or SL; no D1 runner or trailing stop.

- EURUSD January–December 2021.
- Starting equity **$5,000**, **0.5% dynamic-equity risk**, one open position.
- Original **12-hour pending expiry**, **72-hour entry-to-exit holding cap**.
- BID/ASK chronological fills, 0.01-lot steps, preserved assumed **$7/lot commission**, **0.5 pip adverse stop slippage**, swap **0** absent verified financing data.
- No optimization, no MT5/GSR activity and no EURUSD performance inspection before the GBPUSD provenance gate.

## Input-integrity and candidate funnel

| EURUSD 2021 stage | Reported |
|---|---:|
| HistData monthly archives | 12 |
| Total bid/ask ticks processed | 16,766,837 |
| Invalid/crossed/out-of-order/conflicting records | 0 |
| Detector C H1 ranges | 335 |
| Detector C H4 ranges | 176 |
| FVG candidates | 295 |
| Midpoint quote reaches | 189 |
| Confirmed non-reaches | 101 |
| Missing quote coverage | 5 |
| Valid SL2 records | 181 |
| Completed source events | 163 |
| Accepted one-position trades | 145 |
| Overlap exclusions | 18 |

**Coverage and denominator distinction:** 189 + 101 + 5 = 295 FVG candidates; 145 is the accepted executed portfolio, not every eligible FVG. The precise reasons for the 181 → 163 event reduction are not included in the pasted summary; inspect the original local unresolved-record ledger before asserting a full exclusion waterfall.

## Original M0 outcome after modeled costs

| Measure | EURUSD 2021 |
|---|---:|
| Completed accepted M0 trades | **145** |
| Net winning / net losing trades | **121 / 24** |
| **Net win rate** | **83.45%** |
| Average net expectancy | **+0.2068R/trade** |
| **Profit factor** | **2.7165** |
| **Net profit** | **+$700.38** |
| Ending simulated account equity | **$5,700.38** |
| Maximum **balance** drawdown | **$79.53** |
| Maximum floating equity drawdown | **Not supplied** |
| H4-target / SL / time exits | **130 / 15 / 0** |
| Mean / median calendar-month net | **+$58.37 / +$52.79** |
| Best calendar month | **July +$116.41** |
| Worst calendar month | **August −$40.81** |
| Positive months | **11 of 12** |

**Net WR and H4-hit rate are different:** 130 TP exits are not 130 trades necessarily profitable net of spread/commission. **$79.53 is balance DD**, not mark-to-market equity DD.

Only best/worst, average, median and 11/12 profitable month results are reproduced here. **Full month-by-month CSV was not supplied to GitHub**, so no individual monthly amounts beyond July/August are invented.

## Comparison against original GBPUSD M0 reference

| Metric | GBPUSD, Phase 8.3 (~5 years) | EURUSD 2021 (1 year) |
|---|---:|---:|
| Financially complete / accepted trades used in result | 288 financially complete | 145 accepted |
| Net WR | 86.11% | 83.45% |
| Profit factor | 3.401 | 2.7165 |
| Average net R | +0.1803 | +0.2068 |
| Modeled net USD | +$1,340.29 | +$700.38 |
| Reported monthly average | ~$22.72 | $58.37 |

The sample durations and event-cohort/completeness definitions differ. Positive EURUSD expectancy after frozen modeled costs is useful evidence of transfer to another historical instrument; **it is not proof of robustness across market regimes or future profitability**. This test is now used, and should not be treated as an untouched holdout again.

## Source files and limits of this release

Local-only (NOT uploaded) files in `research/eurusd_2021_original_amd_holdout/`:

- `EURUSD_2021_M0_FINAL_REPORT.md`
- `EURUSD_SOURCE_SIGNAL_LEDGER.csv`
- `EURUSD_M0_TRADE_LEDGER.csv`
- `EURUSD_M0_UNRESOLVED_RECORDS.csv`
- `EURUSD_M0_MONTHLY_RESULTS.csv`
- `EXECUTION_INTEGRITY_REPORT.json`
- `HOLDOUT_HASHES.json`

Public GitHub stores this report and the single-row [machine-readable reported summary](../data/summary/eurusd-2021-m0-reported-summary.csv). It **does not include** the raw historical ZIP files, original executable Python, validated broker order-fill logs or a locally independently rerun result.

**Research verdict:** report is positive on the first EURUSD 2021 independent-instrument year at frozen 0.5% modeled risk; the ~$58 monthly mean does not meet a $200/month objective. Hold the M0 rules fixed and schedule genuinely new evaluation without optimizing on this now-used period.
