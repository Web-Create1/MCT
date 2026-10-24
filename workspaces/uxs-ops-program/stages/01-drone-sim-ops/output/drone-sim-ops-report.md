# Stage 01 Report: Drone Sim Ops

**Session:** `session_01YSkxodJYmJpxTEW7C3tQL9` · **Finished:** 2026-10-22 · **State:** draft PRs open, CI green on all ten

## PRs

Web-Create1/AI-Drone-Project#65 to #74, one per row of the PRD 05 plan, stacked on #64. Merge in order.

| Rows | R-ids closed |
|------|-------------|
| #65 to #74 | R1, R2, R3, R4, R5, R6, R7, R8, R9 (Python sim half), R10, R12 |

Tests 105 before, 229 after (`pytest src -q`), 2 SITL tests skipped unless `AIDRONE_SITL=1`.
The `/ops` page replays five Python sim runs, committed unedited, each passing
`verify-log --strict`, labelled "Python sim".

## Found and fixed on the way

- `FlightSession.goto` measured the safety radius from the current position, not from home,
  and refused a legal leg between two in-fence corners. Fixed in #70.
- The envelope accepted stale telemetry, so a frozen reading during a link loss passed every
  check. It now refuses telemetry older than 2 s.
- `*.jsonl` was gitignored, so the log fixture never reached CI. A gitignore exception was
  merged forward through every branch.

## Where a rule won

A fully automated SITL mission test would have needed scripted consent outside the Python sim,
which drone invariant 4 forbids. The full SITL run is a manual step for Eric, and `ops fly`
refuses the agent and any non-terminal caller.

## Open for Eric

1. **Consent** (top of #66): PIC passphrase and the existing phrase (built, the PRD default),
   or the passphrase alone.
2. **SITL run** (#72 body): run the WSL2 block, commit the two logs, and report the Rover boat
   frame name actually used (`motorboat` is a guess). Closes R9's SITL half and program goal 4.
3. **Revoke** (contract C3): only a PIC may revoke consent today. Revoking only removes
   permission, so the build session proposes making it ungated. Changing it means editing C3
   in `references/integration.md` and the drone code together.

## Cut

R11 (`ops export`), a should-ship item that the PRD's PR plan left out. The Lighthouse
first-paint metric was not measured. R13 to R15 stay design-only.
