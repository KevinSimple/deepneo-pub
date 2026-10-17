# Extended trailer script — DeepNeo-CL · 2:30 explainer

Target: longer-form explainer for YouTube main-feed, Twitter long-form, LinkedIn, pub-repo landing-page embed, MDPI SI promo.

**Honest-tier framing** (binding — matches the paper's actual value tier):
- Lead the real findings (**leakage ledger · calibration · SI evidence pack**)
- Headline fusion match as a **tie**, not a win
- Case studies compressed into one beat; framed as "concrete ledgers for known traps"
- Three-condition rule reframed as "standard tools, applied with discipline"

**Visual plates**: 6 FigureLab plates (fl01–fl06) + 4 paper-figure PNGs (fig_S1_calibration, fig_roc_pr_decontam, fig_data_flow, fig07_ablation_grid) + 3 static text cards.

**Pacing**: 10 beats across 2:30, ~15 s per beat; narration ~180 wpm.

---

## 0:00 – 0:15 · The biology opener

**Visual**: `fl01_mhc_presentation.png` (full-frame, slow Ken-Burns zoom).

**Narration** (~40 words):

> Every nucleated cell in your body chops its own proteins into short fragments — **peptides** — and displays them on its surface, bound to **MHC class I**. This is how CD8+ T-cells know what's happening inside a cell they can't see into.

---

## 0:15 – 0:28 · Why it matters

**Visual**: `fl02_normal_vs_cancer.png`.

**Narration** (~35 words):

> Tumour cells also display **neoantigens** — fragments of mutated proteins. If a T-cell sees a neoantigen on an MHC class I molecule, it kills the cell. Personalised cancer-vaccine design depends on predicting which peptides a given HLA allele will present.

---

## 0:28 – 0:43 · Where this prediction sits

**Visual**: 🖼 **Pipeline card** — 5-stage flow: Patient sequencing → Mutation calls → Candidate peptides → **MHC-presentation prediction (DeepNeo-CL)** → Vaccine. Stage 4 highlighted amber with "YOU ARE HERE".

**Narration** (~38 words):

> Here's where machine learning enters. The industry reference is **NetMHCpan-4.1**. We built DeepNeo-CL — a 35-million-parameter PLM, trained on NetMHCpan's own cross-validation folds, so no training-data advantage. The paper is about what happens when you compare the two honestly.

---

## 0:43 – 1:00 · The real finding #1 — 26.9% leakage

**Visual**: `fl04_leakage_venn.png`.

**Narration** (~50 words):

> First real finding. The widely-cited TransPHLA holdout contains **twenty-six point nine percent exact (peptide, HLA) pair overlap** with NetMHCpan-4.1's own training corpus. Forty-three thousand five hundred and nine pairs removed. Every TransPHLA number in the paper is on the clean subset — **n equals 118,143** — and the pair-level ledger ships as machine-readable Supplementary Data, so anyone can reproduce or contest the cut.

---

## 1:00 – 1:14 · The honest headline — a tie

**Visual**: `figures_paper/png/fig_roc_pr_decontam.png`.

**Narration** (~42 words):

> Under exact decontamination plus **Holm-adjusted per-allele tests**, DeepNeo-CL fused-score and NetMHCpan-4.1 fused-score are **tied** on the clean subset — 0.9573 versus 0.9575. NetMHCpan keeps the BA-head lead at Δ = −0.0137, Holm p = 1.7×10⁻³. We report both.

---

## 1:14 – 1:30 · The real finding #2 — calibration

**Visual**: `figures_paper/png/fig_S1_calibration.png`.

**Narration** (~50 words):

> Second real finding, and probably the paper's most useful one. On the TransPHLA EL set, **expected calibration error 0.091 versus 0.202** — DeepNeo-CL's probability outputs have less than half NetMHCpan's calibration error at 10-bin reliability. This matters practically for any vaccine-design pipeline that thresholds scores at a chosen probability.

---

## 1:30 – 1:44 · The model, briefly

**Visual**: `figures_paper/png/fig_data_flow.png` (or `graphical_abstract.svg` middle panel).

**Narration** (~42 words):

> The model is deliberately compact. ESM2-35M trunk, one cross-attention layer letting each peptide position attend over the HLA pseudo-sequence, two heads for BA and EL, five-fold ensemble. Trained on commodity GPUs. The gain over the peptide-only baseline is **distributed** across components, not any single trick.

---

## 1:44 – 2:00 · The three-condition rule

**Visual**: 🧬 `fl05_multiplicity_holm.png` (the 4-comparison Holm family image).

**Narration** (~48 words):

> The evaluation contract: **DeLong (1988) + Holm (1979) + bootstrap (1979)**. All standard tools — the contribution is applying all three with discipline in a sub-field that routinely does pooled-AUROC-only comparisons. Under this contract, the only Holm-robust TransPHLA asymmetry is NetMHCpan's BA-head lead.

---

## 2:00 – 2:14 · Two cautionary ledgers (known traps, concrete numbers)

**Visual**: `fl06_transductive_collapse.png` (left-side 0.862→0.442, with 99.93% overlay in text).

**Narration** (~48 words):

> Two cautionary ledgers. **Ninety-nine point nine three percent** of an author-constructed holdout turns out to be in NetMHCpan-4.2's later training. A pocket rescorer fitted by CV on the eval set hit AUROC **0.862** — then collapsed to **0.442**, below chance, when honestly held out. Known traps. Specific numbers.

---

## 2:14 – 2:30 · The evidence pack + end card

**Visual**: 🖼 **End card** (title, authors, QR, link) with brief "17 SI JSON ledgers · committed audit script" overlay 2:14–2:20.

**Narration** (~35 words):

> **Seventeen public SI JSON ledgers.** Every substantive numeric claim in the paper traces to a committed file; a committed audit script shows 43 of 43 headline checks match. Full paper, evidence pack, and compliance audits at the link.

Fade to end card for the remaining ~8 s (QR scan time).

---

## Word count & timing audit

| Beat | Words | Target seconds @ 180 wpm | OK? |
|---|---|---|---|
| 0:00–0:15 (fl01)                 | 40 | 13 | ✅ |
| 0:15–0:28 (fl02)                 | 35 | 12 | ✅ |
| 0:28–0:43 (pipeline card)        | 38 | 13 | ✅ |
| 0:43–1:00 (**26.9% leakage**)    | 50 | 17 | ✅ |
| 1:00–1:14 (**honest tie**)       | 42 | 14 | ✅ |
| 1:14–1:30 (**calibration**)      | 45 | 15 | ✅ |
| 1:30–1:44 (architecture)         | 42 | 14 | ✅ |
| 1:44–2:00 (Holm discipline)      | 48 | 16 | ✅ |
| 2:00–2:14 (cautionary ledgers)   | 48 | 14 | ✅ |
| 2:14–2:30 (ledger + end card)    | 35 | 12 | ✅ |
| **Total**                        | **423** | **~141 s** | 🟡 brisk read lands under 2:30 with ~8-10 s end-card hold |

---

## What changed from the earlier draft

**Promoted (now have dedicated beats):**
- 26.9% leakage (was folded into "problem 1" — now stands alone as "the real finding #1")
- Calibration (was tacked onto the end — now a dedicated real-finding beat with the honest "probably the paper's most useful finding" framing)
- The SI evidence pack (17 ledgers + committed audit script) — now in the end-card beat

**Demoted / compressed:**
- Multiplicity trap (dropped as a standalone beat; the Holm framing is in beat 8 as "the three-condition rule" with explicit "standard tools, applied with discipline")
- Case studies (compressed from 2 beats to 1 beat; framed as "known traps, specific numbers" not "surprising findings")

**Honest-tie framing throughout:** no "beats NetMHCpan". The 0.9573 vs 0.9575 tie is the headline. The BA-head loss is reported alongside, as the paper does.

**End-card copy change:** emphasizes **17 SI JSON ledgers + committed audit script** (the real receipts), not just the paper title.

---

## Shot list / editor notes

Unchanged from the earlier draft:
- Each FigureLab plate held full-screen with slow Ken-Burns (10–15% zoom over its beat)
- Static text cards (pipeline / end card) stay still
- 0.3 s crossfades between beats
- Hard-burn captions for silent-autoplay viewers
- −18 LUFS integrated, duck under narration to −24 LUFS
- Export: 1080p MP4 + 1080×1080 square crop + SRT captions
