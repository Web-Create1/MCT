# 04 Mission Docs Workspace

Build `workspaces/uxs-mission-docs/` in `Web-Create1/MCT`: an ICM pipeline that turns a mission
request into a CONOPS, a test plan, a mission brief with a preflight card, a debrief from the
ops log, and a quick-reference card, plus one complete worked example.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| MCT | `_core/CONVENTIONS.md` | Patterns 1 to 8, "Naming Conventions" | The rules the new workspace must pass |
| MCT | `_core/templates/` | All four templates | Starting points, not invention |
| This stage | `references/mission-docs-prd.md` | Full file | Requirements, stage list, acceptance criteria, PR plan |
| This workspace | `../../references/integration.md` | C1, C2, C5, C6 | Log format the debrief stage reads, crew roles, units, provenance |
| This workspace | `../../references/design-language.md` | Section 5 | The shared document skeleton |
| This workspace | `../../references/honesty-rules.md` | "Never" and "Wording Bank" | The example run is simulated and must say so |

## Process

1. Read the Inputs. Do not open other workspaces except `workspace-builder/stages/05-validation/CONTEXT.md` for its checklist.
2. Scaffold the folder tree from the PRD, every stage CONTEXT.md in the three-section shape.
3. Write the reference files each stage names (document outlines, wording rules, log reading guide).
4. Write the worked example: a one-page mission request for a simulated USV harbour survey,
   then run every stage by hand and commit each output to `examples/harbour-survey-sim/`.
5. Validate against the workspace-builder checklist and fix what fails.
6. Add the workspace to the root `CLAUDE.md` folder map and routing table, and to `README.md`.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 2 | The stage list and folder tree | Whether a stage is missing or redundant |

## Audit

| Check | Pass Condition |
|-------|---------------|
| Contracts | Every stage CONTEXT.md has Inputs, Process, Outputs and is under 80 lines |
| Routing not content | No CONTEXT.md holds rules or outlines; those live in `references/` |
| One-way references | No reference file points back at a stage |
| Example is honest | Every example document carries the C6 provenance line and says Simulation |
| No em dashes | `LC_ALL=C.UTF-8 grep -rnP '\x{2014}' workspaces/uxs-mission-docs` returns nothing |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Workspace | `workspaces/uxs-mission-docs/` | ICM workspace |
| Example run | `workspaces/uxs-mission-docs/examples/harbour-survey-sim/` | Six markdown documents and the input log |
| Stage report | `output/mission-docs-workspace-report.md` | Written by the orchestrator |
