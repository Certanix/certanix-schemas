# certanix-schemas

**This repository is the canonical host for `https://schema.certanix.eu/`.** It is not a mirror and not a
copy: GitHub Pages serves this tree from `main` at the repository root, so a file at
`v1/evidence-context.jsonld` here *is* the URL `https://schema.certanix.eu/v1/evidence-context.jsonld`, and nothing else
decides that mapping. Moving, renaming or Jekyll-processing a file here changes what a
published URI returns.

The content is **generated**, never hand-written: `tools/build_schemas_repo.py` in
`certanix-beta` emits it from the platform's own pydantic models and from the
`OMIT_WHEN_EMPTY` additive-schema contract in `certanix/verify_core.py`. `--check` fails a
stale build, and *refuses* on any change to bytes that are already published.

## Offline verification does not fetch anything from here

**A Certanix pack verifies locally, with no network, and this repository is not on the
trust path.** The `@context` URI inside a pack is a *vocabulary lookup* for JSON-LD
consumers — it is not dereferenced when a signature is checked. `certanix-verify`, the
specimen `verify.py`, and the platform's own verifier all recompute the pack's canonical
bytes and check the signature against a public key. None of them opens a socket.

So: **a dead or unreachable link here does not mean a pack failed to verify.** It means a
vocabulary could not be fetched. Those are different failures and only one of them is
about trust. This host being up is a convenience for readers, never a dependency of the
proof.

## Versions are immutable, and the `/vN` scheme is how change happens

Every published path is **write-once**. `v1/` holds the vocabulary and the schema shapes
as published; those bytes never change again. A correction is therefore not an edit — it
is a **new path**, a new `pack-1.8`, or a whole new `v2/` prefix minted alongside, with
`v1/` left standing forever. That is the same sign-forward rule the evidence itself
follows: you do not amend a signed record, you sign a superseding one and keep both.

The reason is not tidiness. A pack signed today carries `https://schema.certanix.eu/v1/evidence-context.jsonld` *inside
its signed bytes*, and that string can never be changed for that pack. Edit the file at
that URL and every pack ever signed silently acquires a different vocabulary, with no
signature anywhere going invalid to announce it. Publication moves to meet the signed
bytes; the signed bytes never move.

The single exception is `v1/evidence-context.jsonld`, which is **additive only**: terms may be added,
never removed and never redefined. A term absent from a context is dropped from the
expanded graph and a term added later is simply available, so an addition cannot change
what an older pack means. The generator verifies this term by term against the published
file rather than trusting it, and refuses a removal or a redefinition.

Enforcement, so this is a mechanism and not a promise: the digests below are the ledger,
`--check` compares both the served tree and a fresh build against them, and `main` is
protected against force-push and deletion so history cannot be rewritten underneath a
published digest.

## What is published, and what is deliberately not

Pack schema versions `1.2`, `1.6` and `1.7`, plus the two standalone `1.0` roots — the
versions a live signed artifact actually references. The verifier knows nine values
(`None`, `1.0`–`1.7`); the rest are not published, because writing a schema for a pack
version that no artifact uses would be inventing a record.

This is also the schema-migration answer in the form a certification body asks for it:
*the pack you accepted last year still validates, here is the schema it validates against,
and that file has not changed since the day it was published.*

## What is served

| File | URL | sha256 |
|---|---|---|
| `manifest/v1/device-manifest.schema.json` | https://schema.certanix.eu/manifest/v1/device-manifest.schema.json | `93ffd1da02a9d917…` |
| `v1/delta-refusal-1.0.schema.json` | https://schema.certanix.eu/v1/delta-refusal-1.0.schema.json | `4dcb66fdeb2006b6…` |
| `v1/delta-report-1.0.schema.json` | https://schema.certanix.eu/v1/delta-report-1.0.schema.json | `9c7e5cf9aeb2eab3…` |
| `v1/evidence-context.jsonld` | https://schema.certanix.eu/v1/evidence-context.jsonld | `e82026e79cc0ad6f…` |
| `v1/pack-1.2.schema.json` | https://schema.certanix.eu/v1/pack-1.2.schema.json | `b02315b9047eacd0…` |
| `v1/pack-1.6.schema.json` | https://schema.certanix.eu/v1/pack-1.6.schema.json | `1fe2a64165dc70c2…` |
| `v1/pack-1.7.schema.json` | https://schema.certanix.eu/v1/pack-1.7.schema.json | `02a027e3f9b876f6…` |
| `v1/self-evidence-1.0.schema.json` | https://schema.certanix.eu/v1/self-evidence-1.0.schema.json | `d3880e9d602ef8c4…` |

Two more files sit at the root and are hosting, not schema. `CNAME` is what makes the site
answer on `schema.certanix.eu` — the host named in every pack's signed bytes — and it is
frozen for a stronger reason than any schema is: a schema path can be superseded, a
hostname already inside signed bytes cannot. `.nojekyll` disables Jekyll so the tree is
served verbatim; nothing here starts with an underscore today, and the file is here so
that the day something does, a URI frozen in signed bytes does not begin returning 404.

---
Internal — Certanix. Structural validity only: a document that satisfies a schema here is
well-shaped, not signed, not verified, and not gate-admitted.
