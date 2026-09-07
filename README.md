# certanix-schemas

The published schemas for Certanix signed evidence. **Generated**, never hand-written:
`tools/build_schemas_repo.py` in `certanix-beta` emits this tree from the platform's own
pydantic models and from the `OMIT_WHEN_EMPTY` additive-schema contract in
`certanix/verify_core.py`. `--check` fails a stale build.

## Offline verification does not fetch anything from here

**A Certanix pack verifies locally, with no network, and this repository is not on the
trust path.** The `@context` URI inside a pack is a *vocabulary lookup* for JSON-LD
consumers — it is not dereferenced when a signature is checked. `certanix-verify`, the
specimen `verify.py`, and the platform's own verifier all recompute the pack's canonical
bytes and check the signature against a public key. None of them opens a socket.

So: **a dead or unreachable link here does not mean a pack failed to verify.** It means a
vocabulary could not be fetched. Those are different failures and only one of them is
about trust.

## Status of `schema.certanix.eu`

At the time of publication the host **does not resolve**. Publishing this repository does
not change that: standing up `schema.certanix.eu` to serve `/v1/` is a separate operations
step, and it is **owed, not done**. Until it is served, the `@context` in every signed pack
is unresolvable — which, per the section above, is a broken vocabulary link and not a
broken signature.

**When it is served, two things are binding.** The path must be *exactly*
`https://schema.certanix.eu/v1/evidence-context.jsonld` — that string is frozen inside the signed bytes of every pack
that exists and cannot be changed for any of them. And what is served there must be
**immutable** thereafter: additive edits to the context only, never a removal or a
redefinition, because a removed term silently changes the meaning of every pack ever
signed.

## What is published, and what is deliberately not

Pack schema versions `1.2`, `1.6` and `1.7`, plus the two standalone `1.0` roots — the four
versions that a live signed artifact actually references. The verifier knows nine values
(`None`, `1.0`–`1.7`); the rest are not published, because writing a schema for a pack
version that no artifact uses would be inventing a record.

This is also the schema-migration answer in the form a certification body asks for it: *the
pack you accepted last year still validates, here is the schema it validates against, and
that file has not changed since the day it was published.*

## Files

| File | sha256 |
|---|---|
| `manifest/v1/device-manifest.schema.json` | `93ffd1da02a9d917…` |
| `v1/delta-refusal-1.0.schema.json` | `4dcb66fdeb2006b6…` |
| `v1/delta-report-1.0.schema.json` | `9c7e5cf9aeb2eab3…` |
| `v1/evidence-context.jsonld` | `e82026e79cc0ad6f…` |
| `v1/pack-1.2.schema.json` | `b02315b9047eacd0…` |
| `v1/pack-1.6.schema.json` | `1fe2a64165dc70c2…` |
| `v1/pack-1.7.schema.json` | `02a027e3f9b876f6…` |
| `v1/self-evidence-1.0.schema.json` | `d3880e9d602ef8c4…` |

## Immutability

A published file is **never edited**. A correction is a new version. The one exception is
`v1/evidence-context.jsonld`, which is **additive only** for the reason given above.

---
Internal — Certanix. Structural validity only: a document that satisfies a schema here is
well-shaped, not signed, not verified, and not gate-admitted.
