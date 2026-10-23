---
layout: page
title: Attestation public keys
permalink: /keys/
---

# Attestation public keys

Cairnwork attestations are DSSE envelopes signed with Ed25519 (see [docs/ATTESTATION.md](https://github.com/cairnwork/cairnwork/blob/main/docs/ATTESTATION.md)). Each signature carries a `keyid`, the SHA-256 of the raw 32-byte public key. The matching public key is served here at `/keys/<keyid>.pem`, so a verifier can fetch the key by the `keyid` it sees in a bundle and run `cairnwork-attest verify` or the [cairnwork/verify-action](https://github.com/cairnwork/verify-action) offline against it.

| keyid | holder | status |
|---|---|---|
| [`ab0d10a508d83c26f9fffc11bfb42bb956584310ce961c082b4e46d0a4f3b47a`](ab0d10a508d83c26f9fffc11bfb42bb956584310ce961c082b4e46d0a4f3b47a.pem) | demo-target end-to-end drill key (the key behind the `verify-action` fixture, demo-target PR #4) | demo only |

The demo key is a drill artefact: it proves the publishing and verification path, not the identity of a production attest host. No production signing key has been issued yet; when one is, its public key will be added here and the signing host, issue date and status will be listed in this table. A retired key stays published so that attestations signed with it remain verifiable.

Checking a key's `keyid` locally:

```sh
openssl pkey -pubin -in ab0d10a508d83c26f9fffc11bfb42bb956584310ce961c082b4e46d0a4f3b47a.pem -outform DER | tail -c 32 | shasum -a 256
```

Rotation: a new key is published here and added to the verifier configuration (`verify-action` accepts several PEM blocks) before the attest host switches to signing with it; the old key is marked retired, never removed.
