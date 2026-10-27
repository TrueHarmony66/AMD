# Stop-loss and higher-timeframe liquidity take-profit

## SL alternatives (paired experiment)

The user marked an intermediate stop **between the distal FVG edge and a historically known liquidity sweep / swing extreme**. A second structural method places the stop **beyond the sweep extreme**, with a buffer.

For LONG (buy) with a usable known swing/sweep low S and FVG lower edge F:

- **SL1 intermediate (user):** (F + S)/2.
- **SL2 outer structural:** S − max(0.15 × H1 ATR14, 2 × activation spread).

For SHORT (sell) with a usable known swing/sweep high S and upper FVG edge F:

- **SL1 intermediate:** (F + S)/2.
- **SL2 outer structural:** S + max(0.15 × H1 ATR14, 2 × activation spread).

Halfway positioning and buffer are *research approximations* used to make ideas reproducible, not universally approved optimal levels. Sweep anchor required when genuinely available; otherwise a separately labeled **confirmed structural swing fallback**. No valid anchor ⇒ do not invent one. Must be known at entry. Validate that SL lies strictly on loss side of entry and trades can execute.

### 72-hour stop-hit-only study

| Detector | Paired entries | SL1 hits | SL2 hits | SL1-only hits | SL1 median stop pips | SL2 median stop pips |
|---|---:|---:|---:|---:|---:|---:|
| A | 152 | 88 | 63 | 25 | 27.39 | 41.13 |
| B | 195 | 103 | 84 | 19 | 27.28 | 50.16 |
| C | 308 | 191 | 132 | 59 | 23.45 | 45.91 |
| TOTAL | 655 | 382 | 279 | 103 | — | — |

Anchors in stop study: 255 genuine sweep, 400 structural fallback, 25 without valid anchor. Survival alone does not imply profit, and SL2 is expected to trigger no more often than SL1 for otherwise identical paths if properly ordered.

## User-approved TP philosophy

Take profit **exactly at the historical wick extreme** of a previously causally confirmed H4 or D1 swing in the profit direction. Not ahead of level, not beyond to demand a sweep.

- LONG: wick HIGH of an eligible H4/D1 swing above entry.
- SHORT: wick LOW of an eligible H4/D1 swing below entry.
- **TP H4:** nearest eligible confirmed H4 swing extreme.
- **TP D1:** nearest eligible confirmed D1 swing extreme.
- **TP Combined:** nearer eligible qualifying level among H4 and D1.
- Confirmed pivot must have its required **right-hand confirming candles closed** before it becomes known. Provisional fallback pivot: two left and two right completed candles; use frozen preexisting pivot if available and documented.
- Freeze target when pending order becomes eligible; no future high/low selection, no substitution with a fixed-R target when missing.

The SL×TP matrix has **3 detectors × 2 stops × 3 targets = 18 combinations**.

## Provisional trade lifecycle used for first outcome backtest

- A not-yet-final user-approved **12h pending entry TTL**.
- Max observation/holding period **72 elapsed hours** after fill; time exit at first available executable quote after limit.
- No partial TP, breakeven, trailing stop or unapproved post-fill cancellation.
- Independently simulated trades, permitting overlapping modeled trade paths. That is not a realizable one-position-at-a-time portfolio.
- Bid/ask tick chronology chooses whichever executable SL/TP event occurs first; long exits on bid, short exits on ask. SL gap must use executable quote, not guaranteed stop level.
- Zero-commission reference. Spread represented in historical quotes; do not double-charge. Real commissions, swaps, fills, order latency and funded-account risk limits remain unmodeled.

## Fair evaluation

SL2 reduces stop-hit frequency but widens initial risk and frequently reduces positive TP outcome measured in R. Compare realized net R and cost/overlap sensitivity, not just TP hit share. SL1 remains an archived tested alternative. See [outcome results](07-sl-tp-results.md).

### Diagram

~~~mermaid
flowchart TD
 E[BUY LIMIT at 50% FVG] --> X[Two predeclared SL models]
 X --> S1[SL1: halfway between FVG distal edge and known sweep/swing]
 X --> S2[SL2: outside known sweep/swing + buffer]
 E --> T[Known H4 and/or D1 swing HIGH wick]
 S1 --> Q[Chronological bid/ask exit replay]
 S2 --> Q
 T --> Q
 Q --> R[TP first / SL first / time exit / missing coverage]
~~~
