# Log Reading Guide

How to read an ops log (`uxs-ops-log/1`) as text and turn it into a debrief. The canonical
format is `workspaces/uxs-ops-program/references/integration.md`, contract C1; this guide is
for a reader and wins nothing if the two differ.

## The Shape of a Line

One JSON object per line. Every line has `v`, `seq`, `t_utc`, `t_s`, `mission`, `kind`,
`actor` (`operator` id and `role` code), `body`, and `prev`.

- `seq` counts from 0 with no gaps. Cite it for every fact: `seq 14`.
- `t_s` is seconds since the first line from a monotonic clock. Order events by `t_s`, not by
  `t_utc`, which can jump.
- `prev` is the SHA-256 of the line before. A matching chain is tamper-evident, not
  tamper-proof: anyone can rewrite the whole chain. The debrief stage does not check it; say
  whether `verify-log` was run, and by whom, or that it was not.

## Which Kinds Matter for a Debrief

| Kind | Use it for |
|------|------------|
| `provenance` | Always `seq` 0. Driver, seed, profile, envelope: the debrief's provenance line |
| `plan` | The plan's name and its contingency thresholds, to compare against the test plan |
| `preflight` | Which checks passed, failed, or were not measured, and by which method |
| `cmd` | Every command and its result. `refused` and `failed` are always in the timeline |
| `tlm` | Telemetry samples. Read for measures and for fault onset; do not list every line |
| `anomaly` | What the monitor flagged, with severity, value, threshold and unit |
| `refusal` | A command the envelope blocked, with the rule. Always a finding |
| `contingency` | A failsafe or planned response: trigger, action, and who acted |
| `note` | Crew remarks. Quote short ones; never turn them into facts |
| `discrepancy` | Expected against observed at a procedure step. Always a finding |
| `end` | Outcome, duration, and line count. Check `lines` equals the last `seq` + 1 |

## Time to Detect

Time to detect (TTD) = `anomaly.t_s` minus the fault's onset.

1. If a scenario file states the fault's injection time, that is the onset.
2. Otherwise the onset is the `t_s` of the first `tlm` line whose value is out of the
   anomaly's limit (for example `xtrack_m` above the threshold, or `link_ok` false).
3. Show both `seq` numbers and the subtraction: `TTD = 245.0 s - 240.0 s = 5.0 s (seq 12, 13)`.
4. If no out-of-limit `tlm` line exists before the anomaly, TTD is `not measurable`, with the
   reason. Telemetry sampled sparsely makes TTD an upper bound on the true onset; say so.

## Nulls

`null` means not measured. It is never zero and never skipped silently.

- Write "battery percentage was not measured at t_s 720.0 (seq 22)".
- If any value of a field is null within the window a statistic covers, do not report a
  minimum, maximum or average for that field. Report the measured values with their `seq`
  and say why no statistic is given.
- A preflight `result` of `not-measured` is reported as such, with who accepted it.

## Debrief Sections

Title line, provenance line (from `seq` 0), BLUF: outcome, duration, and the one finding that
matters most. Then:

1. **Log.** File name, mission id, line count, whether `verify-log` was run.
2. **Timeline.** A table: `t_s`, `seq`, kind, what happened. Events only, not every `tlm`.
3. **Anomalies.** A table: rule, severity, value and threshold with unit, onset `seq`, anomaly
   `seq`, TTD.
4. **Refusals.** Command, rule, reason, `seq`.
5. **Contingencies.** Trigger, action, by whom, `seq`, and how the run continued.
6. **Discrepancies.** Step, expected, observed, `seq`.
7. **Metrics.** Each test plan measure with its value and `seq`, or "not measured".
8. **Objectives.** Each objective: met, not met, or not measurable, with the `seq` evidence.
9. **Findings.** Numbered `F1`, `F2`. Each states what the log shows, with `seq`. Findings
   describe; they do not recommend.
10. **Lessons learned (operator).** Reads exactly "not yet written" until a person writes it.
