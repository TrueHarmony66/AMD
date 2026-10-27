# Diagrams, trade geometry and discretionary examples

These are **schematic illustrations** of the research rules, not screenshots of historical returns or a substitute for actual price-series annotations.

## Whole setup

```text
     prior confirmed 4H/1D swing high wick  <---- LONG TP
                ↑
                │  expected advance
  ══════════════╪══════════════  previously defended upper range
  ┌─────────────┐│
  │accumulation ││       confirmed breakout candle CLOSES above box
  │ sideways    ││          ▮
  │ defended    │└──────────▮▮▮▮      confirmed 3-candle bullish FVG
  │ levels      │             ┌──────────┐
  └─────────────┘             │50% BUY LIMIT  <---- entry on ASK reach
  ═════════════════════════   └──────────┘
        isolated sweep wick                 [distal FVG lower edge]
          ↓                                  [SL1 halfway between
       prior low / swing                       FVG edge & known sweep low]
          ↓                                  [SL2 beneath sweep low+buffer]
```

This layout is **not to scale**. A preexisting swing-high wick TP must be in profit direction and confirmed before order activation.

## Comparing raw wick extreme vs defended level (A/B vs C philosophy)

```text
                      isolated upper wick / sweep
                                 │
  B upper line  ─────────────────┼────────────────  B may use outer wick
                       │         │
  C upper line  ═══════┼═════════╪═══════          repeated defended level
          ╭────╮     ╭─┴──╮   ╭──┴─╮
          │    │     │    │   │    │      closes held under C resistance
   chop   │    ╰─────╯    ╰───╯    ╰────
          ╰─────────────────────────────╮
  C lower line  ════════════════════════╪══════     repeated defended support
                       │
  B lower line  ───────┼───────────────────────     B may use lower outer wick
                       ↓ isolated lower wick
```

For a C-defined upper sweep, a candle wick may pierce C's upper line while its **completed close returns within** the box: line stays frozen, no confirmed breakout from that wick alone. A true directional breakout is close beyond frozen range with continuation and valid FVG.

## Scenario A and Scenario B

~~~mermaid
flowchart TD
  R[Confirmed frozen sideways range] --> X{Completed close outside range?}
  X -->|No; wick only| S[Sweep record; keep bounds frozen]
  X -->|Yes| Q{Strong immediate displacement and follow-through?}
  Q -->|Yes| A[Scenario A: immediate qualifying 3-candle FVG]
  Q -->|Smaller first close| B[Scenario B: delayed true continuation]
  B --> P{Genuine later FVG before reclaim?}
  P -->|No| V[Reject invalid delayed gap]
  P -->|Yes| F[Confirmed delayed 3-candle FVG]
  A --> M[50% FVG pending LIMIT]
  F --> M
  M --> T[First correct-side quote reach within activation window]
~~~

## FVG gap geometry

For bullish C1/C2/C3, if Low(C3) > High(C1), the region from High(C1) to Low(C3) is the bullish FVG. Its midpoint is the arithmetic average of those two edges. For bearish, if High(C3) < Low(C1), the FVG is from High(C3) to Low(C1). Candle two usually reflects impulsive displacement but specific body/ATR conditions are frozen per original engine, not reconstructed here.

## Paired stop geometry, LONG case

```text
                        known H4 wick TP  ─────┐
                                                │
                          FVG midpoint  ────────┼─ BUY entry
                         FVG lower edge ────────┤
                                                │
               SL1 = halfway lower edge / S ───┼─ user stop
                                                │
                S = known sweep/swing LOW  ─────┤
                     SL2 = S - ATR buffer  ─────┘─ wider stop
```

SHORT is mirror image; SL1 above FVG upper edge, SL2 beyond known high.

## Actual chart artifacts

The trader supplied screenshots explaining reaction levels, sweeps and an intermediate stop location. Those screenshot files were available in conversation history but **have not been embedded as versioned GitHub image assets in this release**. To retain them, copy approved visual material into `docs/assets/`, redact sensitive overlays if necessary, and reference exact image filenames and annotated times. Never reinterpret an explanatory AUDUSD image as historical GBPUSD backtest evidence.

## 18 outcome experiments

~~~mermaid
flowchart LR
  D[Detector A / B / C] --> S1[SL1 intermediate]
  D --> S2[SL2 beyond extreme]
  S1 --> H[H4 exact wick]
  S1 --> J[D1 exact wick]
  S1 --> K[Nearest H4/D1 exact wick]
  S2 --> H2[H4 exact wick]
  S2 --> J2[D1 exact wick]
  S2 --> K2[Nearest H4/D1 exact wick]
~~~

Each combination is replayed after the same frozen FVG midpoint price reach, with independent chronologically ordered BID/ASK exits.
