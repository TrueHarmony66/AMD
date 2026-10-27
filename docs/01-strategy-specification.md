# Strategy specification — AMD T1 range breakout / FVG midpoint

## 1. Price structure and confirmation

On completed H1 candles, a detector emits a confirmed, frozen range [L, U] at a causally observable time. Detector-dependent range selection is the experimental variable. No future candle may define earlier boundaries or confirmation times.

A candle with high > U but close ≤ U is an **upper sweep**; a candle with low < L but close ≥ L is a **lower sweep**. This is a geometric description, not proof of institutional liquidity activity.

A directional close beyond U/L is a **breakout candidate**, not necessarily an independently confirmed tradable breakout. Record body/ATR, real-body penetration, close location, wick fraction, and continuation. Same rule applies to all three detectors.

## 2. Two supported scenarios

**Scenario A: strong immediate breakout.** Large directional body closes outside range; next completed candle closes in the same direction; an associated valid three-candle FVG forms and is confirmed. The opportunity activates no earlier than the latest required confirmation.

**Scenario B: small initial breakout with delayed displacement.** The initial breakout body is relatively small; no immediately usable FVG; subsequent completed candles provide real same-direction continuation; a delayed valid FVG forms before range reclaim/invalidation. Mere existence of a later gap **does not** qualify.

Both long and short are symmetric in their requirements. Sweeps are optional, not a compulsory entry gate.

### Critical corrected Scenario B audit

Detector C originally produced 1,504 Scenario B-associated events; forensic recheck found **399 valid and 1,105 invalid/misclassified**. Invalid reasons included pre-FVG range reclaim, immediate-FVG mislabeling, and inadequate small-breakout/continuation evidence. C Scenario A was **131/131 valid** under frozen rules. Preserve invalid original events in audit history, *exclude* them from official eligible-order counts.

## 3. FVG geometry

For candles C1, C2, C3 in chronological order:

- Bullish gap: Low(C3) > High(C1). Lower gap edge = High(C1); upper = Low(C3).
- Bearish gap: High(C3) < Low(C1). Lower edge = High(C3); upper = Low(C1).
- Midpoint M = (gap lower edge + gap upper edge) / 2.
- An FVG is not confirmed until **C3 closes**.
- Do not place or simulate entry before *both* C3 close and scenario continuation confirmation.

The selected limit at M is fixed; never substitute a market breakout entry. If an order is already marketable when first eligible, track separately and apply the documented broker/order treatment.

## 4. Order validation and uniqueness

One detected range may generate several breakout evaluations, and a breakout may have multiple candidate FVGs. Multiple overlapping ranges can refer to the *same* actual FVG. Count raw ranges, representative structures, breakout IDs, unique FVG formations, candidate orders, executed orders and closed trades as **different units**.

Use stable IDs and de-dup across source detector memberships when execution parameters are exactly identical. Do not deduplicate genuinely different entries just because they occur within one consolidation.

## 5. Pending order entry semantics

Historical correct-side midpoint price reach:

- Buy limit: historical **ASK ≤ M**.
- Sell limit: historical **BID ≥ M**.

Entry research used 12 elapsed hours following lawful activation as the primary *diagnostic* window; longer 24/48/72-hour reaches were separately studied. Official pending-order expiry and cancellation were not final user-approved rules when these results were produced.

A quote crossing the order level proves a historical *price reach*, not an actual filled live order; queue priority, rejection, margin, partial executions, slippage, routing and active-order cancellation are separate.

## 6. Practical constraints and interpretation

Potential opposing known liquidity levels and structural stop distances matter. Neither a large number of raw signals nor a 60–70% midpoint-reach rate proves trading profitability. Never choose pattern thresholds to hit the desired monthly frequency.

See [detectors](02-range-detectors.md), [execution](03-fvg-execution.md), and [risk management](04-sl-tp-management.md).
