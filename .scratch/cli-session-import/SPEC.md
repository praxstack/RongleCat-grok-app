# Spec: Import Grok Build CLI sessions from Account recent logs

Parent category: **enhancement**, `area:session`, `priority:p1`.
Second-account copy: **enhancement**, `area:auth`, `priority:p2` (maintain.md lists multi-account as P2). Do not build dual live `auth.json`.

Issue form: `.github/ISSUE_TEMPLATE/feature_request.yml` (`[Feature]:`).

## Problem Statement

A person who already talks to Grok Build in the terminal opens Grok App and sees an empty sidebar. Settings → Account → Recent sessions lists those CLI sessions as usage rows. There is no control there that turns a row into a sidebar chat. Settings → General → App → CLI sessions can import, but that screen is not where the list already is. Two SuperGrok logins (different MLIDs) are a separate, already-shipped Add account / switch flow. The App does not keep two live `auth.json` files at once.

## Solution

From Account → Recent sessions, import the listed CLI agent sessions into App journals using Host `cli_session_import`. Import & open a single row. If the sidebar is empty (or only the current unarchived chat) and call logs exist, show the same import on the sidebar. Import may add the CLI cwd as an untrusted App project. Never add `$HOME`, `/`, or shallow paths. Multi-account stays Add account then switch.

## User Stories

1. As a Grok Build CLI user, I want Account → Recent sessions to import listed rows into the sidebar, so I do not hunt for Settings → General → App → CLI sessions.
2. As a Grok Build CLI user, I want Import & open on one row, so I land in that chat.
3. As a Grok Build CLI user, I want Open on a row that is already linked, so I do not duplicate the journal.
4. As a Grok Build CLI user with an empty sidebar and local call logs, I want a sidebar control that imports those sessions, so the first-run App is not a blank column while Account already shows history.
5. As a Grok Build CLI user, I want import to copy `chat_history.jsonl` into an App journal, so the transcript is readable as App messages.
6. As a Grok Build CLI user, I want import to be idempotent when the agent session is already linked, so repeating Import listed does not clone chats.
7. As a Grok Build CLI user, I want invalid agent ids (paths, `..`, empty) skipped, so Host never receives a junk id.
8. As a Grok Build CLI user, I want a failed row not to abort the rest of the listed import.
9. As a Grok Build CLI user, I want the CLI cwd registered as an untrusted App project when it looks like a real project folder, so the next agent run has a project without auto-trusting my home directory.
10. As a Grok Build CLI user, I do not want `/`, `~/`, `/Users/me`, or `/Users/me/Developer` auto-added as projects.
11. As a Grok App user with two SuperGrok memberships, I want copy that points at Add account and switch, so I am not told the App can hold two live logins.
12. As a translator, I want every new string in all 15 catalogs with `en` as the key authority.
13. As a settings-search user, I want Account recent-session import discoverable in `settingsCatalog`.
14. As a maintainer, I want unit tests on the planner, CTA predicate, and auto-add path rules, so Host I/O is not required to prove the gates.

## Implementation Decisions

- Highest seam: pure planner `planCallLogImport` / `runCallLogImport` in front of existing Host `cli_session_import`. Do not invent agent ids.
- `CallLogEntry.id` is the CLI agent folder name. That is the import key.
- CTA: show when `callLogCount > 0` and unarchived App chats ≤ 1. Never invent CLI sessions when the count is 0.
- Auto-add project: `trust=false`, require ≥4 path segments, skip home and roots. Host no-ops missing directories.
- UI stays in Account panel + sidebar empty state. No `window.confirm`. Reuse existing buttons.
- Multi-account: copy only. No second concurrent `auth.json`.
- App.tsx freeze: hook + presentational component, not new App.tsx state blocks.
- i18n: `src/i18n/messages/<locale>/account.ts` and `sidebar.ts`, 15 locales in lockstep.

## Testing Decisions

- Test external behavior of the planner and predicates (invalid ids, duplicates, already-linked, CTA bounds, path skip list). Do not assert file paths of journals inside unit tests.
- Follow existing vitest style next to the module (`cliSessionCallLogImport.test.ts`).
- Host `cli_session_import` stays an integration/QA seam: run it in the real Grok App against this user's `~/.grok/sessions`.
- Do not weaken tests to pass.

## Out of Scope

- Dual live official logins / two `auth.json` at once.
- Importing grok.com cloud history (CLI does not expose it).
- Raising the CLI sessions cap of 50 on the General → App screen.
- Rewriting `~/.grok` in shared session_data_mode.
- Skill-pack files (`docs/agents`, `CLAUDE.md` gstack routing) in the product PR.

## Further Notes

CONTRIBUTING: fork, small diff, `pnpm typecheck` / `pnpm test` / `cargo test`, i18n through messages, no `window.confirm`, PR states motive + change + verification.

How this repo takes work: community files `[Feature]:` / `[Bug]:` with `enhancement` or `bug`, `priority:p*`, `area:*`, often `from:community`. Maintainers land a PR that closes the issue. Open issues at recon time: 0. Recent closed examples: #773–#782 (Windows chrome, updater confirm, scroll lock, tray glyph).

Assumptions (recorded):

- User's CLI sessions live under shared `~/.grok/sessions`.
- Recent sessions table is a call log, not an importer, until this change.
- SuperGrok second membership is solved by existing Add account / switch.

## EARS acceptance criteria

1. WHEN the user clicks Import listed on Account → Recent sessions, the system SHALL call Host `cli_session_import` once per importable, not-yet-linked agent id in the visible table.
2. WHEN a row id is empty, contains a path separator, or contains `..`, the system SHALL skip it and SHALL NOT pass it to Host.
3. WHEN an agent id is already linked, Import listed SHALL skip it; Open SHALL open the existing App chat.
4. WHEN one import call fails, the system SHALL continue the remaining ids and report how many failed.
5. WHEN unarchived App chats ≤ 1 AND call log count > 0, the sidebar SHALL offer Import from Grok Build.
6. WHEN call log count is 0, the sidebar SHALL NOT offer that import.
7. WHEN import runs for a CLI cwd with ≥4 path segments that is not home or `/`, the system SHALL add an untrusted App project if the directory exists.
8. WHEN the cwd is home, `/`, or shallower than 4 segments, the system SHALL NOT add a project.
9. WHEN new UI copy is added, all 15 locale catalogs SHALL define the same keys as `en`.
10. WHEN the product PR is opened, it SHALL NOT include gstack/pstack/Matt Pocock setup files.
