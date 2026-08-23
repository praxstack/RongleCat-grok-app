# Triage labels

The skills speak in five canonical triage roles. This file maps those roles to labels.

This fork uses **both** Matt Pocock's five roles **and** Grok App's maintain vocabulary (`docs/llm-wiki/maintain.md`). Apply both sets when creating GitHub issues.

| Label in mattpocock/skills | Label in our tracker | Meaning |
|----------------------------|----------------------|---------|
| `needs-triage` | `triage` | Maintainer needs to evaluate this issue (repo already uses `triage`) |
| `needs-info` | `needs-info` | Waiting on reporter for more information |
| `ready-for-agent` | `ready-for-agent` | Fully specified, ready for an AFK agent |
| `ready-for-human` | `ready-for-human` | Requires human implementation |
| `wontfix` | `wontfix` | Will not be actioned |

## Extra labels this repo already uses

| Label | Use |
|-------|-----|
| `bug` / `enhancement` / `documentation` | Type (GitHub issue forms set `bug` or `enhancement`) |
| `priority:p0` | Blocks core usage (login, send, stuck UI, data loss) |
| `priority:p1` | Major UX / platform breakage |
| `priority:p2` | Polish, nice-to-have, backlog |
| `area:session` | Streaming, history, permissions, agent connect |
| `area:auth` | OAuth / account / quota |
| `area:composer` | Input, paste, attachments |
| `area:i18n` | Locale strings |
| `platform:macos` / `platform:windows` | OS-specific |
| `from:community` | X / Discord / external report |
| `good first issue` | Small, well-scoped for newcomers |

Issue title prefix from the forms: `[Feature]:` or `[Bug]:`.
