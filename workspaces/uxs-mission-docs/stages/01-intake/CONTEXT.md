# 01 Intake

Turns the user's description of a mission into a one-page mission request every later stage reads.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| User | The conversation | The mission they describe | The only source of mission facts |
| Workspace | `../../CLAUDE.md` | "Workspace Defaults" | Default platform and unit system |
| Reference | `../../references/crew-and-units.md` | "Roles" and "Units" | Role codes and how numbers are written |

## Process

1. Ask, in one message, for whatever is missing: objective, platform, area (shape and size),
   window (date, start, length), crew by role, speed and endurance limits, contingency
   thresholds (lost link, low battery, geofence, GPS loss), and constraints.
2. Offer the defaults for platform and units; never invent a number the user did not give.
   A missing number is written `not given` and listed under open questions.
3. Pick a slug: lowercase-with-hyphens, ending `-sim` for a simulated run.
4. Write the request with the sections objective, platform, area, window, crew, limits,
   contingency thresholds, constraints, open questions.
5. Run the Audit, then save.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 4 | The draft request | Whether every fact and number is right before stage 02 builds on it |

## Audit

| Check | Pass Condition |
|-------|---------------|
| Sourced | Every number came from the user or a stated default, with a unit |
| Roles | Every crew entry uses a code from `crew-and-units.md` and names a PIC |
| Skeleton | Title, provenance line, BLUF, numbered sections |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Mission request | `output/<slug>-mission-request.md` | One page of markdown |
