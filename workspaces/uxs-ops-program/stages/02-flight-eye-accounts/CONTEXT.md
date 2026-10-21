# 02 Flight Eye Accounts

Add optional passkey accounts to `Web-Create1/Flight-Eye` so saved flights, preferences and
alert settings follow the owner between devices, with zero new dependencies.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Flight Eye | `CLAUDE.md` | "House rules", "The rule that matters most" (auto-loaded) | Zero dependencies, mobile first, no em dashes |
| Flight Eye | `docs/PRD-ACCOUNTS.md` | Full file once, then only the A-section for the current PR | Requirements, acceptance criteria, PR plan |
| Flight Eye | `api/lib/kv.js`, `api/lib/config.js` | `grep -n` for `export function` | The Upstash REST store and env reading to reuse |
| Flight Eye | `api/subscribe.js` | Top-of-file comment and the handler | The existing pattern for a write endpoint |
| Flight Eye | `public/lib/starred.mjs`, `prefs.mjs` | Exported functions only | What gets synced, and the validation it must pass |
| Flight Eye | `public/sw.js` | The precache list | Every new `public/lib` module must be added |
| This workspace | `../../references/design-language.md` | Sections 1, 2 and 7 | Account states and copy |

## Process

1. Read the Inputs. Run `npm test` and record the count.
2. Work the PRD's PR plan in order: crypto core, endpoints, sync, interface, docs.
3. For the crypto core, write the tests first using keys generated in the test with
   `node:crypto`, so no fixture can drift from the code that verifies it.
4. Run `npm test` on Node 20 and 22 if both are available, and the em dash grep, before each push.
5. In the last PR, add the new traps to `CLAUDE.md` "Watch out for" and a `docs/ACCOUNTS.md`
   that states exactly what is stored.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 2, before the interface PR | Where the account control sits on the 390 px layout | Placement |

## Audit

| Check | Pass Condition |
|-------|---------------|
| Zero dependencies | `package.json` has no `dependencies` key added |
| Signed out is unchanged | Every existing test passes untouched; nothing is gated behind sign-in |
| Verification is real | Tests reject a wrong origin, a wrong rpId, a reused challenge, a bad signature and a lower sign count |
| No KV, no crash | With KV unset the account control says accounts are unavailable and why |
| Function budget | `api/` stays at or under the Vercel Hobby function limit |
| Precache | `test/sw.test.mjs` passes |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Draft PRs | `Web-Create1/Flight-Eye` | One per PR-plan item |
| Stage report | `output/flight-eye-accounts-report.md` | Written by the orchestrator |
