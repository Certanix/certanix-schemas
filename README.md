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
consumers; it is not dereferenced when a signature is checked. `certanix-verify`, the
specimen `verify.py`, and the platform's own verifier all recompute the pack's canonical
bytes and check the signature against a public key. None of them opens a socket.

So: **a dead or unreachable link here does not mean a pack failed to verify.** It means a
vocabulary could not be fetched. Those are different failures and only one of them is
about trust. This host being up is a convenience for readers, never a dependency of the
proof.

## Versions are immutable, and the `/vN` scheme is how change happens

Every published path is **write-once**. `v1/` holds the vocabulary and the schema shapes
as published; those bytes never change again. A correction is therefore not an edit: it
is a **new path**, a new `pack-1.14`, or a whole new `v2/` prefix minted alongside, with
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

Pack schema versions `1.2`, `1.6`, `1.7` and `1.11` are the versions current signed
artifacts reference; `1.10` is referenced only by superseded signed artifacts, which stay
published and still verify. Pack `1.13` is also published, because it is the version the
platform emits from this release, so its schema describes real output rather than
inventing a record. No artifact signed under the Certanix root declares `1.13` yet;
test-signed specimens, which are not evidence, may. The standalone roots
`delta-refusal-1.0`, `delta-report-1.0`, `embodied-trace-1.0`,
`parameter-coverage-map-1.0` and `self-evidence-1.0` are published beside them. Packs
`1.8`, `1.9` and `1.12` stayed published after the platform moved past them: each was
published while current, and published bytes are write-once, so a superseded version is
never withdrawn. The verifier knows fifteen values (`None`, `1.0`, `1.1`, `1.2`, `1.3`,
`1.4`, `1.5`, `1.6`, `1.7`, `1.8`, `1.9`, `1.10`, `1.11`, `1.12`, `1.13`); the rest are
not published, because writing a schema for a pack version that no artifact uses would be
inventing a record. The device manifest has two published revisions:
`manifest/v1/device-manifest.schema.json`, frozen, and
`manifest/v1/device-manifest-1.1.schema.json`, which adds the optional fields
`arm_length_m`, `drive_type`, `inertia_kg_m2`, `rotor_layout`, `rotor_max_speed_rad_s`,
`rotor_max_thrust_n`, `rotor_torque_ratio_m` and `vehicle_data`. The frozen v1 schema
still validates every manifest that declares none of them, and rejects one that does,
since its layers are closed. The six rotorcraft fields (`arm_length_m`, `inertia_kg_m2`,
`rotor_layout`, `rotor_max_speed_rad_s`, `rotor_max_thrust_n`, `rotor_torque_ratio_m`) are
accepted and recorded; the simulation does not use them until the parametric airframe is
released, and each pack's `twin_fidelity` record states what was simulated.

This is also the schema-migration answer in the form a certification body asks for it:
*the pack you accepted last year still validates, here is the schema it validates against,
and that file has not changed since the day it was published.*

## What is served

| File | URL | sha256 |
|---|---|---|
| `manifest/v1/device-manifest-1.1.schema.json` | https://schema.certanix.eu/manifest/v1/device-manifest-1.1.schema.json | `c198fd743c6368bb…` |
| `manifest/v1/device-manifest.schema.json` | https://schema.certanix.eu/manifest/v1/device-manifest.schema.json | `93ffd1da02a9d917…` |
| `v1/delta-refusal-1.0.schema.json` | https://schema.certanix.eu/v1/delta-refusal-1.0.schema.json | `4dcb66fdeb2006b6…` |
| `v1/delta-report-1.0.schema.json` | https://schema.certanix.eu/v1/delta-report-1.0.schema.json | `9c7e5cf9aeb2eab3…` |
| `v1/embodied-trace-1.0.schema.json` | https://schema.certanix.eu/v1/embodied-trace-1.0.schema.json | `0d8782076a67c849…` |
| `v1/evidence-context.jsonld` | https://schema.certanix.eu/v1/evidence-context.jsonld | `d1d06c6b0fd0c438…` |
| `v1/pack-1.10.schema.json` | https://schema.certanix.eu/v1/pack-1.10.schema.json | `047957f25548ea52…` |
| `v1/pack-1.11.schema.json` | https://schema.certanix.eu/v1/pack-1.11.schema.json | `6f5a6343d6449607…` |
| `v1/pack-1.12.schema.json` | https://schema.certanix.eu/v1/pack-1.12.schema.json | `06ef89887becb818…` |
| `v1/pack-1.13.schema.json` | https://schema.certanix.eu/v1/pack-1.13.schema.json | `798f7bd852457400…` |
| `v1/pack-1.2.schema.json` | https://schema.certanix.eu/v1/pack-1.2.schema.json | `b02315b9047eacd0…` |
| `v1/pack-1.6.schema.json` | https://schema.certanix.eu/v1/pack-1.6.schema.json | `1fe2a64165dc70c2…` |
| `v1/pack-1.7.schema.json` | https://schema.certanix.eu/v1/pack-1.7.schema.json | `02a027e3f9b876f6…` |
| `v1/pack-1.8.schema.json` | https://schema.certanix.eu/v1/pack-1.8.schema.json | `8225d03c0aedd6cd…` |
| `v1/pack-1.9.schema.json` | https://schema.certanix.eu/v1/pack-1.9.schema.json | `65c66d992faf20b0…` |
| `v1/parameter-coverage-map-1.0.schema.json` | https://schema.certanix.eu/v1/parameter-coverage-map-1.0.schema.json | `c1d62919040978ac…` |
| `v1/self-evidence-1.0.schema.json` | https://schema.certanix.eu/v1/self-evidence-1.0.schema.json | `d3880e9d602ef8c4…` |

Two more files sit at the root and are hosting, not schema. `CNAME` is what makes the site
answer on `schema.certanix.eu` (the host named in every pack's signed bytes), and it is
frozen for a stronger reason than any schema is: a schema path can be superseded, a
hostname already inside signed bytes cannot. `.nojekyll` disables Jekyll so the tree is
served verbatim; nothing here starts with an underscore today, and the file is here so
that the day something does, a URI frozen in signed bytes does not begin returning 404.

---
This tree is the published namespace referenced inside the signed bytes of Certanix
evidence packs. Structural validity only: a document that satisfies a schema here is
well-shaped, not signed, not verified, and not gate-admitted.
