# CONOPS: Harbour Survey (Simulated USV)

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** A USV rehearses, in simulation, a 7-lane survey of a 200 m x 120 m harbour box at
1.5 m/s on 2026-10-21 from 09:00 UTC, within a 40 min window. The PIC owns go and every
resume. The run does not start unless the lookout calls the harbour clear.

## 1. Purpose

Show that the survey pattern, the monitor and the contingency plan work together before any
hardware run is considered.

## 2. Concept

The USV launches from the box's south-west corner and drives east-west lanes 20 m apart at
1.5 m/s, inside a geofence of the box plus 30 m. The monitor watches cross-track error
(limit 5.0 m) and link health (alert after 2 s). At the last lane end the MC commands RTL.

## 3. Phases

| Phase | Entry | Activity | Exit | Lead |
|-------|-------|----------|------|------|
| Setup | Crew assembled | Load plan and geofence | Plan loaded | MC |
| Preflight | Plan loaded | Run the preflight card | All checks pass or accepted | PIC |
| Launch | PIC go | Arm, set AUTO | Vehicle on lane 1 | PIC |
| Survey | On lane 1 | Drive lanes, lookout reports lane ends | Last lane end | MC |
| Recovery | Last lane end | RTL, disarm | Disarmed at launch | MC, PIC |
| Post-mission | Disarmed | Save the ops log and notes | Log saved | DL |

## 4. Roles

| Code | Person | Duties |
|------|--------|--------|
| PIC | op-1 | Go decision, arming, resume after any hold, abort |
| MC | op-2 | Plan, mode changes, RTL at survey end |
| VO | op-3 | Harbour clear call, lane-end reports, traffic calls |
| DL | op-4 | Notes, discrepancies against procedure steps |
| AGENT | | Plan authoring and command line; no consent |
| SYSTEM | | Telemetry, anomalies, failsafes |

## 5. Comms Plan

All crew on one voice net. PIC says "go", "hold" or "abort"; nothing else starts, stops or
resumes the run. VO says "lane end" and the lane number, and "traffic" with a bearing.

## 6. Environment

Notional harbour box at the simulator's default origin. Other harbour users are possible.
Water current is not given.

## 7. Contingencies

| Trigger | Threshold | Response | By |
|---------|-----------|----------|----|
| Lost link | Alert 2 s, hold 10 s, RTL 60 s | Hold, then RTL | Flight controller |
| Low battery | 30 % | RTL | Flight controller |
| Geofence | Box plus 30 m | RTL | Flight controller |
| GPS loss | Fewer than 6 satellites or no 3D fix | Hold | Flight controller |

## 8. Risks

Current pushing the vehicle off its lane; lost link; traffic in the harbour; GPS loss; low
battery; geofence breach.

## 9. Open Questions

- Water current is not given.
