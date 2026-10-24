# Brief and Preflight Card Outline

A mission brief is read aloud to the crew before the run. The order is the generic five
paragraph shape: situation, mission, execution, contingencies, comms.

## Brief Sections

Title line, provenance line, BLUF: mission in one sentence, go time, PIC. Then:

1. **Situation.** Area, conditions, other users, anything changed since the CONOPS.
2. **Mission.** One sentence: who does what, where, when, and why.
3. **Execution.** Phases in order with their lead role, the procedure step range for each,
   speed and pattern.
4. **Contingencies.** A table: trigger, threshold with unit, first action, who acts.
   Copied from the test plan, never retyped from memory.
5. **Comms.** Who calls go, hold and abort, and the exact words.
6. **Questions.** Left blank for the crew.

Keep it to one printed page, two at most.

## Preflight Card

One printed page. Title line and provenance line, then one table:

| # | Check | Owner | Method | Pass value |
|---|-------|-------|--------|------------|

- Method is `auto` when the system logs it as a `preflight` line, `manual` when a person
  confirms it aloud and the logger records it.
- The last line is always the PIC's arming consent.
- A check with no pass value is not a check. A check the system cannot measure says
  `not-measured` as an allowed result and names who decides.
