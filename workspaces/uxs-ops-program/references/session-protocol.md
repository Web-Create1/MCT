# Session Protocol

How a build session runs. Written to keep each session cheap and its PRs mergeable.

## Read budget

1. The target repo's `CLAUDE.md` loads by itself. Obey it.
2. Read the stage contract's Inputs rows, in order, and stop. Use the named section, not the file.
3. Find code with `grep -n` for a symbol, then read that range. Never sweep a directory.
4. Do not open research documents, generated pages, lockfiles or fixtures unless a row names them.
5. No subagents unless a single question needs more than ten files to answer.

## Branch and PR rules

- Start from branch `claude/lucid-franklin-xg3pn1`, which carries the repo PRD. Create one
  branch per PR from it, named `ops/<short-slug>`, `accounts/<short-slug>` and so on.
- One concern per PR. The PRD's "PR plan" is the order. Open each as a **draft** into `main`.
- Each PR body names the requirement IDs it closes and links the PRD PR it builds on.
- Before every push run the repo's own checks: drone `python -m pytest src -q` and
  `python scripts/check-conventions.py`; Flight Eye `npm test` and the em dash grep; C51SR-T
  `npm run lint` and `npm run build`; MCT none beyond a self-review.
- Never weaken a test, never skip one, never bypass a hook.

## Commit identity

Every commit in all four repos:

```
export GIT_AUTHOR_NAME="Web-Create1" GIT_COMMITTER_NAME="Web-Create1"
export GIT_AUTHOR_EMAIL="215433136+Web-Create1@users.noreply.github.com"
export GIT_COMMITTER_EMAIL="$GIT_AUTHOR_EMAIL"
```

Use the environment variables, not `git -c user.*`: cloud containers pre-set `GIT_AUTHOR_NAME`,
and an environment variable beats config.

C51SR-T's CI rejects any other author. The others do not enforce it, but one identity keeps the
contribution graph honest and publishes no inbox.

## When a requirement fights a house rule

The house rule wins. Write the conflict into the PR body in two lines (requirement, rule, what
was done instead) and move on.

## Handoff

Before ending, update the repo's own handoff file (drone `HANDOFF.md` and `ROADMAP.md`; Flight
Eye `CLAUDE.md` "Watch out for" if a new trap was found; C51SR-T `docs/sessions/`). Then end
your final message with a five-line report: PRs opened, requirement IDs closed, tests count
before and after, anything cut, anything blocked.
