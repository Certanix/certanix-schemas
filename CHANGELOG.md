# Changelog

Every published file with its sha256 at publication — the **immutability ledger**, read
back by `tools/build_schemas_repo.py --check`, which refuses to rebuild any path whose
bytes would change. A digest that moves means a file was edited, which is forbidden for
everything but additive context terms; the correct response to needing different bytes is
a new path, never a new digest at an old one.

Newest first.

## 2026-09-30: manifest/v1/device-manifest-1.1.schema.json, v1/pack-1.11.schema.json, v1/evidence-context.jsonld (additive)

| File | sha256 |
|---|---|
| `manifest/v1/device-manifest-1.1.schema.json` | `c198fd743c6368bb4aef15c3a806a9c21ba59faa53aecf09919db64694aa6d39` |
| `v1/evidence-context.jsonld` | `834d32075cb24ecb00b8d098c0d16097b585273bb87bef38161b96e74e357faa` |
| `v1/pack-1.11.schema.json` | `6f5a6343d6449607564a6ecfbadf9bc7927929ce80e6f7ab8ae267ac6d63baba` |

## 2026-09-30: v1/pack-1.10.schema.json, v1/evidence-context.jsonld (additive)

| File | sha256 |
|---|---|
| `v1/evidence-context.jsonld` | `b277285c61b3258408fb20debfcb62c31913a2f280fd2ec340ec3246c0a30853` |
| `v1/pack-1.10.schema.json` | `047957f25548ea52789dd2b7b34dfeb601c9b090132b4776d414796149002c6a` |

## 2026-09-24: v1/pack-1.9.schema.json, v1/evidence-context.jsonld (additive)

| File | sha256 |
|---|---|
| `v1/evidence-context.jsonld` | `05447b96fafedfadc9e5c16a96395500d01a5209bda770903b2bcdc45e69da71` |
| `v1/pack-1.9.schema.json` | `65c66d992faf20b09656afbc9382189092c7457c0ef873d22bfbe5845fdb9397` |

## 2026-09-15 — v1/pack-1.8.schema.json, v1/evidence-context.jsonld (additive)

| File | sha256 |
|---|---|
| `v1/evidence-context.jsonld` | `ba601c6f7fff74dee01c54399bba6f24c67beba157217d372c85bbe0a2340cd5` |
| `v1/pack-1.8.schema.json` | `8225d03c0aedd6cdb850727014d97540457ca4313a3c48c7c9d4ba52cbff6b42` |

## 2026-09-07 — .nojekyll, CNAME

| File | sha256 |
|---|---|
| `.nojekyll` | `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855` |
| `CNAME` | `6cb3a1ddabfe5f60f583941752d2db03274dfd61c4afe3aad313631ff7362be4` |

## 2026-09-07 — first publication

Pack schemas `1.2`, `1.6`, `1.7`; the `delta-report`, `delta-refusal` and `self-evidence`
`1.0` roots; the evidence context at the path the signed packs name; the device-manifest
schema the authoring kit already mints.

| File | sha256 |
|---|---|
| `manifest/v1/device-manifest.schema.json` | `93ffd1da02a9d917caa5fab09fe50a80ea83b76579160e0f1a54a0ddb1747a26` |
| `v1/delta-refusal-1.0.schema.json` | `4dcb66fdeb2006b6aeebd3a79f88c7d22f7a7a819bcecb934f8d6d6af92e4bc6` |
| `v1/delta-report-1.0.schema.json` | `9c7e5cf9aeb2eab3f9a004588e7075c435178b5a63472e1f248a0151886a8145` |
| `v1/evidence-context.jsonld` | `e82026e79cc0ad6fe7baf720ba2b4ef7461d36ac09399b33b12e6e827004322b` |
| `v1/pack-1.2.schema.json` | `b02315b9047eacd0988eb494cf630fa817a8d8acad57005784c91f85d9f40d22` |
| `v1/pack-1.6.schema.json` | `1fe2a64165dc70c2ae11a0c8df613016477ebb38679a624705c6843d8d0a7270` |
| `v1/pack-1.7.schema.json` | `02a027e3f9b876f6db8b658ae210790871466d607c08f7cb34545be5ed06fc45` |
| `v1/self-evidence-1.0.schema.json` | `d3880e9d602ef8c4d56bc263242438b74518f5da47acbaa0eb21346485212be7` |
