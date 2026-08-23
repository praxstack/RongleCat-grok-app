# 03: Sidebar empty-state import

**What to build:** When the sidebar has no real history (zero or only the current unarchived chat) and Account already has local CLI call logs, show Import from Grok Build plus a way to open the Account list. Hide that offer when there are no call logs.

**Blocked by:** 01

**Status:** done (commit d696313c)

- [x] CTA appears only when callLogCount > 0 and unarchived chats ≤ 1
- [x] CTA hidden when callLogCount is 0
- [x] Import uses the same Host path as Account
- [x] No new App.tsx state block (hook + presentational component)
