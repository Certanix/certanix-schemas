# Changelog

Every published file with its sha256 at publication — the **immutability ledger**, read
back by `tools/build_schemas_repo.py --check`, which refuses to rebuild any path whose
bytes would change. A digest that moves means a file was edited, which is forbidden for
everything but additive context terms; the correct response to needing different bytes is
a new path, never a new digest at an old one.

Newest first.

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
