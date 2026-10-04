# Phase 0 — Field analysis and reviewer configuration

2026-10-04 · `academic-paper-reviewer` · target manuscript `latex/deepneo_information.tex`

**Author-confirmed venue (not inferred):** MDPI *Information* (ISSN 2078-2489), Special Issue *Emerging Trends in Machine Learning and Natural Language Processing*, Article type, Section Information Processes. Guest Editors: Parma Nand (also corresponding author; COI disclosed) and Wei Qi Yan.

`criteria_binding_unavailable` — no #684 ReviewCriteriaBindingManifest was supplied. Venue metadata below is the author-confirmed target from `AUTHOR_NOTES.md` / `SCOPE_AND_GUIDELINES.md`, not a field-analyst substitution.

## Six-dimension analysis

| Dimension | Result |
|---|---|
| Primary discipline | Machine learning for biomedical sequence ranking (protein language models) |
| Secondary | Computational immunology / immunoinformatics; ML evaluation integrity (leakage, multiplicity); information science (SI home) |
| Research paradigm | Quantitative empirical |
| Methodology type | Statistical modeling / machine learning; benchmark evaluation with predeclared statistical contract |
| Target journal tier | Author-confirmed: MDPI *Information* SI (mid-tier OA; APC 1800 CHF). Not a Nature/NeurIPS claim. |
| Paper maturity | Pre-submission (complete IMRaD + MDPI back matter; Style-A/CS-register pass 2026-09-29) |

---

### Reviewer Configuration Card #1

**Role**: EIC  
**Display role**: Journal-Fit Reviewer  
**Identity Description**: Associate Editor of *Information* handling the SI *Emerging Trends in ML and NLP*; background in applied transformers / domain adaptation; screens healthcare-adjacent ML for overclaim and SI keyword fit (efficiency, interpretability, robustness, responsible AI) without requiring English-text NLP.  
**Review Focus**:
  1. Does a protein-LM pMHC ranker belong in this SI, or should it go to *Bioinformatics* / *Briefings in Bioinformatics*?
  2. Are title keywords (Efficient, Protein Language Models, Leakage-Aware, Multiplicity) delivered or decorative?
  3. Guest-Editor COI (P.N. is SI GE and corresponding author) and independent-handling disclosure.
**Will particularly care about**: Whether readers of an ML/NLP SI get a transferable evaluation lesson, not only a domain AUROC table.
**Possible blind spots**: Will not check DeLong/Holm algebra.

---

### Reviewer Configuration Card #2

**Role**: Peer Reviewer 1  
**Display role**: Peer Reviewer 1 (Methodology)  
**Identity Description**: Computational-immunoinformatics methodologist who runs IEDB auto_bench-style evaluations; specializes in AUROC/AUPR, DeLong, Holm, allele-clustered bootstrap, and train–test pair decontamination against NetMHCpan corpora.  
**Review Focus**:
  1. Three-condition rule internally consistent with Table 1 (including v4.2 rows).
  2. Decontamination is a lower bound — is it oversold as “without the two confounders”?
  3. Ablation on full TransPHLA (n=161,652) vs clean n=118,143; rescorer CV on the evaluation set.
**Will particularly care about**: Allele as inferential unit vs row-level DeLong; two Wilcoxon universes (per-ref p=0.65 vs per-week p=0.0453).
**Possible blind spots**: SI keyword fit; missing Hashemi 2023.

---

### Reviewer Configuration Card #3

**Role**: Peer Reviewer 2  
**Display role**: Peer Reviewer 2 (Domain)  
**Identity Description**: pMHC-I presentation researcher; NetMHCpan / MHCflurry / TransPHLA / BigMHC user; tracks ESM fine-tunes for peptide–MHC (Hashemi *Front. Bioinform.* 2023 and later PLM–pMHC papers).  
**Review Focus**:
  1. Related Work coverage of PLM–pMHC prior art vs from-scratch transformers.
  2. Biological correctness of BA vs EL, MS motif deconvolution, pocket/cleft language.
  3. Whether “competitive with NetMHCpan-4.1” is the right claim given BA-head deficit and IEDB mid-field.
**Will particularly care about**: Misstating NNAlign_MA as assay-side; claiming first/efficient PLM without citing Hashemi.
**Possible blind spots**: MDPI production rules (bib order, 200-word abstract).

---

### Reviewer Configuration Card #4

**Role**: Peer Reviewer 3  
**Display role**: Peer Reviewer 3 (Perspective)  
**Identity Description**: Responsible-ML / evaluation-integrity researcher (Kapoor *Patterns* 2023 lineage); reads leakage, selective reporting, and multiplicity papers; not a pMHC specialist.  
**Review Focus**:
  1. Is the evaluation-contract contribution transferable outside pMHC?
  2. Interpretability SI keyword vs “no model-internal attribution.”
  3. Live demo URL and public claims vs manuscript honesty.
**Will particularly care about**: A landing page that advertises a 12/12 win the paper does not claim; “often” field-frequency claims without a survey.
**Possible blind spots**: Allele-filter n=84 vs 91 vs 112.

---

### Devil's Advocate

Fixed fifth seat. No configuration card. Stress-tests: novelty vs Hashemi; title Efficient; dirty ablation → clean tie; per-length “leads”; live URL; GE corresponding author.

---

Panel provenance (disclosed, not “independence”): all five seats same model family, same provider, no human reviewer IDs. `role_separated=true`; `model_family_distinct=false`; `provider_distinct=false`; `human_distinct=false`. Correlated-error disclosure required.
