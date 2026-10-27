# Three frozen range detectors — design, differences, and tests

## Detector A — original canonical range detector

Uses existing historical high/low windows, ATR-normalized width, duration/maturity, structural quality, touch/quality and independent/nested-range deduplication. Historical baseline:

- H1 **365 independent ranges** (299 top-level + 66 nested).
- H4 **162 independent ranges** (128 top-level + 34 nested).
- Phase 1.5 reports H1 median observed duration 15 H1 candles, median confirmed lifetime 5 bars; H4 6 and 3 respectively.
- Phase 1.5 established/mature H1 188; H4 84; multi-touch H1 156; H4 81.

The detector's boundaries were not fully demonstrated to match the user's hand-drawn defended reaction lines. **Do not retrofit A**: it remains a frozen control.

## Detector B — extreme-wick/chop method

Constructs causal range candidates using actual historic extreme high/low wick anchors combined with sideways/choppiness measures; confirmed boundaries freeze. This can over-broaden a range when isolated wick outliers occur.

- Raw H1 candidates: **2,322**.
- Phase 4B overlap groups: **600** with **2,138** candidates in multi-candidate groups; grouping and representative counts are separate units.
- Phase 4C: **600 causal representatives**, **1,458 raw FVG records** → **382 representative-linked opportunities**.
- Corrected common-rule eligible midpoint-order population: **361**.

Phase 4B had **11 match records** against A, **355 A-only** and **2,311 B-only** under that particular match method. These are match *records*, not guaranteed unique common ranges; note apparent 365/355/11 mismatch (matching may be non-1:1). Later A/C matching used a different method—never equate the two match percentages.

### Known issue

Substantial duplicate/nested detection and short minimum-maturity cases. Large raw signal count is not proof of better structural recognition.

## Detector C — user-defined defended reaction levels (primary focus)

Instead of blindly choosing absolute wick extremes:

1. Maintain recent confirmed swing/reaction candidates.
2. Detect repeated cluster interactions near support and resistance.
3. Require credible sideways chop rather than a trend pause.
4. Choose causally anchored, defended horizontal levels; these may be actual swing wicks without equaling the widest historical outlier.
5. Permit developing candidate levels to update before confirmation.
6. Once confirmed, **freeze both range lines** and their knowledge time.
7. Record isolated wick overshoots closing back inside as sweeps **without moving confirmed boundaries**.
8. A close outside frozen range is breakout candidate; downstream shared Scenario A/B logic determines eligible trades.

Phase 4D: **1,705 H1 range records, 819 H4, 2,980 diagnostic H1 close-breakout events**. A/C proximity-and-boundary comparison: **517 pairs involving 273 unique A ranges**, meaning several match records can involve one A range.

Phase 4E.1 attached missing breakout-timestamp-to-H1-candle-index bridge, emitting C **1,635 provisional FVG events**, including A=131 and B=1,504. Phase 4E.2 corrected the latter to 399 valid. Phase 4E.3 deduplicated/corrected to **499 eligible midpoint orders**. Do **not** treat 1,635 as valid trade count.

## Comparison philosophy

- Same GBPUSD H1 candles; same timeframe, date coverage, breakout quality, FVG formation and quote-side execution.
- Each detector's range construction is the only intended signal-source difference.
- Compare raw range count, independent structures, breakout funnel, scenario and quality classification, exact 50% limit price reach, matched versus exclusive events, and ultimately realized net R after identical risk rules.
- A/B/C should remain accessible even when C is chosen as current primary research hypothesis.
- Current visual chart galleries contain unreviewed examples. **Human visual accuracy winner is unknown**.

## Why these approaches are meaningfully different

~~~mermaid
flowchart LR
 A[Detector A: canonical window + ATR + quality] --> X[Confirmed frozen range]
 B[Detector B: outer historical wick extremes + chop] --> X
 C[Detector C: repeated defended reactions + tolerated sweep wick] --> X
 X --> Y[Identical breakout / FVG / midpoint rules]
~~~

For an explicit sweep drawing see [diagram examples](11-diagrams-and-examples.md).
