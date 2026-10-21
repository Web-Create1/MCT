# QRC: GPS Loss

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** Use this card when the vehicle loses GPS during the harbour survey.

## 1. Trigger

Fewer than 6 satellites or no 3D fix. The flight controller holds.

## 2. First Three Actions

1. VO: keep eyes on the vehicle and call drift.
2. MC: confirm the vehicle is in HOLD; send no commands.
3. PIC: when the fix is back, decide resume or RTL, and say it aloud.

## 3. Who to Tell

All crew: "GPS lost, vehicle holding."

## 4. What to Log

`contingency` with trigger `gps_loss`, the `tlm` `sats` and `gps_fix` values, the PIC's `cmd`.

## 5. When It Happened

Not met in this run.
