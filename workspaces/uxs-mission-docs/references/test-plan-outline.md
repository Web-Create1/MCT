# Test Plan Outline

A test plan turns a concept into something measurable: objectives, measures, criteria. This
outline is generic and public.

## Sections

Title line, provenance line, BLUF: what the run must show and the go line. Then:

1. **Objectives.** Numbered `O1`, `O2`. Each is one sentence and names the CONOPS phase it tests.
2. **Measures.** A table: objective, measure, unit, source. Source is a log field (`tlm.xtrack_m`,
   `anomaly.t_s`) or a manual method (lookout report, logger note).
3. **Procedure.** Numbered steps `P-1`, `P-2`, each with owner role, action, expected result.
   The data logger records any step whose result differs as a discrepancy against its number.
4. **Pass criteria.** A table: objective, criterion, threshold with unit, source of threshold.
5. **Risk register.** A table scored with `risk-matrix.md`: risk, likelihood, severity, score,
   mitigation, owner, residual score.
6. **Go and no-go.** The conditions checked before arming and the conditions that end the run.
7. **Data to keep.** The ops log, notes, and anything a debrief will need.

## Rules

- Derived numbers show their arithmetic once: `7 lanes = 120 m / 20 m + 1`.
- A criterion that cannot be read from the log or a named manual method is rewritten or cut.
- "Not measured" is a valid result and fails any criterion that needed the measurement.
