# FVG entries and historical executable-price verification

## Quote-side lifecycle

A 50% FVG buy limit is evaluated against the **ask**; a sell limit against the **bid**. For an opened BUY, SL and TP later evaluate against **bid**. For an opened SELL, SL and TP later evaluate against **ask**. This distinction prevents phantom fills based on the wrong side of the spread.

Order activation is strictly after all causal signal confirmation. Distinguish:

1. Valid FVG formation;
2. Order eligible to be placed;
3. First eligible historical quote;
4. Already-marketable on first quote versus still pending;
5. Reach while the order is notionally active;
6. Independently simulated position exit.

Price reachability at 12h is not a 12h market win rate. Order rejection, cancellation, concurrent risk, and live routing were outside the original entry-only test.

## Major execution integrity corrections

- Original Phase 3 observed **0/96** 12-hour entry price reaches because the tick parser silently expected 5 fields, while HistData CSV rows actually have four: **datetime,bid,ask,flags**. The zero result is invalid and archived as a failure.
- Correct four-field parser established **37/96 reaches at 12h**, 42/96 at 24h, 54/96 at 48h, 58/96 at 72h.
- Phase 3B widened scenario recall and Phase 3C found **42/99 reaches at 12h**, 50/99 at 24h, 63/99 at 48h, 68/99 at 72h. Those 99 are a previous selection cohort, not the later corrected 239 A-order universe.
- Detector C Scenario B audit invalidated 1,105 earlier events, preventing misleadingly high event counts.
- Early 4E replay status had a **20-candidate legacy-C inclusion** discrepancy, then a five-record overlay discrepancy; both were reconciled.
- Once batching limits were removed, the full scanner processed all 1,099 corrected order memberships.

## Final corrected entry-only full replay

| Detector | Eligible | Reach at 12h | Verified nonreach | Reach share |
|---|---:|---:|---:|---:|
| A | 239 | 158 | 81 | 66.11% |
| B | 361 | 224 | 137 | 62.05% |
| C | 499 | 335 | 164 | 67.13% |
| TOTAL detector-associated | 1,099 | 717 | 382 | 65.24% |

The final execution report recorded **0 unprocessed and 0 missing-source-coverage candidates**. Across the full scan, about **133,166,553 quote rows** were processed spanning recorded source months in 2021–2025.

### Do not mix entry denominators

The later SL-only research used a legacy intermediate **696-reach ledger**, with 680 timestamp-backed entries, 655 paired stop geometries. The later SL×TP cohort reconciled **717** full-scan reaches; 680 timestamps pre-recovery + 24 newly recovered = 704; **13** remained unresolved; only **655** passed paired stop/target inclusion. These are not contradictions to hide—different stages/filters must be documented with order-ID-level ledgers.

## Historical replay performance recovery

- Phase 3G.1 naïve Python tick datetime approach did not finish any of its first 12 expansion candidates.
- Phase 3G.2 streamed ZIP entries with sortable fixed-EST timestamp keys: **16,545,328 ticks / 33.53s**, about **493k rows/s** in its separate benchmark.
- 4E.6 showed zero new committed orders due to repeated per-candidate ZIP rescans, expensive timestamp conversion and delayed batch commits.
- 4E.6.1 proved 3 new orders and safe checkpoints.
- 4E.6.2 scanned April 2024 once (1,640,965 rows), finished 5 orders, but **50.213s/order**, slower than expected; 5 results initially missing from cumulative overlay.
- Execution-only script resolved stale overlay and verified 20 fresh September 2022 orders from 4,834,358 ticks; then uncapped full execution scanned February 2021–December 2025, **133,166,553 rows**, completing remaining 1,041 records.

## Recommended invariants for code import

Stable order IDs; immutable raw/corrected cohorts; idempotent checkpoint/status overlay; exact timezone schema; valid first-quote handling; correct buy/sell quote side; exact C3 activation; conservative spread/gap handling; month-boundary windows; explicit missing-quote status; no premature nonreach classifications.

The full Python scanner and tick archives are local project artifacts **not yet imported into this GitHub repository**.
