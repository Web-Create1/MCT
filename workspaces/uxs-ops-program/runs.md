# Runs

Live register of build sessions. Per-run state, not reference: `status` still reads
`stages/*/output/`, and a stage is complete only when its report lands there.

| Stage | Session | Started | Base PR | State |
|-------|---------|---------|---------|-------|
| 01 drone sim ops | `session_01YSkxodJYmJpxTEW7C3tQL9` | 2026-10-21 | Web-Create1/AI-Drone-Project#64 | complete, #65 to #74 open, CI green; SITL run waits on Eric; report in stage output |
| 02 Flight Eye accounts | `session_017zc9Qx8YGeoHHbE9DhY47v` | 2026-10-21 | Web-Create1/Flight-Eye#78 | complete, #79 to #84 open, CI green; report in stage output |
| 03 C5ISR-T case study | `session_01PqZcd8sQBMu3vDyXUbLEbu` | 2026-10-21 | Web-Create1/C51SR-T-framework-NIST-2.0#32 | complete, #33 to #35 open, checks green; report in stage output |
| 04 mission docs workspace | `session_012iJBRHWcsMRYcf1KuCqXh7` | 2026-10-21 | Web-Create1/MCT#1 | complete, #2 to #5 open; report in stage output |
| 05 integration review | not started | | | waits on Eric merging the stage PRs |

Orchestrating session: `session_019vU4GSaCngnnRoYqasVNou`.
