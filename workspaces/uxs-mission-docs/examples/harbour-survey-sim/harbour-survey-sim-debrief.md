# Debrief: Harbour Survey (Simulated USV)

Provenance: Simulation | driver: none, illustrative hand-written log, not from a simulator run | scenario: harbour-survey-sim, seed: none | run date: 2026-10-21 | drone repo commit: none

**BLUF.** The log records a complete simulated survey in 1286.0 s (seq 29). The vehicle left
its lane by 6.2 m against a 5.0 m limit (seq 10), the lost-link hold came 10.0 s after the
loss (seq 17, 19), and the envelope refused 3.0 m/s (seq 15). The input log is illustrative,
hand-written, not from a simulator run: every number below shows the method, not a result.

## 1. Log

- File: `harbour-survey-sim-ops-log.jsonl`, mission `20261021-harbour-survey-sim-7c41`.
- 30 lines, `seq` 0 to 29; the `end` line's `lines` is 30, which matches.
- `seq` 0 driver: "illustrative, hand-written, not from a simulator run"; seed, ArduPilot
  version and git commit are null.
- `verify-log` was not run. The `prev` hashes were computed when the log was written; this
  stage does not check them. The chain is tamper-evident, not tamper-proof.

## 2. Timeline

| t_s | seq | Kind | What happened |
|-----|-----|------|---------------|
| 1.2 | 1 | plan | Plan loaded by MC: 14 waypoints |
| 20.0 to 50.0 | 2 to 6 | preflight | Battery, GPS, geofence pass; harbour clear confirmed; water current not measured |
| 60.0 | 7 | cmd | Arm, by PIC, acked |
| 62.0 | 8 | cmd | AUTO, by MC, acked |
| 245.0 | 11 | anomaly | Cross-track caution, 6.4 m against 5.0 m |
| 250.0 | 12 | note | DL: "lookout reports vehicle set north of lane 2" |
| 330.0 | 14, 15 | cmd, refusal | MC asked 3.0 m/s; refused, rule `max_speed` |
| 603.0 | 18 | anomaly | Link loss warning, 3.0 s against 2.0 s |
| 610.0 | 19 | contingency | Lost link: HOLD, by the flight controller |
| 640.0 | 21 | cmd | AUTO, by PIC, acked (resume) |
| 760.0 | 23 | discrepancy | Step P-9: 6 of 7 lane-end reports |
| 1110.0 | 26 | cmd | RTL, by MC, acked |
| 1285.0 | 28 | cmd | Disarm, by PIC, acked |
| 1286.0 | 29 | end | Outcome complete, duration 1286.0 s |

## 3. Anomalies

| Rule | Sev | Value | Threshold | Last in-limit | Onset | Anomaly | TTD |
|------|-----|-------|-----------|---------------|-------|---------|-----|
| xtrack | caution | 6.4 m | 5.0 m | seq 9, 120.0 s | seq 10, 240.0 s | seq 11, 245.0 s | 245.0 s - 240.0 s = 5.0 s, lower bound |
| link_loss | warning | 3.0 s | 2.0 s | seq 16, 480.0 s | seq 17, 600.0 s | seq 18, 603.0 s | 603.0 s - 600.0 s = 3.0 s, lower bound |

Telemetry in this log is sparse (gaps up to 220.0 s, seq 25 to 27), so each true onset lies between the last
in-limit sample and the onset sample. The link-loss anomaly's own value of 3.0 s agrees with
an onset at 600.0 s; the cross-track onset could be as early as 120.0 s.

## 4. Refusals

| Command | Rule | Reason | seq |
|---------|------|--------|-----|
| set_speed 3.0 m/s | max_speed | 3.0 m/s exceeds envelope max 2.0 m/s | 14, 15 |

## 5. Contingencies

Lost link at 600.0 s (seq 17). The flight controller held at 610.0 s (seq 19). Link was back
by 625.0 s (seq 20, mode HOLD). The PIC resumed AUTO at 640.0 s (seq 21), 40.0 s after the
loss, so the 60 s RTL threshold was not reached. No other contingency appears in the log.

## 6. Discrepancies

| Step | Expected | Observed | seq |
|------|----------|----------|-----|
| P-9 | VO report at each of 7 lane ends | 6 reports; lane 4 end missed during link loss | 23 |

## 7. Metrics

| Measure | Value | seq |
|---------|-------|-----|
| Duration | 1286.0 s | 29 |
| Largest cross-track error sampled in AUTO | 6.2 m (`tlm`); 6.4 m (anomaly value) | 10, 11 |
| Loss onset to hold | 610.0 s - 600.0 s = 10.0 s | 17, 19 |
| Battery charge | Not measured at 720.0 s. Measured: 93 % (9), 88 % (10), 85 % (13), 77 % (16), 71 % (17), 69 % (20), 58 % (24), 52 % (25), 49 % (27) | 22 |
| Battery voltage at 720.0 s | 15.3 V | 22 |

Battery percentage was not measured at 720.0 s (seq 22), so no minimum battery is reported.
Cross-track error was not measured during RTL (seq 27); RTL is outside O2.

## 8. Objectives

| Objective | Result | Evidence |
|-----------|--------|----------|
| O1 All lanes | Not met | Outcome complete (seq 29), but 6 of 7 lane-end reports (seq 23) |
| O2 Cross-track within 5.0 m | Not met | 6.2 m at seq 10 |
| O3 TTD within 10 s | Not measurable | Lower bounds 5.0 s and 3.0 s; the cross-track gap of 120.0 s (seq 9 to 10) is wider than 10 s |
| O4 Hold within 10 s, PIC resume | Met | 10.0 s (seq 17, 19); resume by PIC op-1 (seq 21) |
| O5 Speed refusal | Met | seq 14, 15 |
| O6 Battery at or above 30 % | Not measurable | `batt_pct` null at seq 22 |

## 9. Findings

- F1. Cross-track error reached 6.2 m on lane 2, above the 5.0 m limit (seq 10, 11), with a
  crew note of the vehicle set north (seq 12). Water current was not measured (seq 6).
- F2. The cross-track detection time cannot be judged against 10 s: the samples either side
  of the onset are 120.0 s apart (seq 9, 10).
- F3. The lost-link hold came exactly at the 10 s threshold (seq 17, 19); resume was the
  PIC's (seq 21).
- F4. The envelope refused a 3.0 m/s request (seq 14, 15).
- F5. One lane-end report was missed while the link was lost (seq 23).
- F6. Battery percentage has a gap at 720.0 s (seq 22); the low-battery objective cannot be
  confirmed for the whole run.

## 10. Lessons learned (operator)

not yet written
