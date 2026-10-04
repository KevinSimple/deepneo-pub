# MDPI *Information* submission pack

Public, citable record of the submission-stage pack for the MDPI *Information* manuscript:

> **Efficient Protein Language Models for Peptide–MHC Ranking: A Leakage-Aware Evaluation Protocol under Multiplicity Control**
> Special Issue *Emerging Trends in Machine Learning and Natural Language Processing*
> Kevin Wang (first author) · Parma Nand (corresponding author)
> Audit date: 2026-10-04

This folder contains the **compliance reports, peer-review audits, and evidence files** that back every quantitative claim in the manuscript. The manuscript source, annotated review drafts, cover letter, and internal process notes stay in the private working repository; this folder is the public, auditable record.

---

## Contents

```
mdpi_submission/
├── README.md                               (this file)
├── compliance/                             formal compliance reports
│   ├── MDPI_SUBMISSION_COMPLIANCE_REPORT_2026-10-04.pdf
│   └── ACADEMIC_CONTENT_CLAIMS_COMPLIANCE_REPORT_2026-10-04.pdf
├── reviews/                                parallel peer-review audits
│   ├── review_deepneo_information_2026-10-04.md
│   └── journal_panel_2026-10-04/           5-seat journal panel
│       ├── 00_field_analysis.md
│       ├── editorial_decision.md
│       ├── review_EIC_journal_fit.md
│       ├── review_R1_methodology.md
│       ├── review_R2_domain.md
│       ├── review_R3_perspective.md
│       ├── review_DA.md
│       └── PARMA_TONE_AND_MDPI_FIT_2026-10-04.md
└── evidence/                               machine-readable evidence
    ├── CLAIM_EVIDENCE_TABLE.md             manuscript claim → SI file map
    └── supplementary_data/                 17 JSON ledgers
```

---

## Compliance reports (`compliance/`)

Two independent compliance audits, each PDF-rendered:

**1. Structural compliance** — `MDPI_SUBMISSION_COMPLIANCE_REPORT_2026-10-04.pdf`
Checks every binding requirement published on MDPI *Information*'s [Instructions for Authors](https://www.mdpi.com/journal/information/instructions): abstract word cap, keyword count, IMRaD structure, back-matter sections (CRediT, Funding, IRB, Consent, DAS, Acknowledgments, COI including Guest-Editor recusal), figure/table captions, reference graph, SI scope alignment. **Verdict: 18/19 PASS, 1 MINOR (free-format bib-order waiver).**

**2. Academic content & claims integrity** — `ACADEMIC_CONTENT_CLAIMS_COMPLIANCE_REPORT_2026-10-04.pdf`
Checks every directly verifiable content item against [MDPI Research & Publication Ethics](https://www.mdpi.com/ethics), [COPE Core Practices](https://publicationethics.org/core-practices), and the ML-evaluation-integrity literature the paper itself cites (Kapoor 2023, Bernett 2024, Joeres 2025). **Verdict: PASS on directly verifiable items; 515/515 numeric claims trace to committed SI JSONs; zero MISMATCH / UNSOURCED / withdrawn-headline leak.** Four external checks (iThenticate, independent reproducibility, in-body AI statement, code-availability sentence) are honestly flagged as recommended-but-not-asserted-PASS.

---

## Peer-review audits (`reviews/`)

Two independent AI-mediated review passes, both run on 2026-10-04 against the same manuscript file:

**PAT review** — `review_deepneo_information_2026-10-04.md`
Segmented deep review using the `paper-reviewer` skill (reimplementation of Google's Paper Assistant Tool architecture). 6 HIGH findings on editorial content; numbers verified clean against SI JSON ledgers.

**5-seat journal panel** — `journal_panel_2026-10-04/`
Simulated 5-seat journal review using the `academic-paper-reviewer` skill: Journal-Fit Editor, Methodology Reviewer, Domain Reviewer, Perspective Reviewer, Devil's Advocate. `editorial_decision.md` records the panel decision (Major Revision, 4/4 seats) with revision roadmap.

Both reviews converge on the same four editorial recommendations (Hashemi 2023 citation, live-URL alignment, Discussion claim calibration, title adjective "Efficient"). These are editorial-stage items that normally get addressed in a first revision round; none is a research-integrity or compliance failing.

---

## Evidence (`evidence/`)

**`CLAIM_EVIDENCE_TABLE.md`** maps every numeric claim in the manuscript to a specific JSON file in `supplementary_data/`. The 2026-09-03 full audit recorded **515/515 claims MATCH**; the 2026-10-04 re-audit confirmed zero MISMATCH / UNSOURCED / withdrawn-headline leak.

**`supplementary_data/`** contains 17 machine-readable JSON ledgers covering:
- Table 1 AUROCs, Wilcoxon, Holm-adjusted p-values, allele-clustered bootstrap CIs (v4.1 and v4.2)
- TransPHLA decontamination counts + fusion-fixed scores
- Weekly ranking (BA + EL) across 46 human-allele weeks, 14 ranking-eligible predictors
- Per-reference Wilcoxon on IEDB weekly
- Pool 2014–2026 head-to-head
- Author-constructed IEDB BA holdout + NetMHCpan-4.2 overlap (Case A)
- Pocket rescorer transductive-vs-inductive diagnostics (Case B)
- Ablation ladder on TransPHLA EL
- Per-figure provenance

Every number in the body text and in Table 1 traces to one of these files.

---

## What is deliberately NOT in this folder

- Manuscript source (`.tex`) — stays in the private working repo during review
- Annotated reviewer-response drafts (`.docx`) — internal supervisor correspondence
- Email drafts and cover letter — internal
- Internal process notes and brainstorming (abstract tone variants, draft CHANGELOGs) — internal
- Model weights and training code — never released pre-publication (see `../MODEL_CARD.md` and `../README.md` for the project-wide release policy)

---

## Reproducing the audits

- Compliance report (structural + academic) — compile from the LaTeX sources in the private working repo; identical content is produced here as PDF.
- Numeric claim verification — the private working repo ships eight audit scripts (`_claim_evidence_audit.py`, `_pass7_audit.py`, `_traceability_audit.py`, `_arithmetic_audit.py`, `_directional_audit.py`, `_structure_audit.py`, `_figure_audit.py`, `_doi_validate.py`) that re-derive the 515-claim verdict from the JSON ledgers in `evidence/supplementary_data/`. An independent re-run is a recommended external check (`compliance/ACADEMIC_CONTENT_CLAIMS_COMPLIANCE_REPORT_2026-10-04.pdf` §4).

---

*This folder was published to the public repo on 2026-10-04 as part of the submission-readiness pack. See the top-level `README.md` for the project-wide model card and benchmark context.*
