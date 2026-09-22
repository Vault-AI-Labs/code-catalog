# VaultAI Code — signed model catalog

This repository is the publish point for VaultAI Code's signed model catalog ("door 1").
The app fetches these three files over HTTPS and verifies the Ed25519 signature of
`catalog.yaml` under `key.pub` before using it:

- `key.pub` — the catalog-signing public key (raw Ed25519 public key, base64, one line)
- `catalog.yaml` — the model catalog (schema v2; top-level `updated:` is the display date)
- `catalog.sig` — the Ed25519 signature over the exact `catalog.yaml` bytes (base64, one line)

The signing private key never enters this repository. Key rotation publishes a new
`key.pub` together with `key.prev.sig` (a signature by the previous key over the new key's
bytes); installed apps accept a new key only with that proof.

Publishing procedure and design: `max-code-lab/Documentation/Door-1-Signed-Catalog.md`
(private).
