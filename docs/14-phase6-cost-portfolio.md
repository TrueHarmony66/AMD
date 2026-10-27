# Phase 6 — Transaction costs, dynamic lot sizing, one-position portfolio

**Research milestone:** 27 October 2026.

**Status:** User-reported Codex local historical execution completed using existing `ABC_SL_TP_TRADE_LEDGER.parquet` without repeating the 133,166,553 tick-row scan. No detector rules, initial limit/FVG geometry, MT5 configuration or GSR files changed. **This publication records reported outputs, not an independent audit of the local Parquet or Python source.**

## The question

After the promising **gross** H4 swing-wick take-profit backtest for all three frozen detectors, what remains after accounting for (i) commission, (ii) execution slippage, (iii) financing/swap assumptions, (iv) position-size rounding/margin and (v) one-position account restrictions?

Use the same existing **SL2** (known sweep/swing extreme plus max(0.15 × completed H1 ATR14, 2 × entry spread) buffer) and exact historically confirmed **H4 swing wick TP**. The stop and target stay frozen after activation. Initial research capital $5,000 USD; 0.5% dynamic risk of available equity; trade/lot sizing based on entry-to-stop risk with volume and margin constraints; one active position per detector-account experiment. The original Phase 6 requested 0.25%, 0.5% and 1.0% risk sensitivity and 18-combination ranking, but only baseline H4/SL2 values were supplied to this archive; **no unsupported sensitivity results are invented**.

## Step 1: Previous gross baseline reconciled

| Detector | Original independent-gross H4/SL2 trades | Average gross R | Gross PF |
|---|---:|---:|---:|
| A canonical | 141 | +0.210 | 4.209 |
| B extreme wick | 189 | +0.169 | 3.610 |
| C defended level | 299 | +0.195 | 3.612 |

The Phase 6 execution report said these figures were reconciled against the saved local trade ledger. Be careful: the portfolio counts below differ (A −1; B same; C −3), so average gross R versus net R differences are **not exclusively a pure cost-drag measurement**.

## Step 2: Model-cost + 0.5% risk portfolio outcomes

The user reported the following **base modeled-cost** results:

| Detector | Portfolio trades | Net profit USD | Net account return | Modeled net PF | Avg net R | Reported maximum **balance** drawdown USD | Ending account balance USD |
|---|---:|---:|---:|---:|---:|---:|---:|
| A | 140 | +595.14 | +11.90% | 3.630 | +0.188 | 50.26 | 5,595.14 |
| B | 189 | +647.55 | +12.95% | 3.117 | +0.149 | 73.59 | 5,647.55 |
| **C** | **296** | **+1,284.03** | **+25.68%** | **3.200** | **+0.174** | **101.08** | **6,284.03** |

All starting from the same $5,000 initial capital, and each A/B/C as a **separate** one-position simulation. Dollar P&L reconciles arithmetically with ending balance; return is P&L / $5,000. Net PF and realized R require exact trade ledger for independent verification.

In this *specific* model:
- Detector A exhibits the largest reported **net profit factor** (3.630), not C.
- Detector C generates the most modeled dollar gains, with 296 entered portfolio trades, positive average reported +0.174R, and 25.68% total modeled historical return.
- C's counted entries fall only three (299→296) in the completed-entry one-position model; this is **not** a valid full pending-order concurrency audit.
- A and B also show positive results under the **modeled assumptions**, not guaranteed real-broker profitability.
- 296 modeled C trades / 59 represented calendar months ≈ **5.02 trades per calendar month on average**; this is a derived overall mean, **not** an independently validated new per-month min/max range. Previous independent-entry C monthly distribution (299 trades) had 0–12, and its per-month counts should not be transferred unchanged to the 296-trade one-position portfolio.

## Step 3: Explicit cost and implementation boundary

- **Commission and slippage:** hypothetical low/base/stress profiles used by local Codex, not verified broker account tariffs. The research prompt proposed $4/$7/$10 per standard lot round-trip and 0.1/0.5/1.0 pip adverse stop/market-exit slippage as possible cases; **this report did not provide the effective realized base assumptions or detailed trade deductions**, so these proposals must not be stated as confirmed effective inputs.
- **Spread:** already represented historically as bid/ask. Charging it a second time would double-count costs.
- **Swaps:** historical direction-dependent broker financing could not be recovered. **Reference swap contribution was zero.** A strategy that occasionally holds overnight is not fully broker-cost-adjusted without a financing sensitivity.
- **Risk and lot sizing:** the reported base scenario used 0.5% of dynamic current equity; confirm broker GBPUSD contract specification, tick value, volume step, minimum lot, margin currency/conversion and gap risk in original sizing-audit artifacts.
- **Leverage and margin:** test prompt suggested 1:100, but effective broker-dependent leverage and historical free-margin checks must be verified from `BROKER_SPEC_AND_ASSUMPTIONS.json` rather than assumed confirmed.
- **Concurrence:** simulation used only completed-entry opportunities and therefore **could not reconstruct interference between multiple resting/unfilled pending limit orders**. A completely chronological order-state simulation might take fewer entries than this Phase 6 count.
- **Drawdown:** reported $50.26/$73.59/$101.08 are maximum *realized balance* drawdowns. **Not mark-to-market equity drawdowns**, which can be materially larger with wide stops.
- **Unresolved market data:** an earlier audit flagged missing February–July 2023 tick source coverage while later monthly results contain trades then. This discrepancy remains unresolved and could alter outcomes.
- **Time exits:** the earlier H4 variants had no reported time exits despite a 72-hour limit; audit first-hit event order, actual open/close timestamps and the time-exit logic.
- **No unseen holdout:** these tests were run on studied 2021–2025 prices. Optimizing after seeing results contaminates the same sample.

## Cost-model interpretation

The gross-to-model-net shifts are directionally sensible (e.g. C PF 3.612→3.200, A PF 4.209→3.630), but no exact cost contribution is available here without `ABC_COST_BREAKDOWN.csv`, `ABC_COST_STRESS_TEST.csv`, `ABC_NET_TRADE_LEDGER.parquet` and broker-input manifest.

The results **do not establish that three variants are fully profitable under real current broker terms**. The accurate conclusion is: under **one specified hypothetical commission/slippage profile with no swaps** and a simplified one-position rule, all three variants have historically positive modeled returns; C produces highest modeled absolute return, A highest modeled PF.

## Outputs reported locally (not yet imported)

```text
research/three_way_detector_benchmark/realistic_cost_portfolio_test/
  NET_PROFITABILITY_MASTER_REPORT.md
  ABC_NET_PROFITABILITY_SUMMARY.csv
  ABC_COST_STRESS_TEST.csv
  ABC_NET_TRADE_LEDGER.parquet
  ABC_COST_BREAKDOWN.csv
  ABC_MONTHLY_NET_RESULTS.csv
  ABC_YEARLY_NET_RESULTS.csv
  ABC_POSITION_SIZING_AUDIT.csv
  ABC_CONCURRENT_TRADE_AUDIT.csv
  BROKER_SPEC_AND_ASSUMPTIONS.json
  EXECUTION_VALIDATION.md
  RUN_CHECKPOINT.json
```

The first four paths were linked by the user as local Windows files. The remaining are **requested/expected** artifacts from the prompt and must be checked for existence; do not assert they were actually produced.

## Immediate next validation

1. Import the exact original source and phase-6 summary/sensitivity inputs, compute file hashes and confirm local file existence.
2. Fix 2023 quote archive provenance contradiction before final approval.
3. Verify timestamps, first-hit TP-vs-SL ordering, same-tick/price-gap handling, 72h end and why no H4 timeouts appear.
4. Confirm broker contract/commission/swap profiles and translate into explicitly bracketed financing scenarios.
5. Run full order-state chronology (pending orders, fills, cancellations, possible portfolio competition) and quote-level **equity** drawdown, rather than completed-entries-only position suppression.
6. Independent out-of-sample/paper-forward validation after rules frozen; only then consider MT5 deployment.

**Do not optimize to achieve 5 trades per month or declare a live strategy based on this in-sample return table.**
