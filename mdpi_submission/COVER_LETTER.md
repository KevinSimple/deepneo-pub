# Cover letter — MDPI *Information* Special Issue

Parma Nand (corresponding author)
Kevin Wang (first author)
School of Design and Creative Technologies
Auckland University of Technology
55 Wellesley Street East, Auckland 1010, New Zealand

Corresponding author email: parma.nand@aut.ac.nz
First author email: kevin.wang.anz@hotmail.com

ORCID: Kevin Wang 0009-0007-0632-2261 · Parma Nand 0000-0001-6853-017X

Date: 2026-10-14

To the Editors,
*Information*
Special Issue: *Emerging Trends in Machine Learning and Natural Language Processing*

---

Dear Editors,

Please consider our research article,

> **"Efficient Protein Language Models for Peptide–MHC Ranking: A Leakage-Aware Evaluation Protocol under Multiplicity Control"**

for the Special Issue *Emerging Trends in Machine Learning and Natural Language Processing*.

**Fit to the Special Issue.** The manuscript studies a transformer-style **protein language model** (ESM2-35M) applied to a biomedical ranking task (peptide–MHC class I binding and presentation). It speaks directly to three themes in the SI call: **responsible evaluation** (predeclared leakage decontamination + Holm-adjusted multiplicity control), **efficiency** (a 35 M-parameter trunk trained on commodity GPUs, with no training-data advantage over the industrial comparator), and **domain adaptation** of language-model architectures outside English NLP. Healthcare is explicitly listed among the SI's application domains.

**What the paper contributes — stated honestly.** We decline to overclaim; three contributions are offered.

1. **A specific leakage ledger on a widely-used public benchmark.** Exact (peptide, HLA) decontamination of the TransPHLA holdout against NetMHCpan-4.1's training corpus removes **26.9% (43,509 of 161,652) of pairs**; all primary comparisons are reported on the clean subset (*n* = 118,143). This decontamination rate on this specific benchmark has not been previously published; future work using TransPHLA can cite the committed JSON ledger or reproduce the audit.
2. **A calibration advantage that practitioners can use.** On the TransPHLA EL set (*n* = 161,652; SI Figure S1), **expected calibration error is 0.091 for DeepNeo-CL EL versus 0.202 for NetMHCpan-4.1 EL** at 10-bin reliability — less than half the baseline's calibration error. (This measurement is reported on the full set and includes the 26.9% rows that would be removed under exact decontamination; a decontaminated re-measurement is noted as future work in the SI.) No pMHC-I predictor paper has previously reported calibration on this benchmark; the difference is directly actionable for any vaccine-design pipeline that thresholds predicted probabilities.
3. **A full-provenance evidence pack.** All 515 numeric claims in the manuscript trace to 17 committed Supplementary Data JSON ledgers (per-row and per-figure); two independent compliance audits (structural + content/claims) both PASS. This level of machine-checkable reproducibility is unusual in the sub-field.

Alongside these, the manuscript also reports a compact-PLM **fusion-score parity** with NetMHCpan-4.1 (0.9573 vs 0.9575, Δ = −0.0002, formally tied under a predeclared three-condition rule: DeLong + per-allele Holm-adjusted Wilcoxon + allele-clustered bootstrap CI). NetMHCpan retains the BA-head advantage (Δ = −0.0137, Holm *p* = 1.7 × 10⁻³), which we state in the headline — we do not claim a victory where the data does not support one.

**What the paper is not.** It is not a new state-of-the-art ranker; it is not a new statistical method (DeLong-1988 + Holm-1979 + bootstrap-1979 are standard — the contribution is their *disciplined application* in a sub-field whose published comparisons routinely rely on single pooled AUROC); and it is not a clinical validation. The two case studies in §3.3 (99.93% successor-corpus overlap; 0.862 → 0.442 inductive collapse of a transductive rescorer) illustrate known evaluation pitfalls — their value here is a **concrete, citable ledger of the pitfall occurring on this specific benchmark**, not a claim of discovering the pitfall itself. We are explicit about this in Discussion.

**Scope boundary.** This submission is confined to the v4.1 comparator line (matched training exposure against NetMHCpan-4.1). Comparisons against NetMHCpan-4.2c, BigMHC, and MixMHCpred v3 belong to a parallel manuscript (paper-2) that uses the NetMHCpan-4.2 training archive; mixing the two lines would conflate separate evaluation universes. The scope decision is documented in the public repository.

**Pre-submission compliance pack.** Two internally-prepared compliance audits accompany this submission (publicly mirrored at <https://github.com/KevinSimple/deepneo-pub/tree/main/mdpi_submission/compliance>):

1. A structural compliance audit against *Information*'s Instructions for Authors (18 of 19 items PASS; the one Minor item is reference ordering, a copy-editing-stage task).
2. A content and claims integrity audit against COPE Core Practices, MDPI Research & Publication Ethics, and the ML-evaluation-integrity literature cited in the paper (515 of 515 numeric claims MATCH; zero MISMATCH, zero UNSOURCED, zero withdrawn-headline leak).

**Authorship and Conflicts of Interest.** Authors are Kevin Wang (first) and Parma Nand (co-author and corresponding). Because Dr Nand is a Guest Editor of this Special Issue, we request **independent editorial handling**; he will take **no part** in peer review or editorial decisions for this manuscript (also stated in the Conflicts of Interest section).

**Suggested reviewers.** We have entered five suggestions in the SuSy portal: three ML-methodology researchers whose work matches the SI's themes of responsible evaluation and reproducibility (Gundersen, Henderson, Card), and two data-leakage methodology authors whose work our evaluation contract directly cites (Bernett, Kalinina). We have deliberately **excluded the NetMHCpan and TransPHLA development teams, the MHCflurry and ESM2 primary developers, and public-critic voices in ML-rigor** to preserve first-round impartiality and keep the review constructive and on-scope for an ML/NLP special issue.

**Required statements.**

- Neither the manuscript nor any part of its content is currently under consideration or published elsewhere. We are submitting this work to MDPI *Information* only.
- All authors have approved the manuscript and agree with its submission.
- Preparation of this manuscript benefited from AI assistance for prose revision, figure rendering, and compliance-report generation. All scientific claims, numerical results, and conclusions remain the authors' sole responsibility, and every quantitative claim traces to a committed Supplementary-Data JSON ledger listed in the manuscript's Data Availability Statement.

Thank you for your consideration. We would welcome the opportunity to address reviewer feedback.

Sincerely,

Parma Nand (corresponding author)
Kevin Wang
Auckland University of Technology
