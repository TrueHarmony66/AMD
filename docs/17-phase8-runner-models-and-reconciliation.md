# Phase 8 — Frozen stop-management tests and integrity history

**Scope:** all frozen research variants M0–M5 across GBPUSD February 2021–December 2025. All are historical modeled executions; no verified live broker fills or actual stop-distance conditions.

## Frozen model definitions

| Model | H4 event | Runner and stop management |
|---|---|---|
| **M0 (control)** | 100% close at H4 wick | No runner |
| **M1 buffered** | 70% close at H4 | 30% toward previously confirmed D1 wick; stop BUY H4–0.25×completed H1 ATR14, SELL H4+0.25×ATR |
| **M2 ATR trail** | 70% close at H4 | 30% toward D1; ratchet 0.25×completed H1 ATR14 behind best favorable executable quote |
| **M3 exact H4 lock** | 70% close at H4 | 30% toward D1; attempt exact H4 wick stop only **after a genuine one-tick H4 sweep** |
| **M4 structural H1** | 70% close at H4 | 30% toward D1; trail beyond causally confirmed H1 swings using frozen structural buffer |
| **M5 early protection** | H1 swing protection after 80% of path to H4, if valid; then 70% at H4 | Remaining 30% follows M1 |

Common rules: frozen Detector C, Scenario A/B, true three-candle FVG, 50% midpoint, SL2, exact confirmed H4 TP, 12h pending lifetime, entry+72h holding cap, 0.5% equity risk, one open position where simulation supports it.

## What failed before the final replay

1. Phase 8 initial aggregate MFE/MAE caches lacked actual partial-fill and stop-amendment quote events; runner profitability could **not** be calculated.
2. Phase 8.1 processed **128,332,195 ticks**, 308 source events, but incorrectly blocked portfolio entries for each event's entire 72h *scan window*. This accepted **197**, skipped **111**.
3. Exit-aware replay accepted **300**, skipped **8**; **12** source-only records absent from Phase 6, while **8** legacy Phase 6 entries were blocked — explaining the net +4 accepted-event difference, *not* proving identical trade universes.
4. An interim fair M0 valued pre-H4 SL trades at H4 TP instead of the actual stop quote. This created false PF **49.762** and false DD **$1.80**. These numbers are **invalid**.
5. Corrected interim M0 reported $1,342.54, PF 3.40478, $109.40 balance DD, before the subsequent full replay.
6. Interim M1 shared the same pre-H4 stop valuation defect and missed actual H4 partial-close quotes. M3 cached stop changes did not support valid H4 amendments.
7. Multiple reports had 291/292 financially complete ambiguity and 7 missing lots + 2 unresolved quote coverage issues, requiring fresh event accounting.

All interim profit figures are historical research artifacts, **not** interchangeable with the final quoted model results. The Phase 6 baseline is separately maintained.

## Phase 8.3 full tick replay and remaining uncertainty

Phase 8.3 subsequently **ran all six frozen models across 128,332,195 historical GBPUSD tick rows**; **308 source events × 6 = 1,848 model/event records**; monthly ZIP coverage February 2021 through December 2025. Regression suite reported **PASS**. Accounting uses 0.5% dynamic equity sizing, historical BID/ASK, assumed **$7/lot commission**, **0.5-pip adverse stop slippage**, **zero swap**, and **0.01-lot steps**. Costs are assumptions; their precise commission charging convention and broker execution metadata require independent verification.

**Important**: for M0/M1/M2/M3/M5 **300 accepted**, 8 blocked; M4 **287 accepted**, 21 blocked because its longer open-runner lifetimes prevent subsequent entries. **292 quote-complete**, **288 financially complete** in other models; four quote-complete records still lacked lot-size evidence and eight source events had unresolved coverage. M4: **260 financially complete**. Do not silently replace unresolved events with zeros.

### Final replay results and verdicts

See [Phase 8.3 table](18-phase8-3-full-tick-results.md) for the exact provisional results and limitations.

## Why a D1 runner did not win

High diagnostic D1 reach after H4 ≠ sufficient incremental profit for the runner. Only 30% of a valid partial position participates after H4; stop hit before D1, commission, lot rounding and increased position occupancy change net outcome. The frozen observed M1–M5 models failed to outperform M0 **on the reported simulated five-year net dollars**. This finding must not be turned into after-the-fact parameter optimization.

**Local source outputs not yet uploaded:** `research/three_way_detector_benchmark/phase8_trailing_d1_runner/`, including `phase8_3_actual_execution/` scripts, Parquet ledgers, amend-event traces, hashes, regression suite, and original checkpoint. The repo stores this written summary, not those source bytes.
