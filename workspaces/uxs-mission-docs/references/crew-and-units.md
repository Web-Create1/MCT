# Crew and Units

A reader's copy of the UxS ops program's crew roles and unit rules. The canonical source is
`workspaces/uxs-ops-program/references/integration.md`, contracts C2 and C5. If they differ,
that file wins and this one is updated.

## Roles

| Code | Role | Duties in a document |
|------|------|----------------------|
| `PIC` | Person in command | Owns the go decision and the only arming consent. For a USV, the vessel operator |
| `MC` | Mission commander | Plans and runs the mission under the PIC's consent |
| `VO` | Visual observer or lookout | Watches the vehicle and the airspace or water; calls traffic and hazards |
| `DL` | Data logger | Records notes and discrepancies against procedure steps |
| `OBS` | Observer or trainee | Notes only, no actions |
| `AGENT` | The AI coding agent | Authors plans and runs the command line. Never a person, never grants consent |
| `SYSTEM` | Driver, monitor, flight controller | Telemetry, anomalies, failsafes |

Rules for documents:

- Every mission names one PIC. One person may hold two roles; write both codes.
- Consent to arm, resume, or override a failsafe is always the PIC's.
- `AGENT` and `SYSTEM` never appear as the owner of a go or no-go decision.

## Units

| Platform | Distance | Speed | Heading | Power | Charge |
|----------|----------|-------|---------|-------|--------|
| Copter, USV | metres (m) | m/s | degrees true | volts (V) | percent (%) |
| Aviation charts | feet (ft), nautical miles (nm) | knots (kt) | degrees true | | |

- Every number carries its unit. Durations are seconds (s) or minutes (min), written out.
- A document that converts shows both units, original first: `20 m (66 ft)`.
- Times in a log are `t_s`, seconds since the mission's first line. Wall-clock times are UTC.
