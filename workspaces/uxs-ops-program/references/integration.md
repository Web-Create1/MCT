# Integration Contracts

Cross-repo interfaces. Each contract has one home, here. A repo implements a contract and
documents its implementation in its own files; it does not restate the contract.

| ID | Contract | Producer | Consumers |
|----|----------|----------|-----------|
| C1 | Ops log format `uxs-ops-log/1` | AI-Drone-Project | drone `/ops` page, MCT `uxs-mission-docs` debrief stage, C51SR-T case study excerpts |
| C2 | Crew roles | AI-Drone-Project | MCT briefs and QRCs, C51SR-T AAA section |
| C3 | Authorization matrix | AI-Drone-Project | C51SR-T AAA section |
| C4 | Public link rules | all | all |
| C5 | Units | all | all |
| C6 | Provenance block | AI-Drone-Project | every page that shows a simulated number |

---

## C1: Ops log `uxs-ops-log/1`

One JSON object per line, UTF-8, LF line endings, keys in the order below, serialised with
`json.dumps(obj, separators=(",", ":"), ensure_ascii=False)` so the bytes are reproducible.

| Field | Type | Rule |
|-------|------|------|
| `v` | string | Always `"uxs-ops-log/1"` |
| `seq` | int | 0 on the first line, +1 per line, no gaps |
| `t_utc` | string | ISO 8601 UTC with milliseconds, `2026-10-21T23:41:07.125Z` |
| `t_s` | number | Seconds since the mission's first line, from a monotonic clock. Orders events if the wall clock jumps |
| `mission` | string | `<yyyymmdd>-<slug>-<4 hex>`, same on every line |
| `kind` | string | One of `provenance`, `plan`, `preflight`, `cmd`, `tlm`, `anomaly`, `refusal`, `contingency`, `note`, `discrepancy`, `end` |
| `actor` | object | `{"operator": "<id>" or null, "role": "<C2 role>"}`. A null operator means unattributed, which only escape hatches and SYSTEM lines may be |
| `body` | object | Shape per kind, below |
| `prev` | string | SHA-256 hex of the previous line's exact bytes without its newline. 64 zeros on `seq` 0 |

Body per kind (null means not measured, never zero):

| Kind | Body |
|------|------|
| `provenance` | `{git_sha, driver, ardupilot, seed, profile, envelope}`. Always `seq` 0. See C6 |
| `plan` | `{name, profile, waypoints: n, contingencies: {lost_link, low_battery, geofence, gps_loss}}` |
| `preflight` | `{item, method: "auto" or "manual", result: "pass", "fail", "not-measured" or "confirmed", evidence}` |
| `cmd` | `{name, args, result: "sent", "acked", "refused", "failed" or "timeout"}` |
| `tlm` | `{lat, lon, alt_m, gs_mps, hdg_deg, batt_v, batt_pct, gps_fix, sats, link_ok, mode, xtrack_m}` |
| `anomaly` | `{rule, sev: "advisory", "caution" or "warning", detail, value, threshold, unit, recommended}` |
| `refusal` | `{cmd, reason, rule}` from the envelope |
| `contingency` | `{trigger, action, by: "fc", "operator" or "monitor-recommended"}` |
| `note` / `discrepancy` | `{text}` / `{expected, observed, step}` |
| `end` | `{outcome: "complete", "aborted", "rtl", "landed" or "emergency", duration_s, lines}` |

**Verification.** A log verifies when `seq` is contiguous, `v` matches, every `prev` matches the
SHA-256 of the line before, `seq` 0 is `provenance` and the last line is `end`. This is
tamper-evident, not tamper-proof: anyone can rewrite the whole chain. Say so wherever it is shown.

## C2: Crew roles

| Code | Role | Notes |
|------|------|-------|
| `PIC` | Person in command | The only role that grants arming consent. For a USV, the vessel operator |
| `MC` | Mission commander | Plans and runs the mission under the PIC's consent |
| `VO` | Visual observer or lookout | Watches the vehicle and the airspace or water |
| `DL` | Data logger | Records notes and discrepancies |
| `OBS` | Observer or trainee | Notes only |
| `AGENT` | Claude Code | Authors plans and runs the CLI. Never a person, never authenticated, never grants consent |
| `SYSTEM` | Driver, monitor, flight controller | Telemetry, anomalies, failsafes |

## C3: Authorization matrix

| Action | PIC | MC | VO | DL | OBS | AGENT | Unattributed |
|--------|-----|----|----|----|-----|-------|--------------|
| Grant or revoke consent | yes | no | no | no | no | never | no |
| Add or remove an operator | yes, at a terminal | no | no | no | no | never | no |
| Takeoff, move, goto, mission (with live consent) | yes | yes | no | no | no | yes, logged with the consenting PIC | no |
| Land, RTL, emergency stop | yes | yes | yes | yes | yes | yes | **yes, always** |
| Note, discrepancy | yes | yes | yes | yes | yes | yes | no |

The last-but-one row is drone invariant 2: escape hatches are never gated, not even on identity.

## C4: Public link rules

| Repo | Visibility | Link from public pages to |
|------|-----------|---------------------------|
| AI-Drone-Project | private | `https://ai-drone-project.vercel.app/<route>` only. Its CI fails on a blob link |
| Flight-Eye | private | `https://flight-eye-sigma.vercel.app` only |
| C51SR-T-framework-NIST-2.0 | private | Its deployed site only |
| MCT | public | GitHub URLs are fine |

## C5: Units

Each repo keeps its system and every number carries its unit. Drone and USV: metres, m/s,
degrees true, volts, percent (ArduPilot's own). Flight Eye: feet, knots, nautical miles. A page
that converts shows both, original first.

## C6: Provenance block

Every page or document that shows a simulated number shows, near the top: the word
**Simulation**, the driver (`Python sim` or `ArduPilot SITL <version>`), the scenario and seed,
the date of the run and the drone repo commit it ran on.
