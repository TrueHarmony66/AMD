# Integrity flags, limitations and interpretation policy

This document is intentionally explicit about known threats to validity.

1. **Gross rather than deployable net profit:** historical quoted spread modeled; commission reference was zero. Re-run cost sensitivity with broker-specific commission per lot, swaps, adverse SL gap fills, realistic order rejection, trading hours and margin.
2. **In-sample parameter selection:** all 18 combinations were evaluated on same historical sample; choosing highest historical PF is subject to data snooping. Require isolated chronological out-of-sample/forward data without reoptimization.
3. **Overlapping trades:** trade-level independent simulated R cannot be summed to cash equity assuming unlimited concurrent funded orders. Need deterministic single-position/portfolio position gate and overlap conflict audit.
4. **Provisional lifecycle:** 12h pending TTL, 72h time exit, no BE/trail were study assumptions, not final approved trading policy. Need sensitivity and final rule approval.
5. **TP causality risk:** past pivot high/low must be confirmed at target assignment, including two right-side candles when default 2×2 definition is used. Validate every trade's known-at timestamp.
6. **Entry status discrepancy:** 717 final reached records; 680 old timestamp records; 24 recovered; 13 unresolved; 655 matched SL-ready; document the 49 additional exclusions via order IDs. The legacy 696 reach number was a different revision.
7. **Time exits suspiciously absent** in selected H4 rows where TP+SL equals total trade count; may be legitimate but demands first-hit replay audit and proof holding window honored.
8. **Paired comparison counts differ:** SL1/SL2 H4 sample size differs for B and C. Strict identical-event comparison mandatory before attributing differences solely to stop placement.
9. **Historical 2023 coverage contradiction:** earlier Feb–Jul gap versus months in later ledgers; independently verify monthly archive provenance.
10. **A/B/C order overlap:** 1,099 are detector-associated records, not automatically 1,099 unique independent opportunities. Shared signals must be identified by matched times, prices, and event geometry.
11. **Win-rate framing:** ~93% H4/SL2 is TP-hit share among selected modeled trades, not confirmed funded-account win rate. Avg realized R (~0.17–0.21) much smaller than winning proportion implies many tiny wins relative to SL distance.
12. **Unlabeled human chart audit:** Detector C expresses manual preferences but the chart gallery lacks independent human structural range quality labels.
13. **Loss of original source context:** local scripts, per-trade Parquet, all 18 combination summaries and complete tests were not available to this documentation author; documented claims are based on supplied historical outcomes and uploaded monthly/yearly summaries.
14. **Prior experimental failures must not be hidden:** misparsed tick records, bad Scenario B, slow scans, stale checkpoint overlay and artificial batch caps must be retained for audit.
15. **Reproducibility:** full quote ZIP hashes, exact source tree commits, Python environment, rounding precision, DST/candle time alignment, synthetic tests and deterministic checkpoint replay are needed for full reproducibility.
16. **Return distributions:** coarse mean R/PF and max DD not a substitute for trade-by-trade drawdown, annual uncertainty intervals, longer loss streak, per-side outcomes and regime stress.
17. **Discretionary liquidity language:** 'liquidity sweep' names a wick break/reclaim or targeted price level proxy, not a measurement of actual resting market orders.
18. **Repository visibility:** this GitHub repository is public as inspected; no credentials, private account numbers, trader-identifying file paths, large licensed tick data or broker secrets should be added.

## Decision criteria

A detector/exit variant is only a **provisional historically positive candidate** if (a) auditable causal trade ledger, (b) full broker-inclusive costs, (c) no duplicated capital/overlap error, (d) stable yearly and regime outcomes, and (e) untouched out-of-sample evidence are all positive under the same precommitted rules.

Do not claim A/B/C are *proven* profitable before satisfying these gates.
