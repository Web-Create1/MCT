# QRC: Low Battery

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** Use this card when battery charge reaches the low-battery threshold during the harbour survey.

## 1. Trigger

Battery at 30 %. The flight controller returns to launch (RTL).

## 2. First Three Actions

1. MC: confirm the vehicle is in RTL; send no other mode.
2. VO: track the vehicle back to launch and call traffic.
3. PIC: disarm at launch; no relaunch on this battery.

## 3. Who to Tell

All crew: "Low battery, vehicle returning."

## 4. What to Log

`contingency` with trigger `low_battery` and the `tlm` lines on the way back. A `batt_pct` of null is "not measured"; the DL notes it.

## 5. When It Happened

Not met in this run.
