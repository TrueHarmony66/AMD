# Detailed chronological research timeline

Every count refers to a particular experiment and should not be added to later totals without an explicit ID reconciliation.

| Phase | Work / finding | Result and caveat |
|---|---|---|
| Concept | Trader hand-drawn sideway defended levels, optional liquidity sweeps, directional close breakout, continuation/FVG midpoint | Long/short symmetry; sweeps not mandatory |
| Early A | Canonical range and multi-timeframe context | 365 H1, 162 H4 independent ranges; not visually verified |
| B initial | Raw wick-extreme/chop range mining | 2,322 raw H1, severe overlapping/nesting |
| 3 initial | Naïve entry scanner | **0/96 reaches INVALID**: expected wrong tick schema |
| 3 corrected | Correct four-column HistData tick parser and bid/ask direction | 37/96 within 12h; 42/96 by 24h; 54/96 by 48h; 58/96 by 72h |
| 3B–3C | Broaden and vet delayed continuation/FVG Scenario B | 42/99 within 12h, 50/99 by 24h, 63/99 by 48h, 68/99 by 72h; older selected cohort |
| 3D–3F | Evaluate occurrence-rate expectations and event geometry | Avoid equating FVGs, candidate orders, fills, trades |
| 3G.1 | Attempt to scale Python scanning | Per-tick conversions and archive rescans stalled |
| 3G.2 | Stream fixed-EST lexical sortable tick keys | 16,545,328 ticks in 33.53 seconds in separate benchmark (~493k/s) |
| 4A | Head-to-head range-detector experiment proposal | Freeze source criteria and share downstream FVG/entry logic |
| 4B | Raw B wick-chop candidates and overlap grouping | 2,322 raw, 600 grouping representatives; duplicates dominant |
| 4C | B causal representative FVG scan | 1,458 raw gap records → 382 representative-linked opportunities |
| 4D | C reaction/defended-level scanner | 1,705 H1 and 819 H4 ranges; 2,980 diagnostic breakout events |
| 4E.1 | C scenario FVG bridge | 1,635 provisional events; breakout timestamp/index join repaired |
| 4E.2 | Critical scenario re-audit | C Scenario B 399/1,504 valid, **1,105 invalid**; 131 valid Scenario A |
| 4E.3 | Unified corrected eligibility and dedup | A 239, B 361, C 499 = **1,099 detector-associated orders** |
| 4E.4 | First incomplete execution overlay | 50 processed vs 1,069 unprocessed mathematically inconsistent |
| 4E.5 | Reconcile verified status | A 0 processed, B 20 (13 reach), C 10 (8 reach): 30 processed, 1,069 remaining |
| 4E.6 | Full tick replay attempt | No fresh committed orders: per-order ZIP rereads, datetime overhead, batch commit delay |
| 4E.6.1 | Root cause and safe commit diagnosis | 3 more processed (A1 miss, B1 reach, C1 miss); 33/1,099 verified |
| 4E.6.2 | Grouped ZIP scan April 2024 | 1,640,965 ticks, 5 entries (2 reach, 3 miss), 50.213s/candidate; initially missing overlay |
| Execution-only | Scanner September 2022 | 4,834,358 ticks, 20 new entries (15 reach, 5 miss), reconciled missing five, 63 synthetic regression cases |
| **Full scan** | Removed hard-coded 20-order/single-archive limits; month-wise checkpoint | February 2021–December 2025, **133,166,553 quote rows**, 58 previous + 1,041 new, 1,099 done, **717 reach / 382 nonreach** |
| SL-only | Two stop placements on usable entered trades | Intermediate reached 382 stops, outer 279, 655 paired, 72h; not profits |
| TP definition | Trader confirmed exact H4 or D1 swing wick extreme | TP H4, D1, combined nearest; causal pivots required |
| SL×TP provisional | 18 combinations, bid/ask ordered exits | Selected H4 SL2 PF A 4.209 B 3.610 C 3.612; zero commission, provisional TTL/holding |
| Frequency | Uploaded monthly/yearly summaries independently parsed | C SL2/H4 **299 trades across 59 represented months**, mean 5.07, median 5, 0–12/month |

## What went wrong and was fixed

### 1. Parser mismatch produced false zero reaches
HistData ASCII tick CSV is exactly `datetime,bid,ask,flags`; do not expect a fifth column. Validation on known synthetic price trajectories is required.

### 2. Scenario B incorrectly qualified future gap patterns
Several delayed FVGs were accepted without sustained continuation or despite reclaim. C Scenario B invalidation of 1,105 of 1,504 provisional events was the most consequential causal correction. Legacy invalid events are audit records only.

### 3. Different event units were silently mixed
Ranges, raw gaps, validated FVGs, unique order IDs, correct-side midpoint touches, timestamp-backed fills, paired stop-ready entries, and TP-valid executed trades all have distinct denominators.

### 4. Execution bottlenecks and arbitrary caps
The old script rescanned entire monthly ZIPs for individual candidates, performed expensive tick-to-datetime conversions, and committed results too late. An experiment prompt also artificially restricted scanning to 20 candidates / one month, falsely resembling scanner incapacity. Final scanner streamed all monthly sources sequentially with persistent checkpoints and no cap.

### 5. Overlay and stale ledger discrepancies
First 4E results did not sum to 1,099 and omitted five completed cases. Event-ID-based, append-safe reconciliation and regression results resolved these; do not overwrite source checkpoints.

### 6. Repeated claims of profitability before real exits
A 65.24% midpoint price-reach rate is not win rate, and a 92% H4 TP-hit share with SL2 hides very small average winners relative to stop distance. The later 18-model backtest represents preliminary gross returns, not proof of implementable profitable trading.

## Release convention

For each experiment archive: exact frozen code hash, dated parameter set, data source, time basis, event IDs, selection counts, error logs, output paths, historical quote-side checks, target knowledge times, outcome distribution, and explicit unresolved gaps. Do not delete unfavorable or invalid historical results; annotate with invalidation rationale.
