# Phase 8.3 — Full GBPUSD quote replay results (provisional)

**Period:** February 2021–December 2025  
**Underlying input:** HistData GBPUSD four-column `datetime,bid,ask,flags`.  
**Processing (reported from local Codex):** 128,332,195 tick rows; 308 source events; 1,848 model/event records; monthly checkpoint to 2025-12; regression suite PASS.

## Simulated model comparison

| Model | Accepted | Financially complete | Net USD | PF | Net WR | Avg net R | Max balance DD USD | D1 TP | Runner SL | Status |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| **M0** H4 full close | 300 | 288 | **+$1,340.29** | **3.401** | **86.11%** | **+0.1803** | **−$109.40** | — | — | Provisional |
| M1 buffered 70/30 | 300 | 288 | +$1,095.16 | 2.710 | 68.06% | +0.1469 | −$112.09 | 121 | 147 | Provisional |
| M2 ATR 70/30 | 300 | 288 | +$1,241.50 | 3.097 | 79.86% | +0.1670 | −$111.10 | 92 | 176 | Provisional |
| M3 H4 lock 70/30 | 300 | 288 | +$1,165.93 | 3.030 | 78.82% | +0.1568 | −$112.32 | 82 | 186 | Provisional |
| M4 H1 structural 70/30 | 287 | 260 | +$883.39 | 1.889 | 73.46% | +0.1249 | −$205.81 | 184 | 58 | Provisional |
| M5 early 70/30 | 300 | 288 | +$1,095.16 | 2.710 | 68.06% | +0.1469 | −$112.09 | 121 | 147 | Provisional |

**Not a live or broker-verified performance table.** The full replay reported broker-agnostic **0-pip minimum stop-distance assumptions for M1/M3/M5**; M2/M4 require more complete broker-stop metadata and structural amendment evidence. M5's identical totals to M1 may mean early protection had no effective effect; earlier GBPUSD M5 check reported **277 assumed amendment attempts, 31 without amendments**, but effective activation needs evidence. All model outcomes remain **provisional**. Completion differs from acceptance due to quote coverage and lot evidence.

**Accounting note:** 86.11% is **net-positive-trade win rate** (248/288), not the earlier 92.6% gross TP-hit rate on a different independent cohort.

## Differences in simulated net USD versus the contemporary M0 control

| Model | USD difference |
|---|---:|
| M1 | −$245.13 |
| M2 | −$98.79 |
| M3 | −$174.36 |
| M4 | −$456.90 |
| M5 | −$245.13 |

M4 has **different accepted trades**, so that delta is an outcome across independently scheduled portfolios, not strictly a matched-event treatment effect. Partial-close volume rounding, longer runner lifetimes and one-position overlap can affect each modeled portfolio.

## Do not mix with historical Phase 6

Legacy **Phase 6** Detector C, SL2, full H4 exit: **296 portfolio trades; +$1,284.03; PF 3.19951; average net +0.17371R; max reported balance DD ~$101.08**. Its commission/slippage conventions and entry population are not identical to the Phase 8.3 executed population. The legacy baseline remains the reference for the original published experiment and has not been overwritten.

## What the evidence supports and does not support

- Among these **frozen, already GBPUSD-developed rules**, M0 had the highest reported simulated USD P&L and net R across five years.
- The results do **not** establish that arbitrary higher take-profits preserve the high M0 win rate. Average M0 **net R is ~0.18/trade**, far from a sustained 1.6R net/trade needed for $200/month on five $25-risk trades (before compounding).
- M1–M5 have **no demonstrated verified net advantage** over M0.
- Comparisons are provisional due to data gaps, incomplete volume evidence, stop placement assumptions, financing at zero, and imperfect portfolio pending-order interactions.
- No fully untouched-instrument profit results were obtained; EURUSD not run.

## Local reproduction (user-reported; not executed by this GitHub documentation update)

```powershell
python "C:\Users\trueh\Documents\AMD-T1-FRESH\research\three_way_detector_benchmark\phase8_trailing_d1_runner\phase8_3_actual_execution\tests\test_execution_regressions.py"
python "C:\Users\trueh\Documents\AMD-T1-FRESH\research\three_way_detector_benchmark\phase8_trailing_d1_runner\phase8_3_actual_execution\scripts\run_complete_replay.py"
python "C:\Users\trueh\Documents\AMD-T1-FRESH\research\three_way_detector_benchmark\phase8_trailing_d1_runner\phase8_3_actual_execution\scripts\account_actual_replay.py"
```

Local evidence folder: `research/three_way_detector_benchmark/phase8_trailing_d1_runner/phase8_3_actual_execution/`. See `FINAL_EXECUTION_REPORT.md`, `outputs/FINAL_TRADE_LEDGER.parquet`, `FINAL_STOP_AMENDMENTS.parquet`, `FINAL_COVERAGE_FAILURES.csv`, `FINAL_ACCOUNTING_CHECKPOINT.json`, `FINAL_HASHES.json`.

The source files and exact hashes were not transferred to the repository in this documentation update.
