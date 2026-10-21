# 05 Debrief

Reads the mission's ops log as text and writes a debrief of what happened against the plan.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Stage 03 | `../03-test-plan/output/<slug>-test-plan.md` | "Objectives", "Measures", "Pass criteria" | What to judge the run against |
| User | The ops log path given at the start of the run | Full file | Every fact the debrief states |
| Reference | `../../references/log-reading-guide.md` | Full file | Which kinds matter, time to detect, nulls, debrief sections |

## Process

1. Read the log's `provenance` line and copy its fields into the provenance line.
2. Build the timeline from `cmd`, `anomaly`, `refusal`, `contingency`, `discrepancy` and `end`.
3. For each anomaly compute time to detect as the guide says; show the two `seq` it uses.
4. Score each objective against its pass criterion from the log, citing `seq`.
5. Write findings, each with its `seq` references. Leave lessons learned as "not yet written".
6. Run the Audit, then save.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 4 | The objective scores with their `seq` evidence | Whether any score misreads the log before findings are written |

## Audit

| Check | Pass Condition |
|-------|---------------|
| Cited | Every number and finding cites at least one `seq` |
| Nulls | No null is reported as zero; no minimum or average is given over a null |
| Lessons | "Lessons learned (operator)" reads "not yet written" |
| Provenance | The provenance line matches the log's `seq` 0 and says Simulation |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Debrief | `output/<slug>-debrief.md` | Markdown in the guide's debrief order |
