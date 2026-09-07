# references/ai-act-annex-iv.md
# EU AI Act, Annex IV: Technical Documentation (Article 11(1))
# Certanix Alpha reference file · v1 · June 2026

## Purpose of this file

This file is the single source of truth for the Annex IV clauses that the Alpha
evidence pack maps to. The mapping functions in `certanix/evidence/ai_act_mapping.py`
MUST take their clause IDs, scope and wording cues from here, never from memory.
If a clause letter ever needs correcting, correct it HERE first, then the code.

Official text: Regulation (EU) 2024/1689 (the AI Act), Annex IV, Official Journal
of 13 June 2024. Verify wording against EUR-Lex (CELEX 32024R1689) or
https://artificialintelligenceact.eu/annex/4/ before any investor or notified-body
conversation. The summaries below are working paraphrases for engineering use,
not the legal text.

## Numbering caution (why this file exists)

Annex IV has 9 points. Point 2 letters in the FINAL act differ from some earlier
drafts. In Regulation (EU) 2024/1689:

- 2(d) covers the data requirements: datasheets describing training methodologies
  and techniques and the training data sets used, including their provenance,
  scope and main characteristics, how the data was obtained and selected,
  labelling procedures and data-cleaning methodologies.
- 2(e) covers the assessment of human oversight measures (Article 14).
- 2(g) covers the validation and testing procedures: data used, metrics for
  accuracy, robustness and compliance, test logs, and dated, signed test reports.

The Alpha maps three clusters: 1(a)-(c), 2(d) and 2(g). It does NOT map 2(e)
in the Alpha. Function names in code must therefore be:
`map_clause_1abc`, `map_clause_2d`, `map_clause_2g`.

<a id="clause-1abc"></a>
## Cluster 1: Annex IV point 1(a), 1(b), 1(c): general description of the AI system

What the regulation asks for (paraphrase):
- 1(a): the system's intended purpose, the provider's name, the version and how
  the version relates to previous versions.
- 1(b): how the AI system interacts with, or can be used to interact with,
  hardware or software, including other AI systems, where applicable.
- 1(c): the versions of relevant software or firmware, and any requirements
  related to version updates.

What the Alpha supplies:
- From the uploaded device manifest: system identity, declared intended purpose,
  platform/firmware versions, interface declarations.
- From the compiled twin: the hardware/software interaction model actually used
  in simulation.

LIMITATIONS to state honestly in the pack:
- The general description is derived from the manifest the customer declares;
  the Alpha does not independently verify firmware versions on physical hardware.

<a id="clause-2d"></a>
## Cluster 2: Annex IV point 2(d): data and datasheets

What the regulation asks for (paraphrase):
- Datasheets describing the training methodologies and techniques and the
  training data sets used: provenance, scope and main characteristics of the
  data, how it was obtained and selected, labelling procedures and data-cleaning
  methodologies.

What the Alpha supplies:
- A scenario datasheet for the synthetic campaign: generation method (quantum-
  optimised diversity selection plus the benchmarked classical fallback),
  scenario distribution and coverage statistics, selection criteria, seeds and
  provenance (including the Pasqal job ID when live hardware is used).

LIMITATIONS to state honestly in the pack:
- Alpha campaigns use synthetic scenarios only. A real OEM training-data audit
  (provenance, labelling, cleaning of the customer's own datasets) is MVP scope,
  not Alpha scope. Say so in exactly these terms.

<a id="clause-2g"></a>
## Cluster 3: Annex IV point 2(g): validation and testing

What the regulation asks for (paraphrase):
- The validation and testing procedures used, including information about the
  validation and testing data and its main characteristics; metrics used to
  measure accuracy, robustness and compliance with other relevant requirements;
  test logs and all test reports, dated and signed by the responsible persons.

What the Alpha supplies:
- Per-scenario telemetry and pass/fail results, campaign-level metrics, SHAP
  attribution records, the full machine-readable test log, and the
  cryptographically signed evidence pack (YubiHSM-backed signature standing in
  for the dated, signed test report).

LIMITATIONS to state honestly in the pack:
- Alpha metrics cover behavioural pass/fail and robustness under the simulated
  scenario set; cybersecurity testing and accuracy-in-the-field metrics are out
  of Alpha scope.
- The signature attests pack integrity and origin; it is pre-certification
  evidence prepared for a notified body or authority. Certanix does not certify.

## One-line doctrine for every mapping function

Every returned dict carries: `clause`, `clause_text_ref`, `platform_response`,
`evidence_artifacts` (type plus content_id), and `limitations`.

`clause_text_ref` format (canonical, stable): a dict with two keys:
  - `file`: "references/ai-act-annex-iv.md#clause-1abc" (or #clause-2d, #clause-2g);
    these explicit anchors are defined above each cluster heading and never change,
    even if heading wording changes. Anchor names match the mapping function names.
  - `legal`: "Regulation (EU) 2024/1689 (CELEX 32024R1689), Annex IV, point 1(a)-(c)"
    (resp. 2(d), 2(g)),
    so the reference stays meaningful outside the repository, in a printed or
    exported evidence pack. The honesty of `limitations` is what
protects the document's credibility under technical scrutiny. Never let it be
empty.
