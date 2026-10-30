# AMD T1 — Trader-Approved Native MQL5 Strategy Specification
**Specification snapshot:** 2026-10-30 · **Version:** `native-mql5-spec-v1-2026-10-30` · **Status:** specification only; NOT a validated or released EA binary.

> This document records the trader's decisions from the Oct 29–30, 2026 conversation. It supersedes contradictory assumptions in earlier Python/MQL5 experiments *for the new from-scratch MT5 EA*. It does NOT claim the old EA implemented these rules or that the strategy is profitable. Do not use older research backtest results as validation of this new specification.

## 1. Scope and development discipline
- Build **from scratch as a native MQL5 MetaTrader 5 Expert Advisor**. No Python/Nautilus strategy engine or copied Python-to-EA implementation.
- Develop one component at a time: trader chart examples → precise behavioral rule → narrowly scoped MQL5 module → compare decisions with trader markings → approve → integrate.
- No invented thresholds or discretionary criteria, no unapproved code modifications, no profit-based fitting, no live trading, no interaction with occupied MT5 GUI/terminal.
- Start with the approved examples; implement execution and backtest only after component and integration validation.
- Prior native FIX1/FIX2/R1/FIX3 and provisional Python M0 are historical context only, not the specification.

## 2. H1 Detector C — accumulation
1. Form a **candidate upper resistance zone** and **candidate lower support zone** from clusters of rejected H1 candle wicks. Several consecutive wicks at similar prices may establish *one zone*, not automatically separate independent bounce cycles.
2. Zones have **adaptive widths derived from the actual wick clusters**, not preset pip widths. A wick touching the defended line OR entering any part of its established zone counts as a **zone visit**; a near miss outside the zone does not.
3. A single unusually distant wick that protrudes beyond resistance/support and **closes back inside** is a **sweep** and does **not** expand the zone (example: four highs around 1.33500, isolated spike to 1.33700 with close back inside → retain 1.33500 resistance).
4. Candidate zones alone do **not** confirm accumulation. Price must chop sideways and complete **two full up-and-down boundary cycles**. Starting at resistance: `R → S → R → S → R`. Starting at support: `S → R → S → R → S`. `R → S → R` is **only one** cycle. Consecutive rejections at one boundary do not count as distinct cycles.
5. **Freeze both boundaries immediately when the second complete cycle finishes on a closed H1 candle.** Use only completed H1 information. After freeze, no automatic widening for wick sweeps. Breakout evaluation starts thereafter.
6. Prior shorthand “2+ independent reactions on each side” is **superseded as a mechanical touch-count test** by zone-cluster formation plus the two full cycles. A 2+1 non-chopping structure is not automatically tradable.
7. A small-bodied candle close outside the frozen range, or wick crossing alone, does not by itself confirm an actionable breakout.

**Not yet quantitatively specified:** how to group nearby wick values without a chosen pip/ATR tolerance; exact zone visit/reversal detection mechanics; how to reject trending zigzags; rules for invalidating/consuming and rediscovering a genuinely new accumulation. Do not claim these are already coded.

## 3. Breakout and associated H1 three-candle FVG
An actionable signal requires the proper breakout sequence, three-candle FVG geometry, gap entirely on the trade's side of the **frozen** range, and nonzero C1/C3 real candle bodies. Use closed H1 candles, with zero lookahead.

**Scenario A — direct strong breakout**
- C1 is the pre-breakout candle within the range.
- C2 is the first directional displacement/breakout candle **closing outside** the frozen range.
- C3 subsequently closes and confirms the three-candle directional FVG with C1 and C2.
- The trader explicitly **approved** C1-inside → C2-breakout → C3-FVG indexing. Earlier local Stage 0 docs saying this indexing is open should be reconciled to this more recent approved instruction.

**Scenario B — small boundary close then immediate displacement**
- C1 is a small-bodied candle closing outside the frozen boundary; *not* itself a qualifying breakout.
- The **immediately following** C2 must provide directional breakout/displacement; the **immediately following** C3 must complete the associated directional three-candle FVG.
- No intervening extra candle, unlimited waiting, or later alternate FVG recovery.
- On failed C2, failed C3, wrong direction or wrong gap side, **abandon that setup and wait for a genuinely new accumulation**, without reusing the failed range.

**Exact FVG geometry and location**
- Bullish: `Low(C3) > High(C1)` and **`High(C1) >= frozen resistance`** (the entire bullish FVG is at/above resistance).
- Bearish: `High(C3) < Low(C1)` and **`Low(C1) <= frozen support`** (the entire bearish FVG is at/below support).
- A gap straddling the frozen range or on the wrong side fails.
- **C1:** `abs(Close-Open) > 0`; exactly bodyless/doji fails. **C3:** same rule. A tiny but nonzero body is valid. Earlier “meaningful body”/“tiny-bodied” filters were explicitly withdrawn.
- **C2:** directional breakout candle in the approved sequence; no independent numeric ATR multiplier, relative-body-size, average-body, or body-to-wick strength cutoff. Earlier numerical displacement filters are superseded. Keep the required directional breakout close and valid FVG; do not reintroduce an arbitrary strength threshold.

**On failure of required breakout/FVG checks:** reject the sequence, search for an entirely new accumulation.

## 4. Entry and structural stop
- After the 3-candle signal is confirmed **at C3 close**, propose a **BUY LIMIT** (bullish) or **SELL LIMIT** (bearish) at the **exact 50% FVG midpoint**. Never chase the breakout with a market order. A non-immediate fill is expected/allowed.
- Pending limit is submitted only after valid structural SL, valid H4 TP and strict R:R gate below; baseline expiry **12 hours after activation**.
- For bearish displacement, identify the **relevant protective high wick from the final few H1 candles forming local structure before displacement**, and place SL safely above it. For bullish, mirror with relevant protective low below local structure.
- Do **not** automatically place SL beyond the whole accumulation range, nor select a tighter anchor merely to engineer a favorable R:R.
- Exact length/identity of the local structure and exact safety buffer remain to be calibrated against trader-marked charts. Historical SL2 formula `max(0.15*completed H1 ATR14, 2*activation spread)` is prior research, **not automatically approved** for this new build.

## 5. H4-only liquidity TP — trader's priority
- **H4 only in V1; D1 excluded**.
- Primary H4 liquidity **zone** = **2 or more H4 candle wicks repeatedly rejecting in approximately the same price area**. Identify the actual clustering/rejection *independently of reward-to-risk*; zone width comes from wick cluster; not fixed pip width.
- Choose an actual historical **representative repeated-rejection wick** from that cluster, **not automatically the highest/lowest wick** or the nearest H4 pivot. In an illustrative resistance cluster of 1.33860, 1.33885, 1.33910, the trader preferred **1.33860** where the repeated rejection was concentrated.
- **Exception explicitly approved from chart #002:** a single particularly **prominent isolated H4 swing wick** can also be a valid liquidity destination. Its significance must be justified, not accepted merely because it is a nearby pivot.
- Longs seek H4 resistance/rejection highs above entry; shorts H4 support/rejection lows below entry. TP is at the **exact selected wick price**, without an extra TP pip buffer.
- A near zone still gets identified and recorded even if its distance is small.
- Evaluate legitimate H4 liquidity destinations **nearest first in trade direction**. For each compute planned R:R from FVG midpoint and independently chosen structural SL:
  - Buy: `RR=(TP-Entry)/(Entry-SL)`
  - Sell: `RR=(Entry-TP)/(SL-Entry)`
- **Require strictly `RR > 1.8` (not equal).** If the closest candidate fails, skip *that TP candidate* and check the next valid H4 zone farther away. If none qualifies, **reject the entire setup and place no order**. Keep intervening skipped zones recorded as possible obstacles.
- Do not move entry or stop to manufacture qualifying R:R.

**Still requires deterministic chart calibration:** numeric/algorithmic wick grouping and representative wick selection; how to qualify a prominent isolated swing wick; how to rank zones with overlapping evidence and verify historical causality.

## 6. Execution / risk baseline
- Risk **0.5% of current equity** per trade.
- One position at a time.
- Pending expiry **12 hours from confirmed activation**; maximum trade hold **72 hours from actual fill**.
- No breakeven, trailing stop, partial take profit or market-entry substitution.
- Exact concurrent candidate scheduling, restart persistence and same-timestamp priority should be documented and verified in native MT5. Do not invent unresolved ordering behavior.
- Final execution testing: MT5 native MQL5 and real BID/ASK ticks; avoid occupied terminals, GUI automation and live execution.

## 7. Approved visual references and exclusions
- **Example #001 — GBPUSD H1 bullish:** trader-marked accumulation resistance ~1.33388 / support ~1.32983; local nearby H4 pivot/red ~1.33580 was *not* the preferred liquidity TP; meaningful repeated H4 rejection/green ~1.33885 was. Potential live breakout must await confirmation. No bullish SL approved from this example.
- **Example #002 — GBPUSD H1 bearish:** range high ~1.35620, low ~1.35308; planned midpoint sell ~1.35346; trader local pre-displacement structural SL ~1.35543 rather than above entire range; prominent isolated H4 swing-wick TP ~1.34840; marked planned ~2.57R. A delayed midpoint-limit fill is permitted. This is a trader decision example, not independently verified profitable execution.
- **Example #003 — excluded:** later bullish SL ~1.33162 / ~1.63R screenshot was explicitly **withdrawn by trader** as too complicated. Do not train rules or tests on it as an approved setup.
- **Eight web-market Detector C example types** were approved as *visual calibration types only*, not publisher-drawn exact boundary prices or hidden numeric thresholds; see local `detector_c_web_market_examples/TRADER_REFERENCE_APPROVAL.md` (local artifact not automatically uploaded here).

## 8. Governance, testing and release interpretation
- Stage 0 source of truth in trader's local workspace: `AMD-T1-Codex/research/amd_t1_native_mql5_stage0/`. This GitHub document is the conversation-derived approved rule snapshot; local files were not directly read for this commit.
- Maintain approved vs open distinction, exact example provenance and rejected interpretations.
- After component-by-component approval: verify actual chart decisions, then separate out-of-sample testing. Historical M0 win rate and MT5 R1/FIX outcomes **do not validate this new EA**.
- **No EA implementation, compilation, Strategy Tester execution, or new performance claim is part of this snapshot.**

## 9. Implementation readiness summary
Approved conceptually: two-cycle accumulation / causal freeze, FVG geometry & side, no-bodyless C1/C3, immediate Scenario A/B indexing, midpoint entry, local stop philosophy, H4 repeated-wick or prominent-swing TP, strict RR gate, baseline risk and lifecycle.

Open for objective conversion to MQL5: cluster grouping, sideways-vs-trend discrimination, exact valid reversal/visit algorithm, local stop anchoring/buffer, isolated H4 swing significance, reliable candidate priority and restart behavior.

**Release intent:** preserve the trader-approved rules accurately and reproducibly. This is a **strategy-specification milestone only**, not a production-ready EA release.
