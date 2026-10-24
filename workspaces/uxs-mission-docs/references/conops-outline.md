# CONOPS Outline

A concept of operations says what a mission is for and how the crew will run it, before any
detail of how it is tested. This outline is generic: purpose, concept, phases, roles. It does not
follow any organisation's controlled format.

## Sections

Title line, provenance line, then a BLUF paragraph: mission, platform, area, window, and the one
thing that would stop it. Then these numbered sections:

1. **Purpose.** Why the mission exists and what a good outcome lets someone do next.
2. **Concept.** The whole mission in one paragraph: vehicle, pattern, speed, area, duration.
3. **Phases.** A table: phase, entry condition, activity, exit condition, lead role.
   Typical phases: setup, preflight, launch, transit, task, recovery, post-mission.
4. **Roles.** A table: role code, person or `notional`, duties per phase. Name the PIC.
5. **Comms plan.** Who talks to whom, on what, and the words for go, hold and abort.
6. **Environment.** Area limits, geofence, expected conditions, other users of the space.
7. **Contingencies.** For lost link, low battery, geofence breach and GPS loss: the threshold
   from the request and the planned response, with who acts (flight controller or operator).
8. **Risks.** A short list of what could go wrong. Scoring happens in the test plan.
9. **Open questions.** Copied from the request, still unanswered.

## Rules

- Numbers come from the mission request only. A number the request lacks is an open question.
- A phase without an exit condition is not a phase yet.
- Keep it to two printed pages. Detail belongs in the test plan.
