# 07: Real Grok App QA, then PR

**What to build:** Prove the feature in a running Grok App built from `feat/cli-session-import-from-account` (not only unit tests, not the App Store build). Capture logs and screenshots of Account Import listed and the sidebar CTA. Then open a PR to RongleCat/grok-app from this fork. Do not attach skill-setup files to that PR.

**Blocked by:** 01, 02, 03, 04, 05

**Status:** ready-for-agent

- [ ] `pnpm typecheck`, `pnpm test`, `cargo test` green on this branch
- [ ] `pnpm dev` (or an equivalent build of this commit) shows Import listed on Account → Recent sessions
- [ ] Clicking Import listed creates sidebar chats from real `~/.grok/sessions`
- [ ] Screenshots + console/log excerpt stored with the review
- [ ] PR body uses the repo template; links the fork tickets; no `docs/agents` / `CLAUDE.md` gstack dump
