# UxS Ops Program: Task Routing

Five stages. Stages 01 to 04 are independent builds in four repos and can run in parallel.
Stage 05 runs last and reads their outputs.

## Task Routing

| Task Type | Go To | Repo | Description |
|-----------|-------|------|-------------|
| Drone ops layer and simulation | `stages/01-drone-sim-ops/CONTEXT.md` | `Web-Create1/AI-Drone-Project` | Mission plans, preflight, monitor, hash-chained log, operator roles, scenarios, MAVLink SITL driver, USV profile, `/ops` replay page |
| Flight Eye accounts | `stages/02-flight-eye-accounts/CONTEXT.md` | `Web-Create1/Flight-Eye` | Passkey accounts from `node:crypto`, cross-device sync of saved flights, prefs and alerts |
| C5ISR-T case study | `stages/03-c5isr-case-study/CONTEXT.md` | `Web-Create1/C51SR-T-framework-NIST-2.0` | A Projects tab page reading the drone stack through C5ISR-T, NIST CSF 2.0 and AAA |
| Mission docs workspace | `stages/04-mission-docs-workspace/CONTEXT.md` | `Web-Create1/MCT` | `workspaces/uxs-mission-docs/`: intake, CONOPS, test plan, brief and preflight card, debrief, quick-reference card |
| Integration review | `stages/05-integration-review/CONTEXT.md` | all four | Role-map coverage, honesty audit of public copy, link check, handoff files |

## Dependency Graph

```
01-drone-sim-ops ──(log schema C1, roles C2)──┐
02-flight-eye-accounts ───────────────────────┤
03-c5isr-case-study ──(reads 01's public routes)┼──> 05-integration-review
04-mission-docs-workspace ──(consumes C1)─────┘
```

Contracts C1 to C6 live in `references/integration.md`. A stage that needs one reads only
that contract's section, not the file.

## Shared Resources

| Resource | Location | Contains |
|----------|----------|----------|
| Program PRD | `references/program-prd.md` | Why, for whom, what success is |
| Role map | `references/role-map.md` | Duty-by-duty coverage table, owned by stage 05 |
| Contracts | `references/integration.md` | C1 log schema, C2 roles, C3 authorization, C4 links, C5 units, C6 provenance |
| Honesty rules | `references/honesty-rules.md` | Claims policy for every public surface |
| Design language | `references/design-language.md` | Status hierarchy, staleness, telemetry tiles, console layout |
| Session protocol | `references/session-protocol.md` | Read budget, PR rules, commit identity, handoff |
