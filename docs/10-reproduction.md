# Reproduction protocol and expected local artifacts

## Source manifest to import from local machine

The current GitHub docs do **not** contain the original local Windows research engine. Reproduce only after adding or referencing the exact frozen Python source code, scanner scripts, detector configurations, source hashes and artifact manifests. See [migration checklist](13-artifact-migration.md).

### Primary project layout (proposed for source import)

```text
AMD/
  README.md
  docs/
  data/
    summary/monthly-h4-sl2-trade-counts.csv
    fixtures/                 # redistributable synthetic ticks
    manifests/                # SHA256 and archive date coverage (no raw paid/licensed ticks)
  src/
    detectors/{A,B,C}/        # archived frozen source, not reconstructed imitations
    signal/                   # shared breakout/Scenario A/B/FVG engine
    replay/                   # original historical quote replay
  tests/
    parser/
    causality/
    quote_side/
    scenario_b/
    checkpoint/
    sl_tp/
  research/
    outputs/                  # selected small CSV/metadata artifacts
    checkpoints/              # selected reproducibility metadata
```

## Deterministic replay expectations

1. Freeze source/tree hash, Python version, dependencies, numeric types and input data SHA256.
2. Verify each 2021–2025 monthly ZIP is discoverable, including every claimed 2023 month.
3. Verify raw four-column parse and source time basis.
4. Rebuild H1/H4/D1 candles; assert same completed-bar boundaries and pivot confirmation times.
5. Re-run Detector A/B/C unchanged; reconcile 239/361/499 corrected eligible order IDs.
6. Verify each order first quote is on/after causal order activation.
7. Stream ZIPs in chronological order; classify 1,099 records as 717 reached, 382 not reached.
8. Reconstruct exact 655 paired stop-valid entries from final 717; publish exclusion reasons for remaining 62 (13 unresolved timestamps plus 49 other exclusions, some missing anchors).
9. For each entry and 6 exits, calculate exact known-at HTF target and first postfill bid/ask event; no future pivots.
10. Reconcile SL1/SL2/H4 event counts, time exits, realized R, PF, DD and monthly/yearly totals.
11. Test crash/restart partway through a ZIP; checkpoint writes atomic and idempotent.
12. Compare imported original source against a fresh independent runner on sampled orders; never auto-correct original results silently.

## Synthetic fixture tests to retain

- 4-column HistData parser accepts expected schema; invalid row handling explicit.
- C3 cannot trade before close; delayed Scenario B cannot exist without continuation.
- FVG is directional and nonzero.
- Buy entry only triggers from ask, sell entry from bid.
- Buy SL/TP from bid; sell SL/TP from ask.
- Broker-spread spikes do not manufacture midpoint reaches.
- Exact TP wick extreme and causal swing confirmation.
- Overnight/month boundary lookback and order lifetime.
- Entry already marketable; same-tick SL, quote jumps and illiquid market close.
- A/B/C IDs unique within variant, exact shared-event matching across variants.
- 72h expiry and no double-closing of trades.
- Deterministic 0–12 monthly trade counts for C under H4/SL2 source CSV.

## Known local paths (relative)

```text
research/three_way_detector_benchmark/phase4e6_grouped_replay/execution_only/
  FULL_SCAN_CHECKPOINT.json
  ABC_EXECUTION_STATUS_AFTER_SCAN.parquet
research/three_way_detector_benchmark/phase4e6_grouped_replay/scripts/
  execute_scan.py
research/three_way_detector_benchmark/stop_loss_comparison/
  SL_COMPARISON_MASTER_REPORT.md
  ABC_STOP_LOSS_RESULTS.parquet
  ABC_SL1_VS_SL2.csv
  ABC_SL_SURVIVAL_BY_HORIZON.csv
  ABC_STOP_ANCHOR_AUDIT.csv
  SL_REPLAY_CHECKPOINT.json
research/three_way_detector_benchmark/sl_tp_backtest/
  SL_TP_MASTER_RESULTS.md
  ABC_SL_TP_TRADE_LEDGER.parquet
  ABC_SL_TP_SUMMARY.csv
  ABC_SL_TP_MONTHLY.csv
  ABC_SL_TP_YEARLY.csv
  ABC_SL1_VS_SL2_PAIRED.csv
  ABC_LIQUIDITY_TARGET_AUDIT.csv
  ABC_ENTRY_COHORT_RECONCILIATION.csv
  ABC_EXECUTION_COST_SENSITIVITY.csv
  SL_TP_BACKTEST_CHECKPOINT.json
  SL_TP_BACKTEST_CONFIG.json
  SL_TP_VALIDATION_STATUS.md
```

Check actual presence and hash before treating any file in this list as a verified artifact; the list combines user-shared output paths and requested output names.

## Version protocol

Preserve upstream branch/tag for each frozen detector and scenario-audit correction. Save one machine-readable run manifest with inputs, SHA256, date span, assumed session, quote/spread scheme, lifecycle rules, output SHA256, and test status. Don't include raw broker account credentials, email, or personal Windows user path.
