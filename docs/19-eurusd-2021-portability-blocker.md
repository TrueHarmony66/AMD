# EURUSD 2021 frozen holdout — unrun: original signal generator unavailable

## Outcome

**No EURUSD P&L, win rate or even a generated executable order ledger exists.** Holdout remains unused for strategy-performance selection. Do not infer cross-pair edge.

- Original out-of-sample manifest specified **EURUSD 2025**.
- The researcher later explicitly selected **EURUSD 2021** before EURUSD performance was inspected, as the new designated holdout. Keep dated freeze-year decision.
- **12/12** EURUSD 2021 HistData ZIPs present, integrity/provenance validated, four-column ASCII (`datetime,bid,ask,flags`).
- No EURUSD 2021 performance ticks scanned; only archive checks were performed.
- Frozen Phase 8.3 GBPUSD execution engine hashed and unchanged.

## Critical portability defect

The preserved `research/manual_range_detector_comparison/scripts/phase4d_detector_c.py` is a **GBPUSD-specific descriptive range script**. It is **not** the full independently executable source event generator.

The original Phase 8.3 event universe is **308 frozen GBPUSD records**, which cannot legally or logically be replayed as EURUSD orders. No instrument-independent source generator exists with verified event-level parity to all of those 308 events, including:

- Scenario A/B follow-through classification and genuine delayed FVG validation;
- three-candle FVG bounds and exact midpoint;
- activation/eligibility timestamps;
- SL2 causal structural anchor and ATR/spread buffer;
- prior confirmed H4 wick target and confirmation timestamp;
- stable event IDs and rejection records.

## Acceptance gate before this holdout can run

1. Discover/recover the actual original GBPUSD event-generation pipeline and configuration. Do not assume Phase 4D's descriptive output is sufficient.
2. Instrument-independent refactor of **exact frozen rules**, with no EURUSD outcome-based parameter adjustments.
3. Regenerate GBPUSD eligible events from original ticks, then compare **field-by-field event identity and causal timestamps** against the 308 preserved event records. Parity must not be declared from count alone.
4. Freeze validated engine code/config/instrument metadata, publish its hashes and version.
5. Then generate EURUSD 2021 Detector C + Scenario A/B + FVG + SL2 + exact H4 eligible events, using genuine source data and causal H1/H4/D1 warmup.
6. Finally execute frozen **M0 only** on EURUSD 2021 with the existing Phase 8.3 quote replay and modeled costs; report positive or negative results unaltered.

**If exact historical generator is unrecoverable:** label new reconstructed implementation as a new version; validate without retrofitting rules to the GBPUSD outcomes and do not call it the exact old holdout algorithm.

## Evidence files present only on local Windows machine

- `research/amd_t1_final_execution_validation/03_eurusd_holdout/EURUSD_FROZEN_YEAR_DECISION.md`
- `EURUSD_SIGNAL_GENERATOR_PARITY.md`
- `EURUSD_2021_M0_EXECUTION_BLOCKER.md`
- `EURUSD_2021_ARCHIVE_INVENTORY.csv`

No original EURUSD ZIPs, standalone frozen generator, old 308-event ledger, or local reports are uploaded as source artifacts in the GitHub release documentation.
