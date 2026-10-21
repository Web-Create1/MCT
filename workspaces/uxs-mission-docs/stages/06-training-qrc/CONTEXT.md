# 06 Training QRC

Writes one quick-reference card (QRC) per contingency the mission planned for or met.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Stage 04 | `../04-brief-and-preflight/output/<slug>-brief.md` | "Contingencies" and "Comms" | Planned triggers, actions, who to tell |
| Stage 04 | `../04-brief-and-preflight/output/<slug>-preflight-card.md` | Full file | Checks a card may point back to |
| Stage 05 | `../05-debrief/output/<slug>-debrief.md` | "Timeline" and "Findings" | What actually happened, with `seq` |
| Reference | `../../references/qrc-outline.md` | Full file | Card format and length |

## Process

1. List the contingencies: every one in the brief, plus any the debrief shows that were not planned.
2. For each, write the trigger as the crew would see it, with its threshold and unit.
3. Write the first three actions in order, each with a role code.
4. Add who to tell, what to log, and, when the debrief met it, one line of what happened.
5. Run the Audit, then save one file per card.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 1 | The contingency list | Whether a card is missing or redundant |

## Audit

| Check | Pass Condition |
|-------|---------------|
| One page | Each card fits one printed page |
| Consistent | Thresholds and actions match the brief exactly |
| Honest | "What happened" lines cite `seq` and say simulated |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Cards | `output/<slug>-qrc-<trigger>.md` | One card per file, trigger in lowercase-with-hyphens |
