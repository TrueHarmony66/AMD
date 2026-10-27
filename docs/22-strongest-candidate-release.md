# strongest candidate — AMD T1 original-strategy restoration milestone

**Release name:** `strongest candidate`  
**Date:** 27 October 2026  
**Type:** preserved research milestone; **not** independently deployable algorithm software or a live-performance claim.

## Summary

The active research workspace has been switched back to **original AMD T1, Detector C + Scenario A/B + completed FVG midpoint entry + structural SL2 + exact causal H4 wick take-profit (M0)**. The attempted portable generator reconstruction was preserved in a separate experimental folder and is **not** the active source of the original historical events.

This release identifies **M0 as the strongest tested *historical research candidate among the frozen Phase 8.3 variants***; "strongest" does **not** mean robustly validated on unseen markets, safe for investor accounts or even fully source-reproducible.

## Restored original components

Reported preserved Windows workspace root: `C:\Users\trueh\Documents\AMD-T1-FRESH`.

| Component | Local source artifact | Status reported |
|---|---|---|
| Detector C: defended/repeated reaction-level range identification | `research/manual_range_detector_comparison/scripts/phase4d_detector_c.py` | Original source-backed component located |
| Scenario A/B and three-candle FVG research logic | `research/three_way_detector_benchmark/phase4e1/scripts/phase4e1_c_fvg_replay.py` | Original source-backed component located |
| Forensic Scenario A/B audit / invalid-event rejection | `research/three_way_detector_benchmark/phase4e2/scripts/phase4e2_audit.py` | Original source-backed component located |
| Preserved executable historical order/trade universe | `research/three_way_detector_benchmark/sl_tp_backtest/ABC_SL_TP_TRADE_LEDGER.parquet` | **308 unique** original events retained |
| Phase 8.3 full BID/ASK replay | `research/three_way_detector_benchmark/phase8_trailing_d1_runner/phase8_3_actual_execution/scripts/run_complete_replay.py` | Original replay script present |
| Phase 8.3 accounting | `research/three_way_detector_benchmark/phase8_trailing_d1_runner/phase8_3_actual_execution/scripts/account_actual_replay.py` | Original accounting script present |
| Active-workspace declaration | `research/ACTIVE_STRATEGY_ENTRYPOINT.md` | Restoration record created locally |
| Original-workspace restoration report | `research/AMD_T1_ORIGINAL_WORKSPACE_RESTORATION.md` | Restoration record created locally |

This table is a **manifest of user-reported local assets**. The original Python files, original Parquet ledger, and restoration report were **not uploaded as bytes to this repository** as part of this documentation publication. Do not treat these paths as files on GitHub.

## Restoration integrity verification (reported)

- Original saved event universe: **308 unique events**.
- Phase 8.3 historical comparison cache: **1,848 rows** = 308 source events × M0–M5 (six variants).
- Full historical quote-processing checkpoint: **128,332,195 GBPUSD ticks**.
- Phase 8.3 regression suite: **PASS**.
- Original Phase 6 and Phase 8.3 files and metrics left unchanged.
- **No new full tick scan** or EURUSD performance test during restoration.
- Experimental `research/amd_t1_portable_signal_engine/` preserved **but removed from the active research path**; its 2,477-candidate reconstruction was **not substituted** for the original 308 events.

## Strongest tested candidate: M0

**Frozen M0 configuration:**

- GBPUSD H1 Detector C defended consolidation and causal close-breakout signal.
- Scenario A immediate or Scenario B genuinely delayed continuation.
- Completed directional 3-candle FVG; pending BUY/SELL limit at exact 50% midpoint, correct quote-side execution.
- Original structural **SL2** (known sweep/swing anchor plus previously frozen ATR/spread buffer).
- Exact **prior confirmed H4 swing wick** take-profit; not a retrospectively selected or forced 2R objective.
- **12h** pending expiry; **72h** maximum holding from entry.
- Starting simulated capital **$5,000**; **0.5%** current-equity risk per entry; one-position portfolio under declared research assumptions.

### Phase 8.3 provisional historical comparison

| Model | Net modeled USD, Feb 2021–Dec 2025 | PF | Net winning trade % | Average net R | Financially complete |
|---|---:|---:|---:|---:|---:|
| **M0 full H4 exit** | **+$1,340.29** | **3.401** | **86.11%** | **+0.1803R** | **288** |
| M1 70/30 buffered H4 stop | +$1,095.16 | 2.710 | 68.06% | +0.1469R | 288 |
| M2 70/30 ATR trail | +$1,241.50 | 3.097 | 79.86% | +0.1670R | 288 |
| M3 70/30 H4 stop lock | +$1,165.93 | 3.030 | 78.82% | +0.1568R | 288 |
| M4 70/30 H1 structure | +$883.39 | 1.889 | 73.46% | +0.1249R | 260 |
| M5 70/30 early protection | +$1,095.16 | 2.710 | 68.06% | +0.1469R | 288 |

These are **reported historical modeled results**, not broker-live verifications. All models remain provisional due to coverage, volume, execution metadata and/or stop-amendment assumptions; M4 uses a different portfolio cohort. Full [Phase 8.3 results and limitations](18-phase8-3-full-tick-results.md).

A separate, older **Phase 6 M0** research cohort had **296 trades, +$1,284.03, PF 3.19951, avg net +0.17371R, max reported *balance* DD ~$101.08**; it is not silently replaced by Phase 8.3.

## What the failed portability experiment did and did not change

The experimental rebuilt generator's GBPUSD event-parity gate **FAILED / INCOMPLETE**:

| Parity item | Reported count |
|---|---:|
| Original frozen executable events | 308 |
| Reconstructed candidates | 2,477 |
| Normalized IDs overlapping | 245 |
| Frozen events not reproduced | 63 |
| Reconstruction-only candidates | 2,232 |
| Reconstructed fully executable events | **0** |

The reconstructive attempt lacked source-backed **final event eligibility filtering**, exact **SL2 anchor determination** and **causally confirmed H4 target selection**. It therefore cannot be substituted for the original engine.

**A. Original source-backed components:** located / PASS.  
**B. Original historical event ledger and replay engine:** present / PASS.  
**C. One independent end-to-end generator that reproduces the original 308 events from new raw quotes:** **NOT ESTABLISHED**.

No evidence indicates that the original stored trade universe was deleted or replaced. Recovering source files for different phases **does not yet prove** there is a portable, self-generating trading algorithm.

## EURUSD holdout

The previously selected **EURUSD 2021** test year remains **unused for performance**. All 12 monthly ZIP archives reportedly passed integrity checks, but no EURUSD executable event ledger was generated or traded. This release makes **no EURUSD returns or robustness claims**. See [EURUSD blocker](19-eurusd-2021-portability-blocker.md).

## Next technical release gate

Trace the original `phase4d` → `phase4e1` → `phase4e2` → 308-trade cohort pipeline. Recover the source-backed final filter, structural SL2 anchors, and H4 confirmed-pivot choices. Demonstrate field-level parity on the frozen 308 GBPUSD events without choosing exceptions based on realized profitability. **Only then** freeze the portable signal engine and execute EURUSD 2021 as a genuine cross-instrument holdout.

Do **not** optimize the trading settings to force a match or to rescue historical profits.

## Availability and scope

This GitHub milestone includes **the written release record, foundational research documentation, Phase 7/8 findings, modeled summary CSV and the previous seven SVG conceptual diagrams**. It does **not** bundle:

- Local Windows-only Python source and restoration reports;
- Original Parquet event/quote ledgers and checksums;
- HistData ZIP archives or real broker statement exports;
- A validated portable strategy generator;
- A verified investor-ready/live trading system.

The explicit status distinction is intentional. A formal GitHub Release entry, if created, should target the commit holding this document and use the title **strongest candidate**.

**Source:** user-reported local Codex restoration report and previously reported Phase 8.3 historical replay; not an independently rerun backtest from GitHub-hosted code.
