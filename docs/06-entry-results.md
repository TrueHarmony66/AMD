# Entry validation results — cumulative correction ledger

## Primary corrected 1,099 detector-associated order population

| Detector | Eligible order records | Midpoint reached in 12h | Non-reaches | % |
|---|---:|---:|---:|---:|
| A | 239 | 158 | 81 | 66.1 |
| B | 361 | 224 | 137 | 62.0 |
| C | 499 | 335 | 164 | 67.1 |
| **All records** | **1,099** | **717** | **382** | **65.2** |

Source: user-reported full historical replay, with unique candidate IDs and no remaining unprocessed entries. No local Parquet ledger uploaded; order-by-order independent audit unavailable in published documentation.

### Detailed full scan facts

- Source archives read in time order (February 2021 to December 2025 as reported).
- 133,166,553 tick records.
- 58 already verified entries retained across resume and 1,041 newly processed.
- Coverage reported as 100%, missing tick source coverage reported as 0, candidate-ID uniqueness and prior classification regressions passed.
- Historical right-side quote test: buy ASK ≤ midpoint, sell BID ≥ midpoint.
- The 717 is the sum of A/B/C classifications; not necessarily 717 unique market setups, because independent detectors can discover the same pattern.

## Reconciliation to trade management

The full SL/TP study subsequently reported:

| Cohort fact | Count |
|---|---:|
| Full scan midpoint-reach records | 717 |
| Timestamp-backed reach records before attempted recovery | 680 |
| Extra timestamps recovered via tick rescan | 24 |
| Remaining unresolved legacy records | 13 |
| Usable paired SL entries | 655 |
| Stop study genuine-sweep anchors | 255 |
| Stop study confirmed structural fallbacks | 400 |
| No valid anchor | 25 |

Arithmetic: 680 + 24 + 13 = 717. 680 + 24 = 704; 655 were modeled as valid paired entries, thus **49 timestamp-backed records are not in the final paired cohort**. The stop study's earlier 696 ledger-reach reporting used a non-final intermediate status overlay, and its 680/16/25 decomposition must not be merged blindly into final 717 denominator. An **ID-level exclusion table** is required to explain all 49 differences between 704 and 655.

## Entry frequency vs trade frequency

The order population is 1,099 detector-associated *eligible midpoint orders* over the represented historical coverage; it is not 1,099 actual trades. Per-month range detections and raw FVG opportunities were higher. Entry reach rates are conditional; TP-valid modeled trade counts are lower than 717 and vary by combination.

Consult [monthly modeled trade frequency](../data/summary/monthly-h4-sl2-trade-counts.csv) for a specific H4/SL2 outcome cohort, and [limitations](09-limitations.md) before treating this as a live fill-rate forecast.
