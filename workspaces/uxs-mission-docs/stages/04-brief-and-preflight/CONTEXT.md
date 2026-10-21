# 04 Brief and Preflight

Writes the crew brief and a one-page preflight card from the CONOPS and the test plan.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Stage 02 | `../02-conops/output/<slug>-conops.md` | Full file | Situation, concept, roles, comms |
| Stage 03 | `../03-test-plan/output/<slug>-test-plan.md` | "Procedure", "Go and no-go", "Risk register" | What the crew will do and when to stop |
| Reference | `../../references/brief-outline.md` | Full file | Brief sections and the preflight card format |

## Process

1. Write the brief in the outline's order; keep it readable aloud in ten minutes.
2. Copy contingency thresholds from the test plan, not from memory.
3. Write the preflight card: one line per check, owner role, method, and pass value.
4. Mark which checks the system logs automatically and which a person confirms.
5. Run the Audit, then save both files.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 3 | The preflight card | Whether a check is missing before the brief is final |

## Audit

| Check | Pass Condition |
|-------|---------------|
| Consistent | Every threshold in the brief matches the test plan exactly |
| One page | The preflight card fits one printed page |
| Owned | Every check names a role code; arming consent is the PIC's alone |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Brief | `output/<slug>-brief.md` | Markdown in the outline's order |
| Preflight card | `output/<slug>-preflight-card.md` | One-page checklist table |
