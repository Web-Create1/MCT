# Runs

Live register of build sessions. Per-run state, not reference: `status` still reads
`stages/*/output/`, and a stage is complete only when its report lands there.

| Stage | Session | Started | Base PR | State |
|-------|---------|---------|---------|-------|
| 01 drone sim ops | `session_01YSkxodJYmJpxTEW7C3tQL9` | 2026-10-21 | Web-Create1/AI-Drone-Project#64 | running |
| 02 Flight Eye accounts | `session_017zc9Qx8YGeoHHbE9DhY47v` | 2026-10-21 | Web-Create1/Flight-Eye#78 | running |
| 03 C5ISR-T case study | `session_01PqZcd8sQBMu3vDyXUbLEbu` | 2026-10-21 | Web-Create1/C51SR-T-framework-NIST-2.0#32 | running |
| 04 mission docs workspace | `session_012iJBRHWcsMRYcf1KuCqXh7` | 2026-10-21 | Web-Create1/MCT#1 | running |
| 05 integration review | not started | | | waits on 01 to 04 merging |

Orchestrating session: `session_019vU4GSaCngnnRoYqasVNou`.
