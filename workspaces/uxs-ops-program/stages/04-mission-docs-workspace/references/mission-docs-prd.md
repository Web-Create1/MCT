# PRD: `uxs-mission-docs` Workspace

## Problem

Operations work is mostly documents: a CONOPS before a program, a test plan before a test
event, a brief before a mission, a debrief after it, and a card a new crew member can use
cold. Writing them from scratch every time is slow and inconsistent, and an AI asked to write
one without structure invents numbers. This workspace makes each document a stage with a
contract, so the agent loads only what that document needs and every number traces to a plan
or a log.

## Goals

1. A mission request becomes a full document set in six stages, each a human edit surface.
2. Every number in every document traces to the mission request, the plan, or a C1 log line.
3. Each stage's CONTEXT.md is under 80 lines and loads 4 files or fewer.
4. One complete worked example, simulated, that a reviewer can read in ten minutes.

## Non-Goals

- Real operational documents for any real program or customer.
- Any classified, controlled, or employer-specific format. The outlines are generic and public.
- Code. The debrief stage reads a log as text; it does not run anything.

## Stages

| # | Stage | Reads | Writes |
|---|-------|-------|--------|
| 01 | `01-intake` | The user's request, conversationally | `output/<slug>-mission-request.md`: objective, platform, area, window, crew, constraints |
| 02 | `02-conops` | 01 output, `references/conops-outline.md` | `output/<slug>-conops.md`: purpose, concept, phases, roles (C2), comms plan, environment, risks |
| 03 | `03-test-plan` | 01 and 02 outputs, `references/test-plan-outline.md`, `references/risk-matrix.md` | `output/<slug>-test-plan.md`: objectives, measures with units, procedure steps, pass criteria, risk register, go and no-go criteria |
| 04 | `04-brief-and-preflight` | 02 and 03 outputs, `references/brief-outline.md` | `output/<slug>-brief.md` and `output/<slug>-preflight-card.md` |
| 05 | `05-debrief` | 03 output, a C1 log, `references/log-reading-guide.md` | `output/<slug>-debrief.md`: timeline, anomalies with time to detect, refusals, discrepancies, metrics, findings, lessons (operator-written) |
| 06 | `06-training-qrc` | 04 and 05 outputs, `references/qrc-outline.md` | `output/<slug>-qrc-<trigger>.md`: one card per contingency the mission met or planned for |

## Requirements

**P0**
- M1. Every stage CONTEXT.md in the three-section shape, with a Checkpoints row on 02, 03 and 05.
- M2. `references/` holds the outlines named above, written from public, generic structure
  (purpose, concept, phases, roles; objectives, measures, criteria; situation, mission,
  execution, contingencies, comms). No outline copies a controlled or proprietary format.
- M3. `references/log-reading-guide.md` explains C1 for a reader: which kinds matter for a
  debrief, how to compute time to detect (`anomaly.t_s` minus the fault's onset in the
  scenario or the first out-of-limit `tlm`), and that `null` is "not measured".
- M4. The debrief stage never writes lessons learned. It writes findings with line references
  (`seq`) and leaves a "Lessons learned (operator)" section reading "not yet written".
- M5. `setup/questionnaire.md`: operator name, default platform (copter, USV), unit system,
  organisation style notes. Flat, all at once, with defaults.
- M6. The worked example `examples/harbour-survey-sim/`: a simulated USV survey of a small
  harbour box, all six outputs, and the input log. If the drone repo's committed USV log is not
  available to this session, write a short C1-conformant example log by hand, mark it
  "illustrative, hand-written, not from a simulator run" in its provenance block, and say so in
  the debrief. Replace it with a real scenario log in a later PR.

**P1**
- M7. A `status` render example in the workspace CLAUDE.md.
- M8. A `references/glossary.md` for terms a newcomer would search: CONOPS, PIC, VO, RTL,
  geofence, failsafe, cross-track error, time to detect.

**P2**
- M9. A stage that turns a debrief's findings into a corrective-action list with owners.

## Acceptance Criteria

- Given only the example mission request, when an agent runs stage 02, then it reads at most
  the files in that stage's Inputs table and produces a CONOPS whose every number appears in
  the request.
- Given a log with a `tlm` line where `batt_pct` is null, when stage 05 runs, then the debrief
  says battery percentage was not measured at that time and does not report a minimum battery.
- Given the workspace-builder validation checklist, when run against the workspace, then every
  check passes.

## PR Plan

1. Scaffold, CLAUDE.md, CONTEXT.md, stage contracts, questionnaire (M1, M5).
2. Reference outlines and the log reading guide (M2, M3, M8).
3. The worked example (M4, M6).
4. Root CLAUDE.md and README entries, status example (M7).
