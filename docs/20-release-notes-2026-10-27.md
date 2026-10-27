# AMD T1 — Research release notes (27 October 2026)

**Release type:** documented historical research milestone, **not** an executable trading software release.

## What has changed since the previous GitHub documentation release

- **Phase 7:** audited post-H4 D1 liquidity reachability, corrected horizon counts, rejection/continuation classifications and stop-survival interpretation. The final 72h *post-H4* tag count is **214/272** target-eligible H4 winners. See [Phase 7](16-phase7-h4-d1-continuation-audit.md).
- **Phase 8:** froze M0–M5 stop-management variants, found missing partial-fill quotes and stop-amendment logs, corrected 72h portfolio-overlap suppression and a major PRE_H4_SL accounting bug that had fabricated ~50× PF in interim control results. See [Phase 8 chronology](17-phase8-runner-models-and-reconciliation.md).
- **Phase 8.3:** ran a full historical quote-level comparison, 128,332,195 GBPUSD ticks across 308 source opportunities and all six fixed models. Reported simulated **M0 +$1,340.29, PF 3.401, 86.11% net WR, +0.1803R**, still **provisional**. M1–M5 showed lower modeled net dollars than M0 on this history and remain provisional due to broker validity assumptions, gaps and incomplete event evidence. See [full results](18-phase8-3-full-tick-results.md).
- **EURUSD holdout:** 2021 data archives verified (12/12); original precommit for 2025 superseded by user-selected 2021 before checking performance. Holdout **not run** because portable Detector C + Scenario A/B + FVG + SL2 event generator and GBPUSD event parity are missing. See [portability blocker](19-eurusd-2021-portability-blocker.md).
- Visual diagram gallery from the earlier release remains at [seven illustrated SVG examples](15-visual-diagram-gallery.md).

## Interpretation

This release **does not** claim profitable live execution, investor-grade audited returns, broker-specific valid stop amendments, fully reproducible source code, or generalized EURUSD performance. The Phase 8.3 completed model summary **cannot** be reproduced from this GitHub repository alone until the user pushes the actual local source, tick archives (or access instructions), original event ledgers and fills.

## Recommended next engineering milestone

Recover the exact signal generator, demonstrate GBPUSD source-event parity, then execute untouched EURUSD 2021 M0. Do not use EURUSD as an iterative parameter-optimization dataset.

## Files included in this GitHub documentation release

The GitHub tree includes these research summaries, the previous foundational strategy docs, the prior historical aggregate CSVs and the seven conceptual SVG diagrams. **No** new raw tick ZIPs, Parquet trade ledgers, source scripts or locally calculated full model CSVs were uploaded.

Release documentation prepared on 2026-10-27, based on research results reported during this conversation.
