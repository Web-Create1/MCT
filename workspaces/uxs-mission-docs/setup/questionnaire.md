# Onboarding Questionnaire

<!-- Agent instructions: Read this file when the user types "setup". Ask ALL questions
     in one conversational pass. Collect answers, replace the placeholders in the files
     named, then scan the workspace for remaining {{ patterns and ask for anything missing.
     Per-mission details (objective, area, window, crew) are collected by stage 01, not here. -->

### Q1: What name or callsign should documents use for you as author?
- Placeholder: `{{OPERATOR_NAME}}`
- Files: `CLAUDE.md`
- Type: free text
- Default: `operator`

### Q2: Which platform do you plan most missions for?
- Placeholder: `{{DEFAULT_PLATFORM}}`
- Files: `CLAUDE.md`
- Type: selection
- Options: copter, USV
- Default: copter

### Q3: Which unit system should documents use?
- Placeholder: `{{UNIT_SYSTEM}}`
- Files: `CLAUDE.md`
- Type: selection
- Options: metric (m, m/s, degrees true, volts, percent), aviation (ft, kt, nm, degrees true)
- Default: metric
- Derived: none. A document that converts shows both units, original first.

### Q4: Any house style notes for your organisation's documents?
- Placeholder: `{{STYLE_NOTES}}`
- Files: `CLAUDE.md`
- Type: free text, one or two example sentences that sound right
- Default: `none`
- Never ask for, or accept, an employer's controlled template. The outlines stay generic.

---

## After Onboarding

Tell the user the defaults are set in `CLAUDE.md` and that a mission starts at
`stages/01-intake/CONTEXT.md`. Then scan the workspace for remaining `{{` patterns.
