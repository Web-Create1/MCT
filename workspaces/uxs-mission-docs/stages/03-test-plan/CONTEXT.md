# 03 Test Plan

Writes the test plan: what the run must show, how it is measured, and when to stop.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Stage 01 | `../01-intake/output/<slug>-mission-request.md` | "Limits" and "Contingency thresholds" | The numbers criteria are built from |
| Stage 02 | `../02-conops/output/<slug>-conops.md` | Full file | Phases, roles and risks |
| Reference | `../../references/test-plan-outline.md` | Full file | Section list and step format |
| Reference | `../../references/risk-matrix.md` | Full file | Scoring and the go threshold |

## Process

1. Write one objective per thing the run must show, each tied to a CONOPS phase.
2. Give each objective a measure with a unit and the log field it is read from.
3. Write numbered procedure steps with an owner role and an expected result each.
4. Set pass criteria from the request's limits; derived numbers show their arithmetic.
5. Score every CONOPS risk with the matrix, add mitigations, write go and no-go criteria.
6. Run the Audit, then save.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 5 | Pass criteria and the scored risk register | Whether the thresholds and the go line are acceptable |

## Audit

| Check | Pass Condition |
|-------|---------------|
| Measurable | Every measure names a unit and a log field or a manual method |
| Traced | Every threshold comes from the request or shows its derivation |
| Owned | Every step and risk has a role code |
| Go line | No risk scored above the matrix's go threshold is left without a mitigation |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Test plan | `output/<slug>-test-plan.md` | Markdown in the outline's section order |
