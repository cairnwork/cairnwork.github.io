---
title: Cairnwork
---

# Cairnwork

Cairnwork is an execution gate for AI coding agents. A change counts as complete only after passing deferred tests applied after the worker has finished, run in an isolated sandbox, with an offline-verifiable signed attestation. Evidence of completion, not a higher success rate.

Whether the worker could have seen those tests depends on the configured `test_source`: with `bundle` (strict) the tests live only in a private store, a task is refused if its bundle was not imported, and there is no fallback to the repository, so "the worker never saw the tests" holds. The default `auto` is a compatibility and demo mode that falls back to a public branch of the target repository and makes no confidentiality claim. The attestation records which mode was used (`test_source`, also printed by `cairnwork-attest verify --json`).

A verified run's notary record can be turned into an in-toto DSSE Ed25519 signed attestation (`cairnwork-attest statement --sign`) that binds the verdict to the exact candidate commit. Anyone can verify it offline with `cairnwork-attest verify` using only the public key and the local git objects (see [docs/ATTESTATION.md](https://github.com/cairnwork/cairnwork/blob/main/docs/ATTESTATION.md)), or check it on pull requests with the [cairnwork/verify-action](https://github.com/cairnwork/verify-action) GitHub Action (the bundle travels in git notes under `refs/notes/cairnwork`; the action needs `contents: read` only and is pinned by commit).

**Status:** pilot (2026-10-20 → 2026-11-16). Apache-2.0. Python ≥ 3.11. macOS (Seatbelt) and Linux (bubblewrap) sandboxes, each with a dedicated verifier account; signed attestation and offline verification available; install and demo verified on macOS, Ubuntu CI and Debian 13. The worker and the verifier still run on the same host; a worker-only account is tracked in cairnwork#19.

We publish only measured or drilled results. The first preregistered A/B (N=28) was a tie: 12/28 adoptable in both arms, the filter never acted ([2026-10-22-ab-run2](https://github.com/cairnwork/cairnwork/blob/main/docs/results/2026-10-22-ab-run2.md)). The deferred-acceptance detector blocked 5 of 7 real wrong patches (too few to conclude), 205/205 rule-based mutants, and falsely blocked 0 of 83 real correct patches ([2026-10-22-filter-mechanism](https://github.com/cairnwork/cairnwork/blob/main/docs/results/2026-10-22-filter-mechanism.md)).

**What it does not claim:** a higher model success rate (strong models rarely fail on small bugs); a replacement for human code review; being an interactive coding agent or assistant; defect-free code after a pass (an independently reviewed case, Nexus-new#2813 fixed by PR #2856, was VERIFIED and its refusal check could still be bypassed; verification is evidence, not proof).

## Try it in five minutes

```sh
uv tool install --from git+https://github.com/cairnwork/cairnwork.git cairnwork
cairnwork demo
```

`cairnwork demo` needs no GitHub, no AI worker and no API key: it builds a throwaway project with a seeded bug, applies a ready-made one-line fix as the candidate, and runs it through the governed verification until the notary records `VERIFIED`. If `cairnwork` is not found right after installing, open a new shell or run `export PATH="$HOME/.local/bin:$PATH"`. Full steps: [docs/QUICKSTART.md](https://github.com/cairnwork/cairnwork/blob/main/docs/QUICKSTART.md).

No `curl | sh` on the main path. If you do not have `uv`, a readable fallback script is published here; read it and check the digest before running it:

- [install.sh](install.sh) — sha256 `52b7bcd146bf5864d05844571cdb85fa59a82e6cbe58b6dfa016c81085dda673` ([install.sh.sha256](install.sh.sha256))

- Source: <https://github.com/cairnwork/cairnwork>
- Security policy: <https://github.com/cairnwork/cairnwork/blob/main/SECURITY.md>
