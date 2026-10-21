# UxS Ops Program

The control plane for a four-repo upgrade that turns a simulation-only drone project into an
inspectable uncrewed systems (UxS) operations portfolio: mission planning, telemetry monitoring,
anomaly escalation, test logging, debriefs, training cards, and operator accounts.

This workspace holds the program PRD and one stage contract per build. The code lives in the
target repos. Each build session reads one stage contract and the files it names, nothing else.

## Folder Map

```
uxs-ops-program/
├── CLAUDE.md                 (you are here)
├── CONTEXT.md                (start here for task routing)
├── runs.md                   (live register of build sessions)
├── setup/questionnaire.md    (already answered, kept for the `setup` trigger)
├── references/
│   ├── program-prd.md        (problem, goals, non-goals, personas, metrics, phasing)
│   ├── role-map.md           (target role duties -> capability -> deliverable -> proof)
│   ├── integration.md        (cross-repo contracts: log schema, roles, links, units)
│   ├── honesty-rules.md      (what public copy may and may not claim)
│   ├── design-language.md    (ops console rules every repo follows)
│   └── session-protocol.md   (how a build session runs cheaply and safely)
└── stages/
    ├── 01-drone-sim-ops/          (AI-Drone-Project: ops layer, SITL, USV, /ops page)
    ├── 02-flight-eye-accounts/    (Flight-Eye: passkey accounts and sync)
    ├── 03-c5isr-case-study/       (C51SR-T: drone ops read through C5ISR-T, NIST CSF, AAA)
    ├── 04-mission-docs-workspace/ (MCT: an ICM pipeline for CONOPS to debrief)
    └── 05-integration-review/     (program: role-map coverage, honesty audit, links)
```

## Triggers

| Keyword | Action |
|---------|--------|
| `setup` | Confirm the answers in `setup/questionnaire.md`; nothing else to configure |
| `status` | Scan `stages/*/output/` and render the pipeline, as `_core/CONVENTIONS.md` describes |

## Routing

| Task | Go To |
|------|-------|
| Build the drone ops layer and simulation | `stages/01-drone-sim-ops/CONTEXT.md` |
| Build Flight Eye accounts | `stages/02-flight-eye-accounts/CONTEXT.md` |
| Build the C5ISR-T case study page | `stages/03-c5isr-case-study/CONTEXT.md` |
| Build the mission docs workspace | `stages/04-mission-docs-workspace/CONTEXT.md` |
| Check the whole program before calling it done | `stages/05-integration-review/CONTEXT.md` |
| Understand why any of this exists | `references/program-prd.md`, "Problem" and "Goals" only |

## What to Load

| Task | Load These | Do NOT Load |
|------|-----------|-------------|
| Any build stage | That stage's `CONTEXT.md`, then only the rows of its Inputs table | Other stages, `role-map.md` (the review stage owns it) |
| Integration review | `stages/05-integration-review/CONTEXT.md` and its Inputs | Target repo source code |
| Changing scope | `references/program-prd.md` in full | Target repo PRDs until scope is settled |

## Rules That Override Everything Here

1. **The target repo's own `CLAUDE.md` wins** over anything in this workspace. Its invariants
   (ArduPilot flies, Python plans; escape hatches never gated; SITL before hardware; zero
   dependencies in Flight Eye) are not negotiable from here.
2. **Simulation is labelled as simulation, every time.** See `references/honesty-rules.md`.
3. **One concern per PR, branch off the PRD branch, draft PR into `main`.**
4. **No em dashes** in any file in any of the four repos.

## Stage Handoffs

Build sessions run in the target repo and cannot write here. When a stage's PRs are open, the
orchestrating session writes `stages/0N-*/output/<slug>-report.md`: session id, PR links, what
shipped, what was cut. `status` reads those files.
