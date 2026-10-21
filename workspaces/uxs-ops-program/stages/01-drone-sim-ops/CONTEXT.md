# 01 Drone Sim Ops

Build the mission operations layer, the ArduPilot SITL loop and a surface vessel profile in
`Web-Create1/AI-Drone-Project`, then publish one simulated mission as the `/ops` replay page.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Drone repo | `CLAUDE.md` | Full file (auto-loaded) | Six invariants. They outrank this contract |
| Drone repo | `HANDOFF.md` | "Where this is", "Decisions already made", "The facts that change decisions" | State and the decisions not to re-litigate |
| Drone repo | `docs/05-ops-and-sim-prd.md` | Full file once, then only the R-section for the current PR | The requirements, acceptance criteria and PR plan |
| Drone repo | `docs/adr/0002-vehicle-abstraction-seam.md` | "Decision" | Before writing any driver |
| Drone repo | `src/beta/vehicle.py`, `session.py`, `consent.py`, `envelope.py` | `grep -n` for the symbol, then that range | The seam the ops layer sits on |
| This workspace | `../../references/integration.md` | C1, C2, C3, C6 only | Log format, roles, authorization, provenance |
| This workspace | `../../references/design-language.md` | Sections 1 to 4 | Only for the `/ops` page PR |

## Process

1. Read the Inputs above in order. Run `python -m pytest src -q` and record the count.
2. Work the PRD's PR plan in order, one branch and one draft PR per item.
3. For each PR: tests first for the acceptance criteria, then code, then the repo checks in
   `../../references/session-protocol.md`, then push.
4. For the `/ops` page: run the two nominal scenarios and one fault scenario on the Python sim,
   commit the logs unedited, build the page with the generator, confirm `verify-log` passes.
5. Update `HANDOFF.md` and `ROADMAP.md` in the last PR.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 2, before the operator-roles PR | The authorization matrix as implemented | Whether the PIC-only consent rule fits how Eric flies |

## Audit

| Check | Pass Condition |
|-------|---------------|
| Invariants | `rtl`, `land`, `emergency` run with no consent, no operator, no envelope check |
| Agent cannot consent | Granting consent or adding an operator with stdin not a TTY is refused, with a test |
| Unknown is not zero | Every `None` telemetry field reaches the log as `null` and the page as "not measured" |
| Log verifies | `verify-log` passes on every committed log and fails on a one-byte edit, with a test |
| Honesty | `/ops` shows the C6 provenance block above the fold |
| Gates | pytest, `check-conventions.py` and the stale-`web/` gate green on every PR |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Draft PRs | `Web-Create1/AI-Drone-Project` | One per PR-plan item |
| Stage report | `output/drone-sim-ops-report.md` | Written by the orchestrator: session id, PR links, R-ids closed, cuts |
