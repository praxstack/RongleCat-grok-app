# Agent notes (gstack)

Product agent notes live in **AGENTS.md**. Read that first, then `docs/llm-wiki/`.

## gstack (recommended)

This project uses [gstack](https://github.com/garrytan/gstack) for AI-assisted workflows.
Install it for the best experience:

```bash
git clone --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && ./setup --team
```

On this machine the install is also at `~/.grok/skills/gstack` and `~/.agents/skills/gstack`.

Skills like /qa, /ship, /review, /investigate, and /browse become available after install.
Use /browse for web pages. Grok App itself is a Tauri desktop app: drive it with `pnpm dev` (or the installed `/Applications/Grok.app` only when you are testing a released build, not a branch).

## Skill routing

When the user's request matches an available skill, invoke it. When in doubt, invoke the skill.

- Product ideas/brainstorming → /office-hours
- Strategy/scope → /plan-ceo-review
- Architecture → /plan-eng-review
- Design system/plan review → /design-consultation or /plan-design-review
- Full review pipeline → /autoplan
- Bugs/errors → /investigate
- QA/testing site or app behavior → /qa or /qa-only (Tauri: real window, not only unit tests)
- Code review/diff check → /review and `/code-review`
- Visual polish → /design-review
- Ship/deploy/PR → /ship
- Save progress → /context-save
- Resume context → /context-restore
- Author a backlog-ready spec/issue → /spec plus `/to-spec` / `/to-tickets`

## Agent skills

### Issue tracker

GitHub issues on the praxstack fork, mirrored as markdown under `.scratch/<feature>/issues/`. See `docs/agents/issue-tracker.md`.

### Triage labels

Matt Pocock roles map onto this repo's labels (`triage`, `ready-for-agent`, plus `enhancement`/`bug`/`priority:p*`/`area:*`). See `docs/agents/triage-labels.md`.

### Domain docs

Single-context. Glossary starts in this file and `docs/llm-wiki/`. See `docs/agents/domain.md`.

## Testing

- `pnpm typecheck`
- `pnpm test`
- `pnpm build:ui`
- `cd src-tauri && cargo test`

See CONTRIBUTING.md. Do not run `npm install` at the repo root.
