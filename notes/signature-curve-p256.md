# A note on the signature curve in pack schemas, revised

This note replaces `notes/signature-curve.md`, published on 5 November 2026, which stays
served as it was published.

The published evidence-pack schemas, versions 1.2 and 1.6 to 1.14, describe the signature as
ECDSA-P384. That text is wrong. The verifier enforces ECDSA P-256. Pack schema 1.15 describes
the signature as ECDSA P-256.

## What is true today

- Both Certanix signing keys, the software key retired on 4 September 2026 and the current HSM key, are P-256.
- The Certanix signing key published at `certanix.eu/verify/keys/certanix-hsm.pub` is a P-256 key.
- From version 0.17.0, `certanix-verify` accepts P-256 keys only. Any other curve, or a key that is
  not an EC key, is refused with exit code 1 (`USAGE`), which says nothing about the pack.
- Before 0.17.0, the verifier did not refuse a key on another curve.

## Where the wrong text is

Each of the schemas 1.2 and 1.6 to 1.14 has it in the `Signature` definition: in the
description, and as the default value of `algorithm`. A schema does not sign or verify
anything, so this text is not used to check a signature. The verifier takes its rule from its
own code.

## Why those schemas are not being edited

Published schemas are write-once. Someone may already rely on the exact bytes of a schema
version, so those files stay as they are, with the wrong text.

## Where the correction ships

In pack schema 1.15, `v1/pack-1.15.schema.json`. Its `Signature` definition describes ECDSA
P-256 with SHA-256, and the default value of `algorithm` is `ECDSA-P256`. The schemas 1.2 and
1.6 to 1.14 keep their text.

## What you need to do

Nothing changes for a pack signed with a P-256 key. If you read the curve from a schema, read P-256.
If you check Certanix packs with your own tooling, use P-256.
