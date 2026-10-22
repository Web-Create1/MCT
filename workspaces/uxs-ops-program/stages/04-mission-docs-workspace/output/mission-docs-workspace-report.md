# Stage 04 Report: Mission Docs Workspace

**Session:** `session_012iJBRHWcsMRYcf1KuCqXh7` · **Finished:** 2026-10-21 · **State:** draft PRs open, awaiting review

## PRs

| PR | Closes | What |
|----|--------|------|
| Web-Create1/MCT#2 | M1, M5 | Scaffold, six stage contracts (40 to 43 lines, 4 files or fewer each), questionnaire |
| Web-Create1/MCT#3 | M2, M3, M8 | Generic outlines, risk matrix, roles and units, log reading guide, glossary |
| Web-Create1/MCT#4 | M4, M6 | `examples/harbour-survey-sim/`: all six documents and a 30-line hand-written C1 log |
| Web-Create1/MCT#5 | M7 | Root routing, README entry, `status` example |

Stacked: #2 on #1, each later PR on the one before. Merge in order.

## Deviations from the contract

- The shared document rules (skeleton, provenance line, simulation wording) live in the
  workspace `CLAUDE.md`, which is always loaded, instead of a reference file, because a separate
  file pushed stages 03 and 06 past the 4-file budget. They are still out of every CONTEXT.md.
- The log reading guide first had time to detect backwards. With sparse telemetry it is a lower
  bound, not an upper one. Fixed on #3, and #4 carries the fix.
- The workspace was assembled from the stage contract rather than through workspace-builder,
  then checked against workspace-builder's validation checklist: 11 of 13 pass, 2 not applicable.

## Cut or deferred

- M9, the corrective-action stage (P2).
- The example log is hand-written and labelled so. Replace it with a real drone scenario log
  once the drone stage's `/ops` PR merges, and run `verify-log` on it then.
