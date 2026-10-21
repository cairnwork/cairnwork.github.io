---
title: Cairnwork
---

# Cairnwork

A delivery verification layer for AI coding agents. Not an agent, not a PR reviewer.

An agent fixes a small bug in an isolated clone. The tests that judge the fix are withheld from the agent, applied afterwards, and run by a sandboxed verifier under a dedicated OS account. An independent notary service records the verdict. Only a `VERIFIED` verdict opens a draft pull request.

**Status:** pilot (2026-10-20 → 2026-11-16). Apache-2.0. Python ≥ 3.11. macOS sandbox today, Linux in progress.

We publish only measured or drilled results. There are no effect numbers yet; a preregistered A/B evaluation is in progress.

- Source: <https://github.com/James3014/cairnwork>
- Security policy: <https://github.com/James3014/cairnwork/blob/main/SECURITY.md>
