# 05 Integration Review

Check the four builds as one program: every duty group covered, every public claim honest,
every cross-repo link live, every handoff file current.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Previous stages | `../01-drone-sim-ops/output/`, `../02-*/output/`, `../03-*/output/`, `../04-*/output/` | Full files | PR links and what shipped |
| This workspace | `../../references/role-map.md` | Full file | The table this stage closes out |
| This workspace | `../../references/honesty-rules.md` | Full file | The audit list |
| This workspace | `../../references/integration.md` | C4, C6 | Link and provenance rules |

## Process

1. For each stage report, confirm its PRs are merged. List any still open; do not review those.
2. For each role-map row, open the deliverable's public URL and set status to `shipped`,
   `planned` or `gap`. A row is `shipped` only if the URL loads and shows the artifact.
3. Audit each public page the program touched against `honesty-rules.md`. One finding per
   line: URL, rule, quote, fix.
4. Check every cross-repo link with `curl -s -o /dev/null -w '%{http_code}'`. Anything not 200
   is a finding.
5. Fix findings in the repo that owns them, one small PR each.
6. Write the review to output and update `role-map.md` statuses.

## Audit

| Check | Pass Condition |
|-------|---------------|
| Coverage | 9 of 9 duty groups `shipped`, or each gap has a reason |
| Honesty | Zero open findings |
| Links | Zero non-200 links |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Review | `output/program-review.md` | Coverage table, findings, fixes with PR links |
| Role map | `../../references/role-map.md` | Statuses updated in place |
