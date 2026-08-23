# Issue tracker: GitHub (fork) + local markdown mirror

Issues and specs for **this fork** live in two places. Skills that "publish to the issue tracker" write **both**.

1. **GitHub (working tracker):** `praxstack/RongleCat-grok-app` via `gh`.
2. **Local markdown (always):** `.scratch/<feature>/issues/<NN>-<slug>.md`.

Upstream product intake (what CONTRIBUTING.md tells contributors) is still **RongleCat/grok-app**. A fork ticket is a working copy. The PR that lands the work targets `RongleCat/grok-app` and links the fork issue.

## Conventions

- **Create (GitHub):** `gh issue create --repo praxstack/RongleCat-grok-app --title "..." --body-file ...`
- **Create (markdown):** one file per ticket under `.scratch/<feature>/issues/`, numbered from `01`.
- **Read:** `gh issue view <number> --repo praxstack/RongleCat-grok-app --comments`, and the matching markdown file.
- **List:** `gh issue list --repo praxstack/RongleCat-grok-app --state open`
- **Labels:** apply Matt Pocock triage labels from `docs/agents/triage-labels.md` **and** this repo's maintain vocabulary (`enhancement` / `bug`, `priority:p0|p1|p2`, `area:*`). See `docs/llm-wiki/maintain.md`.

If `gh` is unauthenticated, write the markdown files and a `ship.sh` that creates the GitHub issues. Do not pretend GitHub issues exist.

## Pull requests as a triage surface

**PRs as a request surface: no.**

PRs are how work lands, not how new requests enter the queue. Feature requests and bugs use the issue forms in `.github/ISSUE_TEMPLATE/`.

## When a skill says "publish to the issue tracker"

Write the markdown ticket, then `gh issue create` on `praxstack/RongleCat-grok-app`. Use RongleCat/grok-app only when opening the public counterpart for a PR into upstream.

## When a skill says "fetch the relevant ticket"

Read `.scratch/<feature>/issues/` first (works offline). Then `gh issue view` if GitHub is reachable.
