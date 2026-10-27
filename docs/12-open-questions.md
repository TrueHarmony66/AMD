# Research roadmap, unresolved issues and release gates

## Highest priority: validate supplied backtest (do not tune parameters yet)

1. **Audit missing 2023 quote coverage contradiction**: earlier Feb–Jul 2023 hole vs positive modeled outcomes; inspect monthly ZIP provenance and dates before treating all 59 months equally.
2. Recover or explicitly exclude the **13 reached records still missing reliable entry timestamps**; document why another **49** timestamp-backed records missed the 655 paired cohort.
3. Verify every TP target knew its H4/D1 pivot right-side confirmation before order activation; check timestamp and candle boundary interpretation.
4. Explain why all reported H4/SL2 outcomes are TP or SL and none a time exit, under a stated 72h rule.
5. Reconcile different sample sizes for B/C SL1 vs SL2 H4 TP; make rigorous matched ID comparison.
6. Add full raw 18-model `ABC_SL_TP_SUMMARY.csv`, full trade ledgers and baseline source code with hashes.

## Next: implementability, not number-chasing

7. Recalculate commissions, broker stop slippage, swaps, uncertain spread conditions and spread spike sensitivity.
8. Implement explicit single-position/maximum-concurrent risk, multiple FVGs per range, session rules, pending limit cancellation, weekend order policy and margin; report trade count and portfolio DD after overlaps removed.
9. Compare H4-only, D1-only, nearest H4-or-D1 on exactly the same eligible TP-cohort with no lookahead and false target fills.
10. Evaluate time exit horizon 12/24/48/72h and pending TTL choices **only as preplanned robustness studies**, not choose the best blindly from the same sample.
11. Stratify Scenario A/B, authentic sweep/fallback, buy/sell, market sessions, trend/chop volatility regimes, and year; bootstrap uncertainty with correlation-aware time blocks.
12. Hold out unseen chronological segment after locking rules, then run paper/forward demo broker executions with exact costs.
13. Independently hand-label blinded chart panels to evaluate whether C truly matches trader's intended defended levels better than A/B.
14. Prepare separate source and test packages for A, B, C while maintaining shared downstream breakout/FVG and execution machinery.
15. Produce a reproducible GitHub release with machine-readable provenance, diagrams and a transparent changelog of research corrections.

## Release gate definitions

- **Documentation archive**: this initial repository, with records and caveats, without claiming to contain unavailable local code.
- **Source-complete research release**: original code, configs, synthetic tests and compact auditable ledgers imported from local storage and verified by hashes.
- **Historical edge candidate**: all source/audit discrepancies closed and net, after-cost, overlap-constrained results positive.
- **Live-ready**: independent out-of-sample and forward demo evidence + risk controls + verified broker execution; not yet achieved.

## Principle

Three variants should be *included*, not labeled all profitable by assumption. If A or B loses after realistic costs or a holdout, record that result; never hide it just to show a profitable repo.
