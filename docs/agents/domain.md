# Domain docs

How the engineering skills should consume this repo's domain documentation.

## Before exploring, read these

- **`AGENTS.md`** at the repo root (this project's agent notes; there is no `CONTEXT.md` yet).
- **`docs/llm-wiki/`** — product rules. For sessions and account: `session-continuity.md`, `session-api.md`, `account.md`.
- **`docs/adr/`**: read ADRs that touch the area you're about to work in. If the directory is missing, proceed silently.

`/domain-modeling` creates `CONTEXT.md` lazily when terms actually get resolved. Do not invent a glossary up front.

## File structure

Single-context repo:

```
/
├── AGENTS.md
├── docs/llm-wiki/
├── docs/adr/          ← create when a decision needs an ADR
└── src/
```

## Use the project's vocabulary

When your output names a domain concept, use the term as this repo already uses it. Do not drift to synonyms.

| Term | Meaning |
|------|---------|
| Grok App session | Journal under `{app_data}/sessions/<id>/`. Sidebar chat. |
| Grok Build CLI agent session | Folder under `{GROK_HOME}/sessions/<encoded-cwd>/<agentSessionId>/`. |
| Call log | Settings → Account → Recent sessions. Usage rows. `CallLogEntry.id` is the CLI agent folder name. |
| `cli_session_import` | Host command. Copies `chat_history.jsonl` into an App journal. Idempotent if already linked. |
| Shared `session_data_mode` | `GROK_HOME=~/.grok`. Default. App must not rewrite `~/.grok` config. |
| Untrusted project | App project with `trust=false`. Import may add one for a CLI cwd. Never home, `/`, or shallow paths. |

If a concept isn't in this table or `docs/llm-wiki/`, either reuse an existing term or note the gap for `/domain-modeling`.

## Flag ADR conflicts

If your output contradicts an existing ADR, surface it explicitly rather than silently overriding.
