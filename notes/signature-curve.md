# A note on the signature curve in published pack schemas

The published evidence-pack schemas, versions 1.2 and 1.6 to 1.14, describe the signature as
ECDSA-P384. That text is wrong. The verifier enforces ECDSA P-256.

## What is true today

- The Certanix signing key published at `certanix.eu/verify/keys/certanix-hsm.pub` is a P-256 key.
- From version 0.17.0, `certanix-verify` accepts P-256 keys only. Any other curve, or a key that is
  not an EC key, is refused with exit code 1 (`USAGE`), which says nothing about the pack.
- Before 0.17.0, the verifier did not refuse a key on another curve.

## Where the wrong text is

Each of those schemas has it in the `Signature` definition: in the description, and as the default
value of `algorithm`. A schema does not sign or verify anything, so this text is not used to check
a signature. The verifier takes its rule from its own code.

## Why the schemas are not being edited

Published schemas are write-once. Someone may already rely on the exact bytes of a schema version,
so those files stay as they are, with the wrong text.

## Where the correction ships

In the next published pack schema version. The `certanix-verify` 0.17.0 README and changelog state
the difference in the meantime. No date is given here for the next schema version.

## What you need to do

Nothing changes for a pack signed with a P-256 key. If you read the curve from a schema, read P-256.
If you check Certanix packs with your own tooling, use P-256.
