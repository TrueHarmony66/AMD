# AMD T1 — Native MQL5 Trader Strategy V1 (30 October 2026)

**Milestone type:** trader-approved strategy specification. **Not an executable EA or performance release.**

Full specification: [docs/26-native-mql5-trader-approved-strategy-2026-10-30.md](26-native-mql5-trader-approved-strategy-2026-10-30.md).

## What's captured

- New from-scratch native MQL5/MT5 development; no Python strategy runtime.
- H1 Detector C: adaptive wick clusters for upper/lower zones; valid zone entry versus near misses; isolated outside wicks closing back in treated as sweeps; **two full boundary round-trips** (`R-S-R-S-R` or reverse) before freeze.
- Immediate causal freeze when the second round trip completes on a finished H1 bar.
- Scenario A: range-interior C1, direct breakout C2, gap-forming C3.
- Scenario B: small close outside C1, immediate directional C2, immediate FVG C3; failure means new accumulation.
- C1/C3 must have nonzero bodies; C2 has no additional numeric body-size threshold.
- Strict FVG geometry and entire gap outside frozen range; midpoint pending limit.
- Structural stop beyond the relevant local *pre-displacement* wick structure, not automatically beyond the entire range.
- H4-only TP: 2+ rejected wick cluster, or trader-approved prominent isolated H4 swing wick exception. Use representative actual wick rather than nearest minor pivot.
- Identify actual zones first; then select first valid farther H4 target with **RR > 1.8**; if no such target, skip setup.
- 0.5%-equity risk, 12h pending order TTL, 72h max position holding; no BE/trailing/partials.
- Examples #001 and #002 retained; #003 explicitly excluded.

## Explicit non-claims and work remaining

This is a **documentation-only milestone**. No native EA constructed or audited against these new rules; no tick test or performance result is implied. Open calibrations include adaptive-cluster grouping, sideways reversal detection, localized stop selection/buffer, significant isolated H4 wick qualification, and deterministic scheduler/restart handling.

The earlier modeled M0 and native FIX/R1 results are **not** evidence of parity for this new specification.

See the [full decision record](26-native-mql5-trader-approved-strategy-2026-10-30.md) before implementing any component.
