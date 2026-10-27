# strongest candidate — AMD T1 original-strategy restoration milestone

**Release name:** `strongest candidate`  
**Date:** 27 October 2026  
**Type:** preserved research milestone; **not** independently deployable algorithm software or a live-performance claim.

## Summary

The active research workspace has been switched back to **original AMD T1, Detector C + Scenario A/B + completed FVG midpoint entry + structural SL2 + exact causal H4 wick take-profit (M0)**. The attempted portable generator reconstruction was preserved in a separate experimental folder and is **not** the active source of the original historical events.

This release identifies **M0 as the strongest tested *historical research candidate among the frozen Phase 8.3 variants***; "strongest" does **not** mean robustly validated on unseen markets, safe for investor accounts or even fully source-reproducible.

## UPDATE — Original signal chain reproduced and EURUSD 2021 holdout completed (27 October 2026)

**This update supersedes the earlier release-state statements below that the complete pipeline was unavailable and EURUSD had not been tested.** Those statements describe the circumstances at the original release date. The original research logic was recovered after publication; no strategy optimization was made for EURUSD results.

### GBPUSD original-source reproducibility gate — PASS (reported local execution)

The ORIGINAL Phase 4E6 grouped tick scanner `research/three_way_detector_benchmark/phase4e6_grouped_replay/scripts/execute_scan.py` was recovered and run with the original GBPUSD BID/ASK research inputs:

- **1,099** candidates → **717** price reaches + **382** non-reaches + **0** missing records.
- **135,426,651** original GBPUSD ticks processed.
- Status and identity matched **all 1,099** preserved candidate IDs.
- The original stop producer `research/three_way_detector_benchmark/stop_loss_comparison/scripts/run_stop_comparison.py` and SL/TP producer `research/three_way_detector_benchmark/sl_tp_backtest/scripts/run_sl_tp_backtest.py` reproduced the **3,930-row multi-detector stop/target ledger exactly**, with **DataFrame equality true** and identical original/reproduced SHA-256: `0bec293e1027637c08d1f924279c1d5250d6476ce772ed073cb60d2d1347106a`.
- In original Detector C: **499** Phase 4E6 candidates → **335** midpoint reaches → **319** timestamp-parseable C entries → **11** invalid stop exclusions → **308** valid stop and final SL2/H4 source events.
- **Distinct scan windows:** the SL/TP producer's earlier reported source scan comprised **133,166,553** ticks; the completed upstream midpoint scan comprised **135,426,651**. These are two distinct reported processing stages, **not** one interchangeable tick-row statistic.
- Frozen SL2 anchor: prior FVG excursion, genuine sweep or structural fallback; offset `max(0.15 × completed H1 ATR14, 2 × activation spread)`. Long SL below the anchor; short SL above.
- Frozen H4 target: closest directionally appropriate **previously confirmed** H4 swing wick, with two completed left and two right H4 candles; confirmation after the second right candle closes. Long exits use BID; short exits ASK.

These are reported source-chain reproductions, **not** a claim that all original source files or raw archives were uploaded into GitHub. [Full reproduction record](24-recovered-gbp-source-chain.md).

### EURUSD 2021 — first untouched historical market holdout (reported result)

The EURUSD year was changed from the original 2025 proposal to **2021 before inspecting EURUSD trading performance**. The same original strategy M0 was run without EURUSD-specific tuning, using real historical quotes and the frozen simulated cost/risk rules.

| Metric | EURUSD 2021 original M0 |
|---|---:|
| Monthly archives / ticks checked | **12 / 16,766,837** |
| Invalid, crossed, out-of-order, conflicting quotes | **0** |
| Detector C H1 / H4 ranges | **335 / 176** |
| FVG candidates | **295** |
| Reached / unreached / quote-missing | **189 / 101 / 5** |
| Valid SL2 / completed source events | **181 / 163** |
| Accepted one-position trades / overlap skips | **145 / 18** |
| Net wins / losses | **121 / 24** |
| **Net win rate** | **83.45%** |
| **Average net R** | **+0.2068R** |
| **Profit factor** | **2.7165** |
| **Net modeled P&L** | **+$700.38** |
| Ending modeled equity | **$5,700.38** |
| **Maximum balance drawdown** | **$79.53** |
| H4 TP / SL / time exits | **130 / 15 / 0** |
| Average / median monthly P&L | **+$58.37 / +$52.79** |
| Best / worst month | **July +$116.41 / August −$40.81** |
| Positive months | **11 / 12** |

**Research interpretation:** EURUSD showed positive **historical** expectancy under modeled costs and frozen 0.5% dynamic-equity risk. This adds one instrument/year of cross-market evidence; it **does not establish forward profitability, a verified live fill model, or a $200/month income level**. Five quote-coverage records remain missing at the upstream candidate stage. Maximum *equity* drawdown is not supplied; **$79.53 is balance DD only**. H4 TP count is based on price-level exit classifications, not net-winning trades. EURUSD 2021 is **no longer an untouched holdout** after this first run.

**Cross-market benchmark (different periods):** earlier GBPUSD Phase 8.3 M0 reports **288 financially complete trades**, **86.11% net WR**, **PF 3.401**, **+0.1803R**, **+$1,340.29** over ~five years. EURUSD reports **145 accepted trades**, **83.45% net WR**, **PF 2.7165**, **+0.2068R**, **+$700.38** over one year. This is contextual comparison only; do not compare total profits as if the observation windows were equal.

Local-only reported evidence: `research/eurusd_2021_original_amd_holdout/EURUSD_2021_M0_FINAL_REPORT.md`, `EURUSD_M0_MONTHLY_RESULTS.csv`, `EURUSD_SOURCE_SIGNAL_LEDGER.csv`, `EURUSD_M0_TRADE_LEDGER.csv`, `EURUSD_M0_UNRESOLVED_RECORDS.csv`, `EXECUTION_INTEGRITY_REPORT.json`, and `HOLDOUT_HASHES.json`. **Their bytes have not been transferred to the public GitHub repository.** [Full EURUSD report summary](25-eurusd-2021-m0-holdout.md).

### Updated research status

**Original source-chain reproduction: reported PASS. EURUSD 2021 historical holdout: reported positive.** Complete source artifacts and broker-valid execution remain outside this GitHub documentation-only release. Preserve all original thresholds and M0 assumptions. A further independently chosen market period and forward demo execution would be separate tests, **not** reasons to retrospectively optimize the EURUSD run.

---

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

## Historical failed reconstruction (superseded by original-source recovery)

Before recovering the original producer scripts, an **experimental non-original generator** failed the GBPUSD event-parity gate. **This failure was superseded for the actual original-source pipeline by the reproduction summarized in the update above.** Historical experimental counts:

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
**C at the time of initial publication:** independent source-chain reproduction **NOT ESTABLISHED**. **Updated status:** original GBPUSD scan and SL/TP ledger reproduction were subsequently reported successful, and EURUSD 2021 was run. See top-of-release update.

No evidence indicates that the original stored trade universe was deleted or replaced. Locating isolated source files alone was not proof; the subsequently executed original scanner and stop/target producer yielded positive reproducibility evidence as recorded above.

## EURUSD holdout — updated

**EURUSD 2021 has now been executed as the first original M0 cross-market historical holdout.** The previous untested state is obsolete. See the full figures in the release update above and the [holdout summary](25-eurusd-2021-m0-holdout.md). The [earlier portability blocker](19-eurusd-2021-portability-blocker.md) is retained as a historical audit record.

## Next technical release gate — updated

Preserve the original restored generator and reproduce the local lineage from source archives on independently accessible infrastructure. Audit unresolved quote records, broker execution costs and equity drawdown, then precommit a new independent year/market or forward-demo evaluation without retuning this holdout.

## Availability and scope

This GitHub milestone includes **the written release record, foundational research documentation, Phase 7/8 findings, modeled summary CSV and the previous seven SVG conceptual diagrams**. It does **not** bundle:

- Local Windows-only Python source and restoration reports;
- Original Parquet event/quote ledgers and checksums;
- HistData ZIP archives or real broker statement exports;
- A complete independently redistributed and executable strategy generator (source-backed original implementation was recovered **locally** after initial publication);
- A verified investor-ready/live trading system.

The explicit status distinction is intentional. The existing formal GitHub Release **strongest candidate** retains its original tag; this documentation has been updated with the later GBPUSD and EURUSD milestone results.

**Source:** user-reported local Codex restoration report and previously reported Phase 8.3 historical replay; not an independently rerun backtest from GitHub-hosted code.
