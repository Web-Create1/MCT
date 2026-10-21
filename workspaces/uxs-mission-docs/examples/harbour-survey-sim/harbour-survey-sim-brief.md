# Brief: Harbour Survey (Simulated USV)

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** Simulated USV survey of the 200 m x 120 m harbour box, 7 lanes at 1.5 m/s, go at
09:00 UTC on 2026-10-21. PIC is op-1. We stop if the lookout sees traffic in the box.

## 1. Situation

Notional harbour box at the simulator's default origin; launch at its south-west corner.
Water current is not measured. Other harbour users are possible.

## 2. Mission

The crew rehearses, in simulation, a 7-lane survey of the box to check track keeping, the
monitor's alerts and the lost-link response, between 09:00 and 09:40 UTC.

## 3. Execution

| Phase | Lead | Steps | Notes |
|-------|------|-------|-------|
| Setup | MC | P-1 | 14 waypoints, fence 260 m x 180 m |
| Preflight | PIC | P-2 to P-4 | Card in `harbour-survey-sim-preflight-card.md` |
| Launch | PIC | P-5, P-6 | Arm on PIC consent only |
| Survey | MC | P-7 to P-10 | Lanes east-west, 20 m apart, 1.5 m/s; VO calls each lane end |
| Recovery | MC, PIC | P-11, P-12 | RTL at last lane end, disarm at launch |

## 4. Contingencies

| Trigger | Threshold | First action | Who acts |
|---------|-----------|--------------|----------|
| Lost link | Alert 2 s, hold 10 s, RTL 60 s | Vehicle holds; PIC decides resume | Flight controller, then PIC |
| Low battery | 30 % | Vehicle returns to launch | Flight controller |
| Geofence | Box plus 30 m | Vehicle returns to launch | Flight controller |
| GPS loss | Fewer than 6 satellites or no 3D fix | Vehicle holds | Flight controller |
| Traffic in the box | VO sighting | PIC calls "abort" | PIC |

## 5. Comms

One voice net. Only the PIC says "go", "hold", "abort" and "resume". VO: "lane end" with the
number; "traffic" with a bearing. DL reads back each lane-end call.

## 6. Questions

