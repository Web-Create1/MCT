# Preflight Card: Harbour Survey (Simulated USV)

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** Every line passes, or the PIC accepts it aloud, before arming.

| # | Check | Owner | Method | Pass value |
|---|-------|-------|--------|------------|
| 1 | Plan loaded | MC | manual | 14 waypoints |
| 2 | Geofence loaded | SYSTEM | auto | 260 m x 180 m, box plus 30 m |
| 3 | Battery | SYSTEM | auto | At least 16.0 V and 90 % |
| 4 | GPS | SYSTEM | auto | 3D fix and at least 6 satellites |
| 5 | Ground link | SYSTEM | auto | Link healthy |
| 6 | Contingency thresholds | MC | manual | Lost link 2 s, 10 s, 60 s; battery 30 % |
| 7 | Harbour clear | VO | manual | "Clear" called |
| 8 | Water current | DL | manual | Measured, or `not-measured` accepted by PIC |
| 9 | Crew on net | PIC | manual | Every role answers |
| 10 | Arming consent | PIC | manual | PIC says "go" |
