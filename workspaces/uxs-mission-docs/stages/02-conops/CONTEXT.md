# 02 CONOPS

Writes the concept of operations: what the mission is for and how the crew will run it.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Stage 01 | `../01-intake/output/<slug>-mission-request.md` | Full file | Every fact and number |
| Reference | `../../references/conops-outline.md` | Full file | Section list and what each holds |
| Reference | `../../references/crew-and-units.md` | "Roles" | Duties per role code |

## Process

1. Read the request. List its open questions; do not answer them yourself.
2. Draft each section of the outline in order, using only facts from the request.
3. Split the mission into phases with an entry and exit condition each.
4. Assign every duty in every phase to a role code.
5. Run the Audit, then save.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 3 | The phase list with entry and exit conditions | Whether the concept is right before roles and risks are filled in |

## Audit

| Check | Pass Condition |
|-------|---------------|
| Traced | Every number in the CONOPS appears in the request |
| Complete | Every outline section is present; empty ones say why |
| Roles | Every phase names who acts and who consents |
| Honest | The provenance line says Simulation; no "operated", "flew" or "deployed" |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| CONOPS | `output/<slug>-conops.md` | Markdown in the outline's section order |
