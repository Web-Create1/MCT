# Mission Request: Harbour Survey (Simulated USV)

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** Rehearse, in simulation, a lawnmower survey of a 200 m x 120 m harbour box by an
uncrewed surface vessel (USV) on 2026-10-21 from 09:00 UTC, to check track keeping, the
monitor's alerts, and the lost-link response. The run stops if the harbour is not clear.

## 1. Objective

Cover the whole box in parallel lanes and show that the vehicle keeps its lanes, the monitor
flags faults quickly, and the planned contingencies behave as written.

## 2. Platform

USV, ArduPilot Rover firmware in simulation, scripted from a ground PC.

## 3. Area

A notional harbour box at the simulator's default origin (-35.363261, 149.165230), which is the
launch point and the box's south-west corner. Box: 200 m east-west by 120 m north-south.
Lanes run east-west, 20 m apart. Geofence: the box plus a 30 m buffer on every side.

## 4. Window

2026-10-21, start 09:00 UTC, length 40 min.

## 5. Crew

| Code | Person |
|------|--------|
| PIC | op-1 (notional) |
| MC | op-2 (notional) |
| VO | op-3 (notional), lookout |
| DL | op-4 (notional) |
| AGENT | Authors the plan and runs the command line |

## 6. Limits

- Survey speed: 1.5 m/s. Envelope maximum speed: 2.0 m/s.
- Cross-track limit: 5.0 m.
- Battery at launch: at least 16.0 V and 90 %.
- Monitor detection target: an anomaly line within 10 s of a fault's onset.

## 7. Contingency Thresholds

| Trigger | Threshold | Response |
|---------|-----------|----------|
| Lost link | Monitor alert after 2 s; hold at 10 s; return to launch (RTL) at 60 s | Flight controller |
| Low battery | 30 % | RTL, flight controller |
| Geofence | Box plus 30 m | RTL, flight controller |
| GPS loss | Fewer than 6 satellites or no 3D fix | Hold, flight controller |

## 8. Constraints

- The VO reports each lane end aloud; the DL records each report.
- No speed change above the envelope maximum, whoever asks.
- Arming and resuming after a hold need the PIC's consent.

## 9. Open Questions

- Water current: no meter is available. Not given.
