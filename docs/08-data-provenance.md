# Historical data sources, clock semantics, and coverage

## GBPUSD tick sources

- HistData monthly ASCII tick ZIP archives with four comma-separated fields `datetime,bid,ask,flags`.
- Raw archive periods described as February 2021 to December 2025.
- Source time zone reportedly **fixed EST** in the earlier research. This convention needs hash-verified confirmation from the final `execute_scan.py` script and input manifest before public reproducibility can be claimed; fixed EST is **not** equivalent to civil US Eastern Time with DST.
- Local complete scan processed **133,166,553 rows**. It was resumed by ZIP/month, checkpointed after each archive, and could skip previously verified order IDs.
- Do not upload the 133M-tick ZIP corpus to Git history without legal/provenance, licensing and storage planning. Prefer download/checksum manifest and a documented, small redistributable synthetic fixture.

## Candle construction and causality

Construct H1, H4 and D1 bars with explicit clock boundaries from tick source; log the source offset, normalized UTC, aligned bar-open and bar-close time. For target swings, a pivot at bar t with right confirmation k is only available after t+k closes, not on bar t.

A study using broker server time, daylight saving offset or shifted H4 bar opens can materially change pivot dates and selected take-profits. Every result is tied to a precise candle alignment.

## Coverage problem requiring investigation

An earlier data audit reported a missing **February–July 2023** source-data interval, yet the later full-scan report and the uploaded `ABC_SL_TP_MONTHLY.csv` contain nonzero modeled trades in all six months. The full-scan summary simultaneously claimed **zero missing source coverage**. These statements cannot all be accepted without reconciling final archive inventory and trade-ID quote provenance.

Do not silently assume the 2023 gap was resolved, or that earlier gap findings were correct. Check archive file hashes and the 2023 timestamp/quote distribution against the precise July and February month boundaries. Include per-month quote availability, sampled first/last tick timestamps, unresolved gaps, and source version.

2022-09 has **zero C SL2/H4 modeled trades** despite the existence of a scanned September 2022 ZIP; zero trades does not imply zero market data.

## Files in local working tree

Representative Windows root used by the original researcher:

`AMD-T1-FRESH/` (relative, under user's local Documents directory)

Relevant reports:
`research/three_way_detector_benchmark/phase4e6_grouped_replay/execution_only/FULL_SCAN_CHECKPOINT.json`
`research/three_way_detector_benchmark/phase4e6_grouped_replay/execution_only/ABC_EXECUTION_STATUS_AFTER_SCAN.parquet`
`research/three_way_detector_benchmark/phase4e6_grouped_replay/scripts/execute_scan.py`
`research/three_way_detector_benchmark/stop_loss_comparison/...`
`research/three_way_detector_benchmark/sl_tp_backtest/...`

Local file paths are not web-accessible GitHub source links. These original sources were described by the user but **not copied into this repository**. See [migration](13-artifact-migration.md).
