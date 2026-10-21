# Test Plan: Harbour Survey (Simulated USV)

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** Six objectives, each read from the ops log or a named manual method. Go needs every
preflight check passed or accepted by the PIC and no residual risk above 9.

## 1. Objectives

- O1. Complete all lanes of the survey (Survey phase).
- O2. Keep cross-track error within limit on every lane (Survey).
- O3. The monitor flags each fault within the detection target (Survey).
- O4. The lost-link contingency holds as planned and resumes only on PIC consent (Survey).
- O5. The envelope refuses a command above maximum speed (Survey).
- O6. Battery stays at or above the low-battery threshold throughout (all phases).

## 2. Measures

| Objective | Measure | Unit | Source |
|-----------|---------|------|--------|
| O1 | Run outcome; lane-end reports | count | `end.outcome`; VO reports logged by DL |
| O2 | Cross-track error in AUTO | m | `tlm.xtrack_m` |
| O3 | Time to detect | s | `anomaly.t_s` minus onset, per the log reading guide |
| O4 | Loss onset to hold; who resumed | s; role | `tlm.link_ok`, `contingency.t_s`, `cmd.actor.role` |
| O5 | Refusal present | yes or no | `refusal` line |
| O6 | Battery charge | % | `tlm.batt_pct` |

## 3. Procedure

| Step | Owner | Action | Expected |
|------|-------|--------|----------|
| P-1 | MC | Load plan and geofence | 14 waypoints, fence 260 m x 180 m |
| P-2 | SYSTEM | Auto preflight: battery, GPS, geofence | All pass |
| P-3 | VO | Call the harbour clear | Confirmed |
| P-4 | DL | Record water current | Not measured; PIC accepts or stops |
| P-5 | PIC | Arm | Acked |
| P-6 | MC | Set AUTO | Acked, vehicle on lane 1 |
| P-7 | MC | Request 3.0 m/s once lane 2 is done | Refused by envelope |
| P-8 | SYSTEM | Ground link drops during the run (the fault under test) | Alert, then hold |
| P-9 | VO | Report each lane end | 7 reports |
| P-10 | PIC | Resume AUTO after link returns | Acked |
| P-11 | MC | RTL at the last lane end | Acked |
| P-12 | PIC | Disarm at launch | Acked |

Derived: 7 lanes = 120 m / 20 m + 1. Path = 7 x 200 m + 6 x 20 m = 1520 m, about
1013 s (17 min) at 1.5 m/s, inside the 40 min window. Fence = (200 + 2 x 30) m by
(120 + 2 x 30) m = 260 m x 180 m. Waypoints = 7 lanes x 2 ends = 14.

## 4. Pass Criteria

| Objective | Criterion | Threshold | From |
|-----------|-----------|-----------|------|
| O1 | Outcome complete and 7 lane-end reports | 7 | Derived lane count |
| O2 | Every AUTO `xtrack_m` at or below limit | 5.0 m | Request, Limits |
| O3 | Every TTD at or below target | 10 s | Request, Limits |
| O4 | Hold within 10 s of onset; resume by PIC | 10 s | Request, Contingencies |
| O5 | Refusal logged for 3.0 m/s | 2.0 m/s maximum | Request, Limits |
| O6 | Every `batt_pct` at or above threshold | 30 % | Request, Contingencies |

## 5. Risk Register

| Risk | L | S | Score | Mitigation | Owner | Residual |
|------|---|---|-------|------------|-------|----------|
| Current sets vehicle off lane | 3 | 2 | 6 | Cross-track caution at 5.0 m; MC may slow | MC | 4 (L2, S2) |
| Lost link | 2 | 4 | 8 | Hold at 10 s, RTL at 60 s | SYSTEM | 4 (L2, S2) |
| Traffic enters the box | 2 | 5 | 10 | Lookout; PIC abort call | VO, PIC | 5 (L1, S5) |
| GPS loss | 2 | 3 | 6 | Hold below 6 satellites or no 3D fix | SYSTEM | 4 (L2, S2) |
| Low battery | 1 | 4 | 4 | Launch at 16.0 V and 90 %; RTL at 30 % | PIC | 4 |
| Geofence breach | 1 | 4 | 4 | RTL at box plus 30 m | SYSTEM | 4 |

## 6. Go and No-Go

- Go: every P-2 check passes, P-3 confirmed, P-4 accepted by the PIC, battery at least
  16.0 V and 90 %, no residual above 9.
- No-go or abort: traffic in the box, any failed preflight check, or the PIC's call.

## 7. Data to Keep

The ops log unedited, the DL's notes, and this plan as run.
