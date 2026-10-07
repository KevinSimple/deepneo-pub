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

### Making biology accessible to CS readers

The primary audience skews CS/ML. Biology slides (especially slide 2) must bridge the gap with:

1. **Concrete analogies** — map biology to CS concepts the audience already knows:
   - MHC-I = "a display rack on every cell's surface"
   - Peptide binding = "a lock-and-key lookup — the MHC groove is the lock, the peptide is the key"
   - T-cell surveillance = "a distributed anomaly-detection system — every cell reports, T-cells are the classifiers"
   - Proteasome = "a shredder that chops proteins into short fragments for inspection"
   - Neoantigen = "a mutant fragment that triggers a true-positive alert"
   - Binding prediction = "given a lock (HLA allele) and 10,000 candidate keys (peptides), rank which keys fit"

2. **Vivid visual language** — the slides should feel visual and alive, not like a textbook:
   - Use colour to separate biological actors (e.g. green = healthy, red/orange = mutant, blue = MHC machinery)
   - Inline SVG diagrams are preferred over text-heavy explanations
   - Show the biology as a **process with steps** (protein → shredding → loading → surface display → T-cell recognition), not as a static definition
   - Use numbered steps (①②③④) to guide the viewer's eye through biological pathways

3. **"So what?" framing** — every biology fact must connect to why a CS person should care:
   - "This is why it's a ranking problem" (not just "this is how the immune system works")
   - "Errors here → wrong peptides tested in the lab → wasted experiments"
   - "The combinatorial space is huge: ~10⁴ candidates × ~10⁴ HLA alleles"

4. **Visual assets the agent should create or source**:
   - Inline SVGs for biological pathways (the deck already has one on slide 2 — extend this style)
   - Schematic diagrams over photographs (schematics are clearer at slide resolution)
   - Side-by-side "CS concept ↔ biology concept" mapping cards where appropriate
   - Data visualisation (bar charts, forest plots) over tables where possible

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

### Ablation ladder (7 cumulative steps → deployed model)

Each step adds one component on top of the previous. AUROC/AUPR are on the **full** 161,652-row TransPHLA EL benchmark.

| Step | Component | AUROC | Δ AUROC | Source |
|---|---|---|---|---|
| 1 | ESM2-35M baseline (peptide only) | 0.952 | — | `ablation_ladder.json` |
| 2 | + V37 position-resolved physicochemical features | 0.957 | +0.005 | same |
| 3 | + pseudo-sequence concatenation | 0.962 | +0.005 | same |
| 4 | + peptide × pseudo cross-attention | 0.964 | +0.002 | same |
| 5 | + effective-number weighting (pseudo-cluster × BA-bin) | 0.969 | +0.005 | same |
| 6 | + LDS (label-distribution smoothing) on IC50 | 0.971 | +0.002 | same |
| 7 | + SupCon v2 refinement (deployed headline) | 0.970 | −0.001 | same |

Key prose claims from manuscript:
- Cross-attention cumulative gain over baseline (steps 3–4): **+0.012**
- Effective-number weighting single-step gain: **+0.005**
- SupCon v2 rare-allele AUPR boost (n_train < 100): **+0.022**
- No single step Δ exceeds +0.005
- SupCon v2 carries a small AUROC cost (−0.001) but improves rare-allele robustness

### Withdrawn / rejected components (negative results)

These were tested and deliberately excluded from the deployed model:

| Component | Reason for rejection | Source |
|---|---|---|
| Crystal-template pocket rescorer | Transductive overfitting (0.862 → 0.442) | `inductive_reranker_result.json` |
| ESMFold pocket descriptor | pLDDT ≈ 0.42 on 34-mer pseudo-sequence (unreliable) | `ablation_ladder.json` |
| Allele-identity contrastive label | Over-clusters HLA-A*02:01 | same |
| Focal loss (γ=5) | Within-noise; worse rare-allele performance | same |
| Anchor-pocket hard attention mask | No gain | same |
| Learned-adaptive anchor-pocket bias | No gain | same |
| Full ESM2 fine-tune (all layers) | No improvement over frozen trunk | same |

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

### IEDB per-reference Wilcoxon (deployment-fair comparison)

| Metric | Value | Source |
|---|---|---|
| Per-ref W/T/L (DeepNeo fusion vs NMP-4.1 BA) | 15 / 12 / 19 | `weekly_perref_wilcoxon_vs_nmp41.json` |
| Per-ref Wilcoxon p | 0.65 (not significant) | same |
| Per-ref mean Δ | −0.0067 | same |
| Per-week W/T/L (pooled AUROC) | 13 / 5 / 28 | `weekly_ranking_v41_2020_2026_singlecol_v2.json` |
| Per-week Wilcoxon p | 0.045 | same |
| Per-week mean Δ AUROC | −0.012 | same |

**Important**: the per-reference and per-week tests give different results (p=0.65 vs p=0.045). The manuscript reports p=0.65 as the primary result because per-reference is the deployment-fair unit.

### IEDB auto_bench pool-level comparison (146 intersection references)

| Metric | DeepNeo Fusion | NMP-4.1 BA | MHCflurry | Source |
|---|---|---|---|---|
| BA intersection mean AUROC | 0.7506 | 0.7689 | 0.7564 | `head_to_head_ba_el_split.json` |
| vs DeepNeo Wilcoxon p | — | 0.0194 | 0.7182 | same |
| vs DeepNeo W/T/L | — | 52/22/72 | 60/12/74 | same |

### IEDB auto_bench pool contamination

| Metric | Value | Source |
|---|---|---|
| Pool rows | 44,516 | `autobench_decontam_vs_41.json` / slide 5 |
| NMP-4.1 overlap | 21.4% | same |
| NMP-4.2 overlap | 22.7% | same |
| Eval rows (used for weekly) | 38,606 | same |
| Eval NMP-4.1 overlap | 15.1% | same |

### Transductive-overfitting case study

**Headline (IEDB BA — the worst collapse):**

| Metric | Value | Source |
|---|---|---|
| Base AUROC | 0.828 | `inductive_reranker_result.json` → IEDB BA |
| In-sample (transductive) AUROC | 0.862 | same |
| Held-out (inductive) AUROC | 0.442 | same |
| Interpretation | Below chance; transductive overfitting | Manuscript Sec 3.6 |
| Disposition | Component withdrawn; reported as negative result | same |

**Cross-benchmark rescorer results (all three channels):**

| Benchmark | Base | Transductive | Inductive | Source |
|---|---|---|---|---|
| IEDB BA | 0.828 | 0.862 | **0.442** | `inductive_reranker_result.json` |
| TransPHLA BA | 0.955 | 0.977 | 0.871 | same |
| TransPHLA EL | 0.970 | 0.978 | 0.889 | same |

The IEDB BA channel shows the most dramatic collapse because it has the fewest alleles and most extreme class imbalance. TransPHLA channels also degrade but less dramatically because they have 112 alleles (more diverse).

### Three-condition superiority rule

A signed Δ is reported as a real win only if **all three** hold:
1. Paired DeLong p < 0.05 on the same rows
2. Per-allele Wilcoxon signed-rank with **Holm-adjusted** p < 0.05 across the family of four TransPHLA comparisons
3. Allele-clustered bootstrap 95% CI on Δ excludes zero (B = 1,000; n = 118,143)

### Fusion closeness metric

| Metric | Value | Source |
|---|---|---|
| CDF |Δ| batch-rank vs CDF-fusion | 9.1 × 10⁻⁵ | `transphla_fusion_cdf_rescored.json` |
| Interpretation | Fusion method choice barely matters; the tie is robust | same |

### Key directional claims (re-derived from ledgers)

These are non-numeric claims verified in `CLAIM_EVIDENCE_TABLE.md`:

- NMP-4.0 BA is the BA mean-rank consistency leader (4.98)
- DeepNeo BA is mid-board, not leader (6.85 vs leader 4.98)
- DeepNeo hits rank-1 on more BA weeks than NMP-4.1 BA (14 vs 11, incl. ties)
- DeepNeo EL leads the three-predictor EL board (1.80; board size = 3)
- No single ablation step Δ exceeds +0.005
- **Only the v4.1 BA-head survives all three conditions** (DeLong + Holm + CI)
- The surviving BA-head effect is a DeepNeo **deficit** (mean per-allele Δ = −0.0053)
- The deployed fusion's pooled lead (+0.0073) is **not** Holm-robust (Holm p = 0.151)
- Fusion-vs-fusion is a tie (Δ = −0.0002, bootstrap CI includes zero)
- Inductive rescorer is below chance (0.442 < 0.5)

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
