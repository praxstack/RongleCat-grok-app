# 01: Planner in front of Host import

**What to build:** Given Account recent-session rows, decide which CLI agent ids are safe to import, skip junk and already-linked ids, and call Host import for the rest without inventing ids. A single failure must not stop the rest.

**Blocked by:** None (can start immediately).

**Status:** done (commit d696313c)

- [x] Invalid ids (empty, path separators, `..`) never reach Host
- [x] Already-linked ids are skipped
- [x] Duplicates in the table import once
- [x] One failure leaves other ids still attempted
- [x] Unit tests cover the planner without Host I/O
