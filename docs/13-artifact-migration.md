# Local-to-GitHub research artifact migration checklist

This repository was initialized with only a five-character README and no research files. The documentation was added through the GitHub connector from known user-reported research phases plus available monthly/yearly summary CSVs. The original complete local working tree **was not accessible through a GitHub URL**.

For a truly complete, independently reproducible repo, import the following original materials from your local `AMD-T1-FRESH` tree. Avoid blind recursive `git add .` because of hundreds of millions of proprietary-ish tick rows, Windows absolute paths and private settings.

## Mandatory source and config

- [ ] Original frozen Detector A Python source/config and hashes.
- [ ] Original frozen Detector B source/config and hashes.
- [ ] Original frozen Detector C defended-level source/config and hashes.
- [ ] Common breakout, continuation Scenario A/B, C3 FVG signal builder and corrected Scenario B rejection audit source.
- [ ] Final updated `execute_scan.py` from `phase4e6_grouped_replay/scripts`.
- [ ] SL-only, SL×TP run scripts, full run configurations and exact environment lock files.
- [ ] Synthetic 63-case regression suite plus scenario, bid/ask, pivot and checkpoint tests.

## Mandatory ledger and reports

- [ ] Full-scan JSON checkpoint and `ABC_EXECUTION_STATUS_AFTER_SCAN.parquet`.
- [ ] Range/FVG raw → representative → correction funnels for all three detectors, with original ID joins and excluded legacy artifacts.
- [ ] `SL_COMPARISON_MASTER_REPORT.md`, paired SL result parquet and audit CSVs.
- [ ] `ABC_SL_TP_TRADE_LEDGER.parquet`, `ABC_SL_TP_SUMMARY.csv`, paired and cost sensitivity CSVs, target audit, validation and source provenance.
- [ ] Verify original `ABC_SL_TP_MONTHLY.csv` and `ABC_SL_TP_YEARLY.csv` attached in the research conversation against the numbers recorded under `data/summary`.
- [ ] Preserve all 18-model full results; do not fabricate missing D1 or nearest-target metrics.

## Chart/diagram library

- [ ] Approved, anonymized discretionary chart screenshots showing defended ranges and wick sweeps.
- [ ] Approved stop placement screenshot showing distal FVG edge, SL1 and relevant sweep extreme.
- [ ] Blinded detector A/B/C chart panels and review score sheets.
- [ ] Drawings should describe whether they are toy illustrations vs market screenshots; cite symbol, timeframe, time basis and source.

## Provenance without distributing raw tick ZIPs

- [ ] Archive manifest: each monthly filename, source URL/license, first/last tick, row count, SHA256, session/candle time offset.
- [ ] Reconcile Feb–Jul 2023 missing-data warning before reporting complete coverage.
- [ ] Small *synthetic* quote fixtures with expected outcomes to permit CI testing without sharing 133 million tick rows.

## Avoid committing

Credentials, broker account identifiers, private exchanges, absolute `C:/Users/...` paths, personal emails, unrestricted binary dump archives, giant ZIPs, cache folders, editor temporary files and accidental API keys.

## Required final cross-check

Run hash and row-count comparison against the locally frozen source. Set tags documenting baseline and corrected cohort. Until those are imported and checked, this GitHub repo is an **extensive documentation archive**, not a complete verified reproduction package.
