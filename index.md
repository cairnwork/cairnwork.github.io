---
title: Cairnwork
---

# Cairnwork

A delivery verification layer for AI coding agents. Not an agent, not a PR reviewer.

An agent fixes a small bug in an isolated clone. The tests that judge the fix are withheld from the agent, applied afterwards, and run by a sandboxed verifier under a dedicated OS account. An independent notary service records the verdict. Only a `VERIFIED` verdict opens a draft pull request.

**Status:** pilot (2026-10-20 → 2026-11-16). Apache-2.0. Python ≥ 3.11. macOS sandbox today, Linux in progress.

We publish only measured or drilled results. There are no effect numbers yet; a preregistered A/B evaluation is in progress.

## Try it in five minutes

```sh
uv tool install --from git+https://github.com/James3014/cairnwork.git cairnwork
cairnwork demo
```

`cairnwork demo` needs no GitHub, no AI worker and no API key: it builds a throwaway project with a seeded bug, applies a ready-made one-line fix as the candidate, and runs it through the governed verification until the notary records `VERIFIED`. Full steps: [docs/QUICKSTART.md](https://github.com/James3014/cairnwork/blob/main/docs/QUICKSTART.md).

No `curl | sh` on the main path. If you do not have `uv`, a readable fallback script is published here; read it and check the digest before running it:

- [install.sh](install.sh) — sha256 `6699d02f8e933c068ef43b7375f8c928c230bfa9a72231f165dc827407437355` ([install.sh.sha256](install.sh.sha256))

- Source: <https://github.com/James3014/cairnwork>
- Security policy: <https://github.com/James3014/cairnwork/blob/main/SECURITY.md>
