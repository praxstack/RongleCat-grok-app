# 04: Untrusted project auto-add for CLI cwd

**What to build:** After a CLI session import, if the session cwd looks like a real project folder, add it as an untrusted App project. Never add home, `/`, Windows drive roots, or shallow paths like `/Users/name`. Missing directories are a no-op. Trust stays false.

**Blocked by:** 01

**Status:** done (commit d696313c)

- [x] Host skips home, `/`, and paths with fewer than 4 segments
- [x] Added projects are untrusted
- [x] TypeScript mirror of the rule is unit-tested
