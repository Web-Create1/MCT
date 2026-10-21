# Design Language

Rules every ops surface in the four repos follows. Rules, not files: each repo keeps its own
tokens in its own home (listed at the bottom), because the drone site forbids shared
stylesheets and Flight Eye forbids dependencies.

## 1. Status hierarchy

Four levels, always as colour plus glyph plus word. Colour alone is never the signal.

| Level | Word | Glyph | Meaning |
|-------|------|-------|---------|
| Nominal | `OK` | filled circle | Measured and inside limits |
| Advisory | `ADVISORY` | ring | Worth knowing, no action |
| Caution | `CAUTION` | triangle | Act soon, a contingency may follow |
| Warning | `WARNING` | octagon | Act now, or a failsafe is already acting |

Plus one state that is not a level: **Not measured**, a dashed outline and the words "not
measured". It is never green and never grey-as-OK.

## 2. Staleness

Every live or replayed reading shows its age. Past twice its expected interval it dims and
says "stale, N s". Past five times it is replaced by "not measured since HH:MM:SS".

## 3. Telemetry tile

```
┌──────────────────────┐
│ BATTERY        [OK]  │  label, status word
│ 15.8 V   74 %        │  value + unit, tabular numerals
│ 1.2 s ago            │  age
└──────────────────────┘
```

Value and unit are never split across lines. Numbers use tabular figures so a changing value
does not jitter. Minimum tile 44 px tall.

## 4. Console layout

Phone first, designed at 390 by 844.

```
Phone (stacked)                     Wide (three columns)
┌───────────────────────┐           ┌──────────┬───────────────┬──────────┐
│ PROVENANCE BANNER     │           │ PROVENANCE BANNER                    │
├───────────────────────┤           ├──────────┬───────────────┬──────────┤
│ track (SVG)           │           │ timeline │ track (SVG)   │ tiles    │
├───────────────────────┤           │ events   │               │          │
│ tiles, 2 across       │           │ anomalies│ scrubber      │ preflight│
├───────────────────────┤           └──────────┴───────────────┴──────────┘
│ scrubber              │
├───────────────────────┤
│ events and anomalies  │
└───────────────────────┘
```

The provenance banner (contract C6) is the first thing on screen and does not scroll away on
wide layouts.

## 5. Documents

Briefs, CONOPS, test plans, debriefs and quick-reference cards share one skeleton: title line,
provenance line, a one-paragraph bottom line up front, then numbered sections. Quick-reference
cards fit one printed page: trigger, first three actions, who to tell, what to log.

## 6. Diagrams

Inline SVG, labelled, readable at 390 px wide, light and dark. A hardware diagram says which
pin is pin 1 (drone repo convention).

## 7. Copy

No em dashes. Every number carries its unit. Sentence case. A state that is missing data says
which data and why, using Flight Eye's three absences as the model: not published, no record,
lookup failed.

## Where each repo keeps its tokens

| Repo | Token home |
|------|-----------|
| AI-Drone-Project | Inline `:root` variables in each `web/*.html`; copy from the nearest existing page |
| Flight-Eye | `public/lib/palette.mjs` (`STATUS`, reserved ramps) |
| C51SR-T | `docs/prd/design-system-v3.md` and `app/globals.css` |
| MCT | Markdown only; no tokens |
