# Recovered original AMD T1 GBPUSD source chain — reproduced

**Status:** PASS **as reported by local Codex execution** (27 October 2026). This document is a research audit summary; the Windows-only original source code and tick archives are not uploaded.

## Original source locations

| Stage | Source file or artifact | Reproduced finding |
|---|---|---|
| Defended range detection | `research/manual_range_detector_comparison/scripts/phase4d_detector_c.py` | Detector C |
| Scenario A/B / FVG candidates | `research/three_way_detector_benchmark/phase4e1/scripts/phase4e1_c_fvg_replay.py` | Original candidate construction |
| Forensic Scenario audit | `research/three_way_detector_benchmark/phase4e2/scripts/phase4e2_audit.py` | Original checks |
| Phase 4E6 grouped midpoint scanner | `research/three_way_detector_benchmark/phase4e6_grouped_replay/scripts/execute_scan.py` | 1,099 candidates; 717 reaches; 382 non-reaches; zero quote missing |
| Source-backed SL1/SL2 construction | `research/three_way_detector_benchmark/stop_loss_comparison/scripts/run_stop_comparison.py` | Original stop outputs exactly equal |
| H4 target and SL/TP ledger | `research/three_way_detector_benchmark/sl_tp_backtest/scripts/run_sl_tp_backtest.py` | 3,930 original/reproduced ledger rows exactly equal |
| Original saved ledger (comparison reference, not new-signal source) | `research/three_way_detector_benchmark/sl_tp_backtest/ABC_SL_TP_TRADE_LEDGER.parquet` | Original C + SL2 + H4 = 308 |

## Audited stage reconciliation

| Stage | Count |
|---|---:|
| A/B/C eligible Phase 4E6 midpoint candidates | 1,099 |
| Actual bid/ask midpoint reaches | 717 |
| Non-reaches | 382 |
| Quote coverage missing | 0 |
| Detector C Phase 4E6 candidates | 499 |
| Detector C midpoint reaches | 335 |
| Detector C combined timestamp-parseable entries consumed by stop producer | 319 |
| Detector C invalid-stop exclusions | 11 |
| Detector C valid structural stop rows | 308 |
| Detector C final SL2 + H4 events | 308 |
| All detectors / stops / target variants in SL/TP ledger | 3,930 |

The difference between 335 reaches and 319 timestamp-parseable producer inputs reflects the **original producer's input eligibility and parsing stage**, not necessarily one single cause. Do not infer the precise rejection breakdown beyond the verified 11 invalid-stop exclusions.

- Tick scanner reportedly examined **135,426,651** GBPUSD BID/ASK tick rows.
- The downstream SL/TP producer separately scanned **133,166,553** tick rows.
- Identity and reach/non-reach status exactly matched all 1,099 saved source candidates.
- Original and reproduced full 3,930-row SL/TP ledger: **DataFrame equality TRUE**.
- Original and reproduced SHA-256: `0bec293e1027637c08d1f924279c1d5250d6476ce772ed073cb60d2d1347106a`.
- Original intermediate files also reproduced exactly: `ABC_STOP_LOSS_RESULTS.parquet`, `ABC_STOP_ANCHOR_AUDIT.csv`, `ABC_SL1_VS_SL2.csv`, and `ABC_SL_SURVIVAL_BY_HORIZON.csv`.

## Causal SL2 and H4 wick selection

- SL2 anchor from the prior FVG excursion, categorized as genuine sweep or a structural fallback.
- Buffer `max(0.15 × last completed H1 ATR14, 2 × activation BID/ASK spread)`.
- Long SL2 = anchor − buffer; short SL2 = anchor + buffer.
- Target = nearest **already-confirmed**, direction-eligible H4 swing wick.
- H4 pivot has two left and two right H4 candles; confirmation after closure of right candle #2.
- Long exit quote BID, short exit quote ASK.
- Avoid lookahead and futures-dependent pivot labels.

## Evidence and limitation

The user-reported local evidence file is `research/sl_tp_ledger_recovery/GBPUSD_MIDPOINT_SCAN_REPRODUCTION.md`; additional proof is in `PRODUCER_REPRODUCTION_REPORT.md`, `UPSTREAM_STOP_PRODUCER_REPRODUCTION.md`, `EVENT_STAGE_RECONCILIATION.csv`, and `RECOVERED_SOURCE_LOGIC.md`.

**Not attached to the repository:** script bodies, actual Parquet ledgers, source market ZIPs and intermediate equality outputs. Reported SHA equality is a stronger historical lineage result than candidate-count similarity alone; it does not prove broker-live execution or future trading returns.

Next: [EURUSD 2021 independent-instrument test](25-eurusd-2021-m0-holdout.md).
