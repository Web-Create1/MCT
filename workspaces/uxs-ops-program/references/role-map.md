# Role Map

The target role, duty group by duty group, against what a reviewer can open and inspect.
Source: a public posting for an entry-level USV operations specialist, San Diego, dated
2026-10-20. The posting itself and the application notes live in a private repo; this file
carries only the duty groups.

**Status values:** `exists` (live today), `planned` (in a stage), `shipped` (merged and live),
`gap` (nothing planned, say why). Stage 05 owns this file and updates statuses from merged PRs.

| # | Duty group | What proving it looks like | Deliverable | Stage | Status |
|---|-----------|----------------------------|-------------|-------|--------|
| D1 | Program and operational support: R&D, test events, demos, tracking progress, flagging concerns | A visible plan with gates, and concerns recorded where they were found | Drone roadmap gates G0 to G4 and the audit register | existing | exists |
| D2 | Mission planning and coordination: route planning, environment, contingencies, CONOPS, test plan support, mission briefs, debriefs | A mission plan file with contingencies, and a CONOPS, test plan and brief produced from it | Mission plan format with contingency block (drone R1); `uxs-mission-docs` workspace and example run | 01, 04 | planned |
| D3 | USV operations: setup, pre-mission checks, monitoring C2 and telemetry, logging navigation, propulsion, payload and link health | A USV run in simulation with a preflight record and a telemetry log | USV profile on the sim and SITL drivers (R9); preflight runner (R2); `/ops` replay (R10) | 01 | planned |
| D4 | Real-time monitoring and incident response: alerts, anomalies, contingency procedures, timely reporting | Anomalies detected, graded and escalated with a recommended action and a time to detect | Telemetry monitor and rules (R4); fault scenarios (R5); quick-reference cards (R12) | 01 | planned |
| D5 | Test execution and technical feedback: procedures, observations, discrepancies, field logs | Scripted tests with expected outcomes, and a log that shows tampering | Scenario library with assertions (R5); hash-chained ops log (R3); existing field runbook | 01 | planned |
| D6 | Data analysis and reporting: mission data, metrics, findings, lessons learned, recommendations | A debrief generated from a log, with operator-written lessons | Debrief generator (R6); debrief stage of `uxs-mission-docs` | 01, 04 | planned |
| D7 | Training and operational support: operator training, manuals, quick-reference cards | One-page cards a new crew member can use cold | QRC set (R12); QRC stage of `uxs-mission-docs` | 01, 04 | planned |
| D8 | Compliance, safety and risk: regulations, safety procedures, risk assessment | Rules cited with dates, a risk register per test, authority that matches the rules | Existing `/regulatory` page; risk section in the test plan stage; operator roles and consent (R7) | 01, 04 | planned |
| D9 | Cross-functional integration: autonomy, payload, logistics teams | One system read through the frameworks those teams use | `/drone-ops` case study (C5ISR-T, NIST CSF 2.0, AAA) | 03 | planned |

## Qualifications Row

| Qualification | Proof |
|---------------|-------|
| Command-and-control software, telemetry tools | MAVLink SITL driver (R8), telemetry monitor (R4), `/ops` console (R10) |
| Attention to detail in data recording | Hash-chained log plus `verify-log` (R3); "not measured" never shown as zero |
| Reading and following technical procedures | Field runbook, preflight runner, scenario assertions |
| Clear written communication | `uxs-mission-docs` example run; every PR in four repos |

## Not a Duty, Still Worth Building

Flight Eye accounts (stage 02) do not map to a duty line. They are there because the user asked
for the portfolio to be more functional, and multi-device situational awareness is a real need
for anyone carrying a tracker into the field. Do not dress them up as a duty match.
