# 03 C5ISR-T Case Study

Add a `/drone-ops` page to the Projects tab of `Web-Create1/C51SR-T-framework-NIST-2.0` that
reads the drone stack through C5ISR-T, NIST CSF 2.0 and AAA, using the site's existing engine.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| C51SR-T | `README.md` | The route table, "Navigation", "Reading system" | How a page joins the site |
| C51SR-T | `docs/prd/drone-ops-case-study.md` | Full file | Requirements, content outline, PR plan |
| C51SR-T | `lib/site/nav.ts` | The Projects tab entry | Where the page is registered |
| C51SR-T | One existing project page, `app/offline-ai/page.tsx` | Structure only | The pattern to copy rather than invent |
| C51SR-T | `docs/prd/design-system-v3.md` | Token and component sections | Visual rules |
| This workspace | `../../references/integration.md` | C2, C3, C4 | Roles, authorization and link rules for the AAA section |
| This workspace | `../../references/honesty-rules.md` | Full file | The page describes a simulation-only project |

## Process

1. Read the Inputs. Run `npm run lint` and `npm run build` and confirm both pass before editing.
2. Work the PRD's PR plan: content data module, page and figures, nav entry, session note.
3. Every fact about the drone project is taken from its public site and dated. Link only to
   `https://ai-drone-project.vercel.app` routes, never to the private repo.
4. Check the page at 390 by 844 and at desktop width in both themes.
5. Add a dated note under `docs/sessions/`.

## Audit

| Check | Pass Condition |
|-------|---------------|
| Author guard | Every commit authored as `Web-Create1` with the noreply address |
| No private links | No `github.com/Web-Create1/AI-Drone-Project` or `Flight-Eye` in the diff |
| No employer | No employer name, product or branding on the page |
| Honesty | "Simulation" and "in progress" appear in the hero, per the honesty rules |
| Build | `npm run lint` and `npm run build` green |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Draft PRs | `Web-Create1/C51SR-T-framework-NIST-2.0` | One per PR-plan item |
| Stage report | `output/c5isr-case-study-report.md` | Written by the orchestrator |
