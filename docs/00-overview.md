# Overview, motivation and research scope

## Research question

Can the **AMD T1** range breakout / three-candle FVG midpoint-limit method produce repeatable, realistic trading expectancy on GBPUSD while capturing an acceptable number of high-quality opportunities?

The discretionary trader initially sought around **5–6 genuinely good setups per covered month**, of which **1–3 exceptional setups** with executable midpoint returns. These are *aspirational* and must not be used to tune parameters in-sample.

The research evolved from (1) range discovery, through (2) breakout/FVG association, (3) real bid/ask midpoint price reachability, (4) comparison of three range-detector concepts, to (5) paired structural stop and confirmed higher-timeframe swing-wick liquidity targets.

## Original manual requirements, clarified with charts

- Detect obvious horizontal sideways price chop with repeated highs, lows and reactions.
- At formation, prefer price levels defensible as prior **reaction/defended structure**, often aligned with wick extremes.
- The **absolute outermost wick is not always the correct range line**: if a candle briefly pierces a repeatedly defended level and closes back within the consolidation, treat it as a **sweep** and preserve the level.
- Confirm breakout by a **completed directional candle close beyond a frozen level**, never a wick breach alone.
- Larger breakout + directional next candle can form Scenario A; smaller first breakout + delayed genuine continuation and FVG can form Scenario B.
- FVG is three completed candles; exact pending entry is **50% of the gap**.
- For TP, prefer the **exact previously confirmed H4 or D1 swing wick extreme** in the trade direction, not a pip buffer before or beyond that level.
- SL1 lies between the distal FVG edge and relevant known sweep/swing extreme; SL2 is beyond the known extreme plus volatility/spread buffer.
- Trader chose Detector C as *current focus* while keeping A and B in the eventual repository.

The AUDUSD H1/H4 screenshots used to clarify drawing behavior are **illustrative specification examples**, not GBPUSD validation samples and not performance evidence.

## Historical context

- GBPUSD H1 is the primary signal timeframe; H4 ranges were separately examined and H4/D1 swings supply structural TP context.
- Local historical study used 2021–2025 HistData monthly ASCII tick archives, reconstructed candles and a fixed source EST offset used by the original research.
- Distinct research populations differ: 365 H1 A ranges; 2,322 raw B; 1,705 H1 C; 1,099 corrected *detector-associated* eligible orders.
- Results have been revised after parser failures, causal Scenario B misclassification, legacy candidate exclusion, and stale execution status overlays.

## Evidence hierarchy

1. Raw quote and candle data, locally available.
2. Frozen detector/signal source + hashes and complete event ledgers, locally available.
3. Corrected full historical candidate-to-tick replay: 1,099/1,099 eligible records classified.
4. Paired SL-only result set: 655 valid paired entries.
5. Provisional SL×H4/D1 swing-target trade-level outcome ledgers; H4 results reproduced from user-reported summaries.
6. Monthly and yearly summary CSVs supplied as conversation attachments and independently parsed for this documentation.
7. Manual visually blinded chart review still **unlabeled**; visual range accuracy has not been measured as a reviewer statistic.
8. Live/external robustness still **unproven**.

See [limitations](09-limitations.md) before treating any historical PF as an implementable edge.
