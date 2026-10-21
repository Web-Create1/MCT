# QRC: Lost Link

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** Use this card when the monitor warns of link loss during the harbour survey.

## 1. Trigger

Link-loss warning after 2 s without a ground link; the flight controller holds at 10 s and
returns to launch (RTL) at 60 s.

## 2. First Three Actions

1. VO: keep eyes on the vehicle and call its position.
2. MC: confirm the vehicle is in HOLD; do not send commands until the link is back.
3. PIC: when the link is back, decide resume or RTL, and say it aloud.

## 3. Who to Tell

All crew on the net: "Lost link, vehicle holding." PIC answers "resume" or "RTL".

## 4. What to Log

`anomaly` with rule `link_loss`, `contingency` with trigger `lost_link`, the PIC's `cmd`.
DL notes any lane-end report missed.

## 5. When It Happened

Simulated, illustrative log: loss at 600.0 s (seq 17), hold at 610.0 s (seq 19), PIC resumed
at 640.0 s (seq 21). A lane-end report was missed (seq 23).
