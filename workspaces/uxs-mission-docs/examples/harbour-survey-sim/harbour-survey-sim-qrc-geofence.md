# QRC: Geofence

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** Use this card when the vehicle reaches the geofence during the harbour survey.

## 1. Trigger

Vehicle at the box plus 30 m (fence 260 m x 180 m). The flight controller returns to launch (RTL).

## 2. First Three Actions

1. MC: confirm the vehicle is in RTL; send no other mode.
2. VO: track the vehicle and call its position against the box.
3. PIC: hold the run until the cause is understood.

## 3. Who to Tell

All crew: "Fence breach, vehicle returning."

## 4. What to Log

`contingency` with trigger `geofence`; DL notes the lane and position.

## 5. When It Happened

Not met in this run.
