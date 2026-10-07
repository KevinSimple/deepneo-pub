# Prompt for content-generation AI

> **Usage**: paste this prompt verbatim into a content-generation model (e.g. Claude, GPT-4).
> It encodes the paper's ground truth, scope restrictions, tone rules, and audience.
> The expected output is 11 markdown blocks (slides 2–12) that a cloud agent will integrate into `slides.html`.

---

## System context

You are writing slide-level content for a 12-slide HTML presentation deck accompanying a peer-reviewed manuscript:

**Title**: "Efficient Protein Language Models for Peptide–MHC Ranking: A Leakage-Aware Evaluation Protocol under Multiplicity Control"
**Authors**: Kevin Wang, Parma Nand
**Venue**: MDPI *Information* — Special Issue: Emerging Trends in Machine Learning & Natural Language Processing
**Status**: Under review, October 2026
**Code**: github.com/KevinSimple/deepneo-pub

The deck is a 3:45 YouTube intro video slide pack. Each slide maps to one narration block (see timing below). Slide 1 is the title slide and does not need generated content.

---

## Audience

Mixed CS + biology YouTube audience. Viewers range from ML practitioners unfamiliar with immunology to immunoinformaticians unfamiliar with modern PLMs. Assume no prior knowledge of either MHC biology or transformer architectures.

---

## Tone rules

- **Measured, confident, plain English.** No boastful adjectives.
- **NEVER use** the following words or phrases: "groundbreaking", "revolutionary", "state-of-the-art", "novel", "pioneering", "cutting-edge", "game-changing", "breakthrough", "outperforms", "superior", "best", "first-ever".
- Claims must be **hedged where the data hedges**. If the verdict is TIED, say "matches", not "competitive with" or "comparable to" (those imply inferiority).
- Use the **assertion-evidence model**: each slide makes one named claim, backed by data.
- Numbers must be **exactly** as listed in the frozen ground truth below. Do not round, interpolate, or infer.

---

## Scope restrictions (hard)

- **MHC class I only.** No class II claims.
- **Canonical 8–11-mer peptides only.** No post-translational modifications (PTM), no spliced peptides.
- **No clinical claims.** The paper is computational; do not claim clinical utility, patient outcomes, or vaccine efficacy.
- **No TCR-specificity claims.** The model predicts peptide–MHC binding/presentation, not T-cell recognition.
- **No claims about NetMHCpan-4.2.** The paper's primary comparisons are against 4.1.
- **No new quantitative claims** beyond what appears in the frozen ground truth below.

---

## Frozen ground truth

All numbers below are committed to SI JSON ledgers in `../evidence/supplementary_data/`. Every number in the deck must trace to one of these.

### Model

| Fact | Value | Source |
|---|---|---|
| Architecture | ESM2-35M trunk + cross-attention | Manuscript Sec 2 |
| Parameters | 35 million | Manuscript Sec 2 |
| Layers | 12, d=480 | Manuscript Sec 2 |
| Training data | NetMHCpan-4.1 official 5-fold BA + EL | Manuscript Sec 2 |
| Heads | BA head + EL head → batch-rank fusion | Manuscript Sec 2 |
| Deployed config | 5-fold ensemble | Manuscript Sec 2 |

### TransPHLA benchmark (decontaminated vs NMP-4.1)

| Metric | Value | Source |
|---|---|---|
| Total rows | 161,652 | `transphla_rescored_fusion_fixed.json` |
| Contaminated rows removed | 43,509 (26.9%) | `transphla_rescored_fusion_fixed.json` |
| Clean rows | 118,143 | `transphla_rescored_fusion_fixed.json` |
| **Fusion vs Fusion Δ AUROC** | **−0.0002** | `transphla_rescored_fusion_fixed.json` → `clean_vs_41_118143` |
| Fusion DeepNeo AUROC | 0.9573 | same |
| Fusion NMP AUROC | 0.9575 | same |
| Fusion DeLong p | 0.424 | same |
| Fusion Holm-adjusted p | 0.505 | `table2_holm_adjusted.json` |
| Fusion bootstrap CI | [−0.0061, +0.0059] | `paired_bootstrap_ci.json` |
| Fusion CI excludes zero? | **No** → TIED | same |
| **BA vs BA Δ AUROC** | **−0.0137** | `transphla_rescored_fusion_fixed.json` → `clean_vs_41_118143` |
| BA DeepNeo AUROC | 0.9363 | same |
| BA NMP AUROC | 0.9500 | same |
| BA DeLong p | < 0.001 | same |
| BA Holm-adjusted p | 1.7 × 10⁻³ | `table2_holm_adjusted.json` |
| BA bootstrap CI | [−0.0199, −0.0075] | `paired_bootstrap_ci.json` |
| BA CI excludes zero? | **Yes** → NMP wins | same |
| **EL vs EL Δ AUROC** | **+0.0059** | `transphla_rescored_fusion_fixed.json` → `clean_vs_41_118143` |
| EL DeepNeo AUROC | 0.9640 | same |
| EL NMP AUROC | 0.9581 | same |
| EL Holm-adjusted p | 0.505 | `table2_holm_adjusted.json` |
| EL bootstrap CI | [−0.0032, +0.0180] | `paired_bootstrap_ci.json` |
| EL CI excludes zero? | **No** → Holm-tied | same |

### IEDB weekly leaderboard (46 human-allele weeks, 2020–2026)

| Metric | Value | Source |
|---|---|---|
| BA board predictors | 14 | `weekly_ranking_v41_2020_2026_singlecol_v2.json` |
| DeepNeo BA mean rank | 6.85 / 14 | same |
| DeepNeo BA mean AUROC | 0.7951 | same |
| DeepNeo BA rank-1 weeks (incl. ties) | 14 | same |
| DeepNeo BA rank-1 outright | 9 | same |
| NMP-4.0 BA mean rank | 4.98 | same |
| NMP-4.1 BA mean rank | 5.14 | same |
| EL board predictors | 3 | same |
| DeepNeo EL mean rank | **1.80** | same |
| DeepNeo EL mean AUROC | 0.7763 | same |
| DeepNeo EL rank-1 weeks (incl. ties) | 24 / 46 | same |
| DeepNeo EL rank-1 outright | 19 | same |
| NMP-4.1 EL mean rank | 2.01 | same |
| NMP-4.0 EL mean rank | 2.17 | same |

### IEDB auto_bench pool contamination

| Metric | Value | Source |
|---|---|---|
| Pool rows | 44,516 | `autobench_decontam_vs_41.json` / slide 5 |
| NMP-4.1 overlap | 21.4% | same |
| NMP-4.2 overlap | 22.7% | same |
| Eval rows (used for weekly) | 38,606 | same |
| Eval NMP-4.1 overlap | 15.1% | same |

### Transductive-overfitting case study

| Metric | Value | Source |
|---|---|---|
| In-sample (transductive) AUROC | 0.862 | `inductive_reranker_result.json` → IEDB BA |
| Held-out (inductive) AUROC | 0.442 | same |
| Interpretation | Below chance; transductive overfitting | Manuscript Sec 3.6 |
| Disposition | Component withdrawn; reported as negative result | same |

### Three-condition superiority rule

A signed Δ is reported as a real win only if **all three** hold:
1. Paired DeLong p < 0.05 on the same rows
2. Per-allele Wilcoxon signed-rank with **Holm-adjusted** p < 0.05 across the family of four TransPHLA comparisons
3. Allele-clustered bootstrap 95% CI on Δ excludes zero (B = 1,000; n = 118,143)

### Contamination protocol

- Exact peptide–HLA pair match against NetMHCpan-4.1's training-pair union
- On TransPHLA: 43,509 / 161,652 removed (26.9%) → 118,143 clean rows
- Applied before all scoring; no shared pair remains in any evaluation

---

## Expected output

Generate 11 markdown blocks, one per slide (slides 2–12). Each block should contain:

1. **Slide number and title** (matching the existing slide structure)
2. **Key claim** (one assertion-evidence sentence)
3. **Supporting text** (2–4 bullet points or short paragraphs, suitable for slide body text)
4. **Data points** (exact numbers from the frozen ground truth, with source citation)
5. **Narration cue** (which `[time]` block from the narration script this corresponds to)

### Slide mapping

| Slide | Topic | Narration block |
|---|---|---|
| 2 | Biology: MHC class I antigen presentation | [0:00–0:15] HOOK + [0:15–0:45] WHY IT MATTERS |
| 3 | ML framing: sequence ranking under a context key | [0:45–1:10] FRAMING AS ML |
| 4 | DeepNeo-CL architecture | [1:10–1:30] PIVOT |
| 5 | Why reported gains are hard to trust (leakage + multiple testing) | [1:30–2:05] THE PROBLEM |
| 6 | Three-condition superiority rule | [2:05–2:25] OUR PROTOCOL |
| 7 | Decontaminated TransPHLA headline result | [2:25–2:45] HEADLINE RESULT |
| 8 | IEDB weekly leaderboard | [2:45–3:05] IEDB WEEKLY |
| 9 | Where NetMHCpan still wins (BA-head) | [3:05–3:15] HONEST |
| 10 | Transductive-overfitting failure (0.862 → 0.442) | [3:15–3:35] CASE STUDY |
| 11 | What this paper actually claims (3 cards) | [3:35–3:45] TAKEAWAY |
| 12 | Resources + CTA | [3:40–3:45] CTA |

---

## Final check

Before submitting your output, verify:
- [ ] Every number matches the frozen ground truth exactly
- [ ] No scope-restricted claims (class II, clinical, TCR, PTM)
- [ ] No banned words used
- [ ] Each slide has exactly one key claim
- [ ] Source citations are included for every data point
