# UxS Mission Docs

Turns a mission request for an uncrewed system (UxS) into a CONOPS, a test plan, a brief with a
preflight card, a debrief from the ops log, and quick-reference cards, one stage per document.

## Folder Map

```
uxs-mission-docs/
├── CLAUDE.md                     (you are here)
├── CONTEXT.md                    (start here for task routing)
├── setup/questionnaire.md        (one-time onboarding)
├── references/                   (outlines, rules and guides the stages load)
├── examples/
│   └── harbour-survey-sim/       (one complete simulated run, every stage's output)
└── stages/
    ├── 01-intake/                (request -> one-page mission request)
    ├── 02-conops/                (request -> concept of operations)
    ├── 03-test-plan/             (request + CONOPS -> test plan with risks)
    ├── 04-brief-and-preflight/   (CONOPS + test plan -> brief and preflight card)
    ├── 05-debrief/               (test plan + ops log -> debrief with findings)
    └── 06-training-qrc/          (brief + debrief -> one card per contingency)
```

## Triggers

| Keyword | Action |
|---------|--------|
| `setup` | Run `setup/questionnaire.md` |
| `status` | Scan `stages/*/output/` and render the pipeline, as `_core/CONVENTIONS.md` describes |

### `status` example

With stages 01 to 03 run for a mission slugged `pier-check-sim`:

```
Pipeline Status: uxs-mission-docs

  [01-intake] --> [02-conops] --> [03-test-plan] --> [04-brief-and-preflight] --> [05-debrief] --> [06-training-qrc]
   COMPLETE        COMPLETE        COMPLETE           PENDING                      PENDING          PENDING
   (pier-check-sim-mission-request.md)
                   (pier-check-sim-conops.md)
                                   (pier-check-sim-test-plan.md)
```

## Routing

| Task | Go To |
|------|-------|
| Start a new mission's documents | `stages/01-intake/CONTEXT.md` |
| Any later document | `CONTEXT.md`, then the stage it names |
| See what a finished run looks like | `examples/harbour-survey-sim/` |
| Look up a term | `references/glossary.md` |

## What to Load

| Task | Load These | Do NOT Load |
|------|-----------|-------------|
| Any stage | That stage's `CONTEXT.md` and only the rows of its Inputs table | Other stages' references, the example run, the glossary |
| Studying the method | `examples/harbour-survey-sim/README.md`, then one document | All the example documents at once |

## Workspace Defaults

- Operator: {{OPERATOR_NAME}}
- Default platform: {{DEFAULT_PLATFORM}}
- Unit system: {{UNIT_SYSTEM}}
- House style notes: {{STYLE_NOTES}}

## Rules for Every Document

1. Skeleton: title line, provenance line, a one-paragraph bottom line up front (BLUF), then
   numbered sections. A quick-reference card fits one printed page.
2. Provenance line, near the top: `Provenance: Simulation | driver | scenario and seed | run
   date | drone repo commit`. Every document here is for simulation or training, so it says
   Simulation. A field that does not exist yet reads `none`.
3. Simulated work "ran in simulation", was "rehearsed" or "simulated". Never "operated",
   "flew", "piloted" or "deployed". The ops log is tamper-evident, never "secure" or
   "tamper-proof".
4. Every number carries its unit and traces to the mission request, the plan, or a log line
   (`seq`). A `null` in the log is "not measured", never zero.
5. Lessons learned are written by a person. A generated document says "not yet written".
6. Outlines are generic and public. No employer names, no controlled or proprietary formats.
7. No em dashes.

## Stage Handoffs

Each stage writes to its own `output/` folder and the next stage reads from there. Edit an
output and the next stage picks up your edit. Outputs are git-ignored; a run worth keeping is
copied to `examples/<slug>/`.
