# 02: Account Recent sessions import actions

**What to build:** On Settings → Account → Recent sessions, the user can Import listed (visible table), Import & open one row, or Open a row that is already a sidebar chat. Copy says these are Grok Build CLI sessions. No `window.confirm`.

**Blocked by:** 01

**Status:** done (commit d696313c)

- [x] Import listed uses the planner against the visible table
- [x] Import & open imports one row then opens that App chat
- [x] Open does not re-import a linked row
- [x] Strings go through i18n catalogs
