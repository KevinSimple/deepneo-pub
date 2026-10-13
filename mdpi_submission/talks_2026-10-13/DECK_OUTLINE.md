# Conference deck outline — DeepNeo-CL · 15 slides · 10–12 min

**Target venue**: ML/NLP SI-style session, CS/ML-literate audience. Also serviceable at a bioinformatics venue (the biology intro is correct, not just friendly).

**Timing budget**: 45 s per slide average. Section 1 (biology intro) runs slightly longer per slide; results slides run shorter.

**Visuals**: FigureLab outputs (`figures_input/fl0N_*.png`) for biology; real paper figures (`figures_paper/*.pdf`) for data. Paper figures ship inside [latex/figures/](../../latex/figures/).

**Legend for the Visual column**:
- 🧬 = FigureLab illustration (from `FIGURELAB_PROMPTS.md`)
- 📊 = real paper figure (from `latex/figures/`)
- 📝 = text-only slide

---

## Section 1 — Biology for CS (slides 1–4, ~3:30)

### Slide 1 · Title

| Field | Content |
|---|---|
| Headline | **Efficient Protein Language Models for Peptide–MHC Ranking** |
| Subheadline | A Leakage-Aware Evaluation Protocol under Multiplicity Control |
| Visual | 📝 text-only; small graphical abstract thumbnail bottom-right |
| Footer | Kevin Wang · Parma Nand · Auckland University of Technology · MDPI *Information* 2026 |
| Speaker note | *"Thanks for having me. This talk is about one specific — and in my view under-reported — failure mode in protein-language-model benchmarking. We'll start with 60 seconds of biology, then spend the rest on evaluation."* |
| Timing | 0:00 – 0:20 |

### Slide 2 · The biology in 60 seconds

| Field | Content |
|---|---|
| Headline | **MHC class I presents 8–11-residue peptides to CD8+ T-cells** |
| Visual | 🧬 `fl01_mhc_presentation.png` (full-slide, right 60%) |
| Bullet (left 40%) | · Cytosolic proteins → proteasome → short peptides<br>· Peptides loaded onto MHC-I in the ER<br>· Displayed on the cell surface for TCR surveillance |
| Speaker note | *"Every nucleated cell is constantly chopping its own proteins into little fragments and holding them up on its surface. CD8+ T-cells patrol and inspect those fragments. If the fragment looks wrong, the cell dies. That's immune surveillance."* |
| Timing | 0:20 – 1:10 |

### Slide 3 · Why we care computationally

| Field | Content |
|---|---|
| Headline | **Which peptides will a given HLA allele present?** |
| Visual | 🧬 `fl02_normal_vs_cancer.png` |
| Bullet | · Healthy cells → self peptides → tolerance<br>· Tumour cells → *neoantigens* → cytotoxic recognition<br>· **Neoantigen prediction = cancer-vaccine design** |
| Speaker note | *"The clinical application that gets most of the attention is personalised cancer vaccines. If we can predict which peptides a patient's tumour will present on their specific HLA alleles, we can prioritise which neoantigens to put in a vaccine. That upstream prediction is where this field lives."* |
| Timing | 1:10 – 2:00 |

### Slide 4 · The task, formally

| Field | Content |
|---|---|
| Headline | **A ranking problem over 10²–10⁴ candidate peptides per allele** |
| Visual | 🧬 `fl03_ranking_task.png` |
| Bullet | · Input: (peptide, HLA pseudo-sequence) pair<br>· Output: BA (log-IC50) + EL (binding probability)<br>· Deployed score: rank-averaged fusion of BA + EL |
| Speaker note | *"The task is ranking. We output two scores — binding-affinity and eluted-ligand — and fuse them at inference. The paper uses the fused score as the headline for deployment and reports the two heads separately only for diagnosis."* |
| Timing | 2:00 – 2:50 |

---

## Section 2 — The evaluation problem (slides 5–8, ~3:30)

### Slide 5 · Who the comparator is

| Field | Content |
|---|---|
| Headline | **NetMHCpan-4.1: the industrial reference** |
| Visual | 📝 text + 3 small logos (NetMHCpan, MHCflurry, TransPHLA) |
| Bullet | · Trained on massive public BA + EL corpus<br>· Comparators: MHCflurry-2.0, external TransPHLA benchmark<br>· **DeepNeo-CL ships on the exact same NetMHCpan-4.1 CV folds — matched training exposure** |
| Speaker note | *"Fair comparison first. We trained on the official NetMHCpan-4.1 five-fold BA and EL partitions. Same training data, same folds, same fold-level test rows. Any gap we report cannot be blamed on 'you had more data'."* |
| Timing | 2:50 – 3:30 |

### Slide 6 · Problem 1 — leakage via a shared public corpus

| Field | Content |
|---|---|
| Headline | **26.9% of a popular holdout was in the training set** |
| Visual | 🧬 `fl04_leakage_venn.png` |
| Bullet | · Exact (peptide, HLA) match between training and test<br>· 43,509 of 161,652 pairs removed<br>· Clean subset: **n = 118,143** |
| Speaker note | *"Here's the first trap. Public benchmarks accumulate over years. When a new model trains on all of them and is then evaluated on 'the next' public benchmark, the overlap is enormous. Our exact-pair decontamination removes 26.9% of the holdout. We only report numbers on the clean subset."* |
| Timing | 3:30 – 4:30 |

### Slide 7 · Problem 2 — multiplicity across the comparison family

| Field | Content |
|---|---|
| Headline | **Four head-to-head tests → Holm across the family of 4** |
| Visual | 🧬 `fl05_multiplicity_holm.png` |
| Bullet | · Per-allele Wilcoxon within each row (84 alleles → 1 p-value)<br>· Holm family-wise correction across the **4 Table 2 comparisons** (m = 4)<br>· Allele-clustered bootstrap CI on paired Δ |
| Speaker note | *"The second trap. Our Table 2 reports four comparisons: BA head, EL head, deployed fusion, and a control. Within each row, we run a per-allele Wilcoxon signed-rank test over 84 alleles to get one p-value per row. Those four p-values then get Holm-corrected. Why four and not 112? Because the comparisons are the inferential family — the 112 alleles are the sample for the within-row Wilcoxon. Under this contract only the NetMHCpan BA-head Δ = −0.0137 (Holm p = 0.0017) survives; the pooled fusion win (raw p = 0.05) drops to Holm p = 0.15 and does not."* |
| Timing | 4:30 – 5:30 |

### Slide 8 · The three-condition rule

| Field | Content |
|---|---|
| Headline | **Only all three conditions = a claim** |
| Visual | 📝 three-column text slide, each column a condition |
| Columns | **① DeLong paired ROC**<br>Pooled AUROC difference, same rows, p < 0.05<br><br>**② Per-allele Wilcoxon · Holm-adjusted**<br>Family-wise error controlled across 112 alleles<br><br>**③ Allele-clustered bootstrap 95% CI**<br>Resample at the allele level, CI on Δ excludes zero |
| Speaker note | *"If a comparator passes all three, we claim an asymmetry. If it passes one or two, we report numbers but refuse to claim superiority. This is the paper's main methodological contribution."* |
| Timing | 5:30 – 6:20 |

---

## Section 3 — The model + the results (slides 9–13, ~3:30)

### Slide 9 · A cautionary case study

| Field | Content |
|---|---|
| Headline | **Transductive fit: 0.862 in-sample → 0.442 held-out** |
| Visual | 🧬 `fl06_transductive_collapse.png` |
| Bullet | · We trained a second-stage pocket-rescorer with 5-fold CV on IEDB BA<br>· CV AUROC: 0.862 (looks SOTA)<br>· Deployed held-out: AUROC 0.442 (below chance)<br>· **Transductive CV on the evaluation set is not a benchmark.** |
| Speaker note | *"Before results, one cautionary tale. We built a pocket rescorer and fitted it with cross-validation on the IEDB BA evaluation set. CV AUROC looked spectacular. When we actually deployed it to held-out alleles, it collapsed below chance. We're documenting the failure mode because this specific trap is very easy to fall into."* |
| Timing | 6:20 – 7:10 |

### Slide 10 · DeepNeo-CL architecture

| Field | Content |
|---|---|
| Headline | **ESM2-35M + peptide × HLA cross-attention + two heads** |
| Visual | 📊 `latex/figures/fig_data_flow.pdf` (middle panel of the graphical abstract works too) |
| Bullet | · 35M-param ESM2 trunk (frozen 2 epochs → top-2 unfrozen)<br>· Cross-attention: peptide positions attend over 34-residue HLA pseudo-sequence + V37 physchem<br>· BA head (censored log-IC50) · EL head (focal BCE)<br>· 5-fold ensemble; deployed BA = rank average |
| Speaker note | *"The model is deliberately compact. ESM2 trunk, one cross-attention layer letting each peptide position attend over the HLA pocket pseudo-sequence, two heads. Trained as a 5-fold ensemble; the deployed score is the batch-rank average of the two heads."* |
| Timing | 7:10 – 7:50 |

### Slide 11 · Headline result — TransPHLA fusion match

| Field | Content |
|---|---|
| Headline | **Fusion vs fusion on decontaminated TransPHLA (n = 118,143): a tie** |
| Visual | 📊 `latex/figures/fig_pooled_h2h_ba.pdf` + inset Table 1 fusion row |
| Numbers | · DeepNeo-CL fusion AUROC **0.9573** vs NetMHCpan-4.1 fusion **0.9575**<br>· Δ = −0.0002 · Tied under the three-condition rule<br>· NetMHCpan retains the **BA-head** advantage (Δ = −0.0137, Holm 1.7×10⁻³) |
| Speaker note | *"The headline. At the fused score we deploy, DeepNeo-CL and NetMHCpan-4.1 are tied — Δ is 0.0002 in NetMHCpan's favour, which under our three-condition rule is a tie. If you look at the BA head alone, NetMHCpan keeps a small but Holm-robust lead."* |
| Timing | 7:50 – 8:40 |

### Slide 12 · IEDB weekly scoreboard

| Field | Content |
|---|---|
| Headline | **Mid-field on BA (6.85 / 14) · EL panel lead (mean rank 1.80 of 3)** |
| Visual | 📊 `latex/figures/fig_weekly_ranking_ba.pdf` |
| Bullet | · IEDB auto_bench weekly, same rows across 14 predictors<br>· BA: mid-field — not a win, not a loss<br>· EL (3-predictor MS panel): leads mean rank |
| Speaker note | *"On the IEDB weekly scoreboard — this is the field's rolling community benchmark — DeepNeo sits mid-field on binding-affinity, which is honest. On the smaller eluted-ligand MS panel, which is three predictors, it leads mean rank at 1.80. Neither is a 'we beat the baseline' claim."* |
| Timing | 8:40 – 9:20 |

### Slide 13 · Calibration

| Field | Content |
|---|---|
| Headline | **Expected calibration error 0.091 vs 0.202** |
| Visual | 📊 `latex/figures/fig_S1_calibration.pdf` |
| Bullet | · Reliability diagram, 10-bin ECE<br>· DeepNeo-CL better calibrated at low-score end<br>· Matters for score thresholding in downstream vaccine pipelines |
| Speaker note | *"One place DeepNeo does win cleanly: calibration. The ECE on the clean TransPHLA set is 0.091 for DeepNeo and 0.202 for NetMHCpan-4.1. This matters practically — a vaccine-design pipeline that thresholds scores at a chosen cutoff needs the thresholds to mean what they say."* |
| Timing | 9:20 – 9:50 |

---

## Section 4 — Takeaway (slides 14–15, ~1:30)

### Slide 14 · What the paper actually contributes

| Field | Content |
|---|---|
| Headline | **Three contributions — not a bigger model** |
| Visual | 📝 three large text blocks |
| Columns | **① A compact PLM ranker**<br>35M params, trained on the public corpus<br>Matches the industrial baseline at the fused score<br><br>**② A leakage-aware, multiplicity-controlled evaluation contract**<br>Exact decontamination + DeLong + Holm + bootstrap<br>Portable to any shared-corpus ranking task<br><br>**③ Two failure-mode case studies**<br>Successor-corpus overlap (99.93%)<br>Transductive-CV collapse (0.862 → 0.442) |
| Speaker note | *"If there's one thing to remember, it's contribution two. The model is a compact competitor; that's fine. The methodology is what we hope people adopt. The failure-mode case studies are there because the field needs cautionary tales as much as it needs new models."* |
| Timing | 9:50 – 10:50 |

### Slide 15 · Links + QR

| Field | Content |
|---|---|
| Headline | **Thanks** |
| Visual | QR code (top-right) → github.com/KevinSimple/deepneo-pub |
| Bullet | · Paper + evidence pack: github.com/KevinSimple/deepneo-pub/mdpi_submission<br>· Live model: deepneo.kevinwanglab.org<br>· Personal site: kevinwanglab.org<br>· Contact: kevin.wang.anz@hotmail.com |
| Speaker note | *"The pub repo has the full compliance pack — every number traces to a committed JSON ledger. The live service is a follow-up v4.2 line; its numbers are not comparable with this paper's. Happy to take questions."* |
| Timing | 10:50 – 11:30 |

---

## Export checklist

Before you give the talk:

- [ ] All 6 `fl0N_*.png` files present in `figures_input/`
- [ ] Paper figures copied to `figures_paper/` (or linked from `../../latex/figures/`)
- [ ] Deck exported as both `.pptx` (fallback) and `.pdf` (projection-safe)
- [ ] Speaker-notes printed or on a second screen
- [ ] A **1-slide backup** with just slide 11's headline number for Q&A reference
- [ ] Timer app set to 11:30 soft, 12:30 hard
