# Program PRD: UxS Ops Portfolio Upgrade

**Owner:** Eric Adler · **Written:** 2026-10-21 · **Status:** approved to build, stages 01 to 04 running
**Scope:** four repos. Per-repo requirements live in each repo's PRD (paths in "Requirements by stage").

## Problem

The target role is an entry-level uncrewed systems operations specialist: unmanned surface
vessel (USV) setup and pre-mission checks, telemetry monitoring, anomaly escalation, contingency
execution, test logging, mission reports, and training material. The two public proofs Eric
points reviewers at, the drone site and Flight Eye, show safety-first engineering but almost none
of that operational work product. There is no mission plan a reviewer can read, no telemetry
console, no field log, no debrief, no quick-reference card, and no surface vessel anywhere.

Underneath that, the drone stack's only passing gate (G0) runs on a pure Python simulator. The
ArduPilot SITL loop the roadmap promises was never closed: `drivers/mavlink.py` does not exist.
And nothing in any repo ties an action to a person: consent is a phrase typed at a terminal,
not an operator with a role, and Flight Eye forgets everything when a browser is cleared.

Cost of not solving it: a reviewer reads "simulation only, 105 tests" and cannot see whether the
candidate can plan, monitor, log and report, which is the job.

## Goals

| # | Outcome | Measured by |
|---|---------|-------------|
| G1 | Every duty group in the target role maps to an inspectable artifact on a public URL | `role-map.md`: 9 of 9 duty groups at status `shipped` with a working URL |
| G2 | One command runs a full simulated mission, copter or USV, and leaves a field log, an anomaly timeline and a debrief | `python -m src.ops.cli scenario run nominal-copter --target sim` exits 0 and writes three files; same for `nominal-usv` |
| G3 | Faults are rehearsed, not hoped about | At least 8 fault scenarios, each asserting its expected anomaly, severity, time to detect and vehicle outcome, green in CI |
| G4 | Every command in a mission log is attributed to a person or marked unattributed | `ops verify-log` passes on every committed log; 0 lines with a missing actor |
| G5 | Flight Eye saved flights and alert settings follow the owner between two devices | Sign in on phone and desktop with passkeys, star on one, see it on the other within one poll; zero new npm dependencies |
| G6 | Build sessions stay cheap | Each stage contract under 80 lines; each build session's required reading is 6 files or fewer before its first edit |

## Non-Goals

| Not doing | Why |
|-----------|-----|
| Buying or flying hardware | Invariant 6 in the drone repo: SITL before hardware. Phase 1 money is still blocked on the BOM rewrite |
| Claiming operational USV or UAS experience | Nothing has been operated. The work is simulation and documentation, and says so |
| Any employer's branding, proprietary data, or export-controlled material | All inputs are public: ArduPilot, MAVLink, FAA rules, public job text |
| Weapons or targeting features | The "T" in C5ISR-T is read as precision-landing target acquisition, which the drone roadmap already has |
| Accounts on the drone public site or the C5ISR-T site | Both are static, public and auth-free by design. Operator identity in the drone repo is local CLI only |
| Live command and control from a web page | Nothing on a public page can command a vehicle, simulated or not |
| An MCP server in any runtime path | Drone ADR 0001. The control surface stays a plain Python CLI |

## Personas

1. **Eric, operator in training.** Runs the simulator, plays every crew role, writes the reports.
   Visual learner, hardware beginner. Needs diagrams and checklists, not prose.
2. **Claude Code, mission-script author.** Edits mission files and runs the CLI. Cannot grant
   consent, cannot authenticate as an operator, never stabilises a vehicle.
3. **The reviewer.** A senior operations specialist or hiring manager with five minutes and a
   phone. Opens a public URL, wants to see a mission brief, a console and a debrief.
4. **A future crew member** (visual observer, data logger). Reads the quick-reference card,
   logs a discrepancy, never needs repo access.

## User Stories (priority order)

- As the reviewer, I want one page that replays a real simulated mission with its telemetry,
  anomalies and operator log, so I can judge ops literacy in five minutes.
- As Eric, I want a preflight checklist that checks what it can measure and makes me confirm
  what it cannot, so I never mistake an unmeasured item for a passed one.
- As Eric, I want to inject a link loss or a GPS dropout into a simulated mission and see it
  detected, escalated and handled, so contingency procedures are rehearsed before a field day.
- As Eric, I want the same mission tooling to drive a simulated boat, so surface vessel
  operations are something I have practised and can describe accurately.
- As the person in command, I want only my role to grant arming consent, while anyone can
  trigger land, RTL or stop, so authority is clear and the escape hatches stay open.
- As a data logger, I want a log that shows if a line was altered or removed, so a debrief can
  be trusted.
- As Eric, I want my Flight Eye saved flights on my phone and my desktop without an email or a
  password, so the tracker is a tool I carry rather than a tab I lose.
- As the reviewer, I want CONOPS, test plan, mission brief, debrief and quick-reference card
  examples produced from the same simulated mission, so documentation skill is shown rather
  than asserted.

## Requirements by Stage

Each repo PRD is canonical for its requirements. This table is the index, not a copy.

| Stage | Repo | PRD | P0 headline |
|-------|------|-----|-------------|
| 01 | AI-Drone-Project | `docs/05-ops-and-sim-prd.md` | Ops log, operator roles, plan and preflight, monitor, scenarios, debrief, MAVLink SITL driver, USV profile |
| 02 | Flight-Eye | `docs/PRD-ACCOUNTS.md` | Passkey register and sign-in, signed session cookie, sync document, delete account |
| 03 | C51SR-T-framework-NIST-2.0 | `docs/prd/drone-ops-case-study.md` | `/drone-ops` page in the Projects tab |
| 04 | MCT | `stages/04-mission-docs-workspace/CONTEXT.md` (this workspace) | `workspaces/uxs-mission-docs/` with one worked example run |

## Success Metrics

**Leading (first two weeks):** stages 01 to 04 have draft PRs with green CI; G2 and G3 pass in
CI; the `/ops` page and `/drone-ops` page render on a 390 by 844 viewport with no horizontal scroll.

**Lagging (first month):** role map at 9 of 9 shipped; the reviewer can find a CONOPS, a
console, a debrief and a quick-reference card from the drone site home page in three taps or
fewer; zero honesty-audit findings open in stage 05.

## Open Questions

| Question | Who | Blocking? |
|----------|-----|-----------|
| Does `sim_vehicle.py -v Rover -f motorboat` exist in the ArduPilot version Eric runs in WSL2? | Engineering, first SITL run | No: the Python sim USV profile ships first |
| Which `SIM_*` fault parameters survived the 4.7 renames? | Engineering, before writing SITL scenarios | Only for SITL scenarios |
| Does Flight Eye's Upstash plan have room for account documents at the free tier? | Eric | No: accounts degrade to "unavailable" honestly |
| Should the drone site link to the C5ISR-T case study and the MCT example run? | Eric | No |

## Phasing

1. **Now:** stages 01 to 04 in parallel, one build session each, small PRs.
2. **After their PRs merge:** stage 05 review, role map closed out, handoff files updated.
3. **Later, outside this program:** Phase 1 hardware, MAVLink2 signing on a real link, a maritime
   (AIS) layer in Flight Eye, which needs a data-source and terms study before any code.
