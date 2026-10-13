# Trailer script — DeepNeo-CL · 90 seconds

Target: short promo for the MDPI *Information* submission. Lives on YouTube Shorts (vertical crop), Twitter/X (16:9), and the pub-repo README banner. CS audience; real biology vocabulary.

**Visual plates**: the 6 FigureLab illustrations from `FIGURELAB_PROMPTS.md`, each held on screen for ~12 s with subtle Ken-Burns pan. End card at 1:20.

**Pacing**: 90 s total. One illustration per 12-s beat. Narration deliberately under-fills so the images breathe.

---

## 0:00 – 0:12 · The biology

**Visual**: `fl01_mhc_presentation.png` (MHC class I presentation pathway).

**Narration**:

> Every cell in your body displays short protein fragments on its surface — called **peptides** — bound to a molecule called **MHC class I**. This is how CD8+ T-cells know what's going on inside the cell.

---

## 0:12 – 0:24 · Why it matters

**Visual**: `fl02_normal_vs_cancer.png` (healthy vs tumour display).

**Narration**:

> When a cell is healthy, it presents **self** peptides, and the immune system ignores them. When it's a tumour, it presents **neoantigens** — mutation-derived peptides that mark it for destruction. Predicting which peptides any given MHC class I allele will present is central to neoantigen vaccine design.

---

## 0:24 – 0:36 · The task

**Visual**: `fl03_ranking_task.png` (candidate peptides → model → ranked list).

**Narration**:

> Computationally, this is a **ranking problem**. Sort ten-thousand candidate peptides against one HLA allele, upstream of expensive experimental validation. We built DeepNeo-CL — a compact 35-million-parameter protein language model — to do that ranking.

---

## 0:36 – 0:48 · Problem 1 — leakage

**Visual**: `fl04_leakage_venn.png` (train/test Venn overlap).

**Narration**:

> But here's the catch. Most public benchmarks for this task overlap the training corpus of the industrial reference, NetMHCpan-4.1. We checked one widely-used holdout: 26.9% of its pairs were already in the training set. If you don't remove those, you're grading on the training data.

---

## 0:48 – 1:00 · Problem 2 — multiplicity

**Visual**: `fl05_multiplicity_holm.png` (4 TransPHLA comparisons pre/post Holm).

**Narration**:

> There's a second trap. On this benchmark we run four head-to-head tests between DeepNeo-CL and NetMHCpan-4.1 — BA head, EL head, deployed fusion, and a secondary control. If you report whichever one looks like a win without correcting across the family, you've cherry-picked. We predeclare **per-allele Wilcoxon tests, Holm-adjusted across all four comparisons**, with allele-clustered bootstrap confidence intervals.

---

## 1:00 – 1:12 · The honest result + case study

**Visual**: `fl06_transductive_collapse.png` (0.862 → 0.442 case study).

**Narration**:

> Under that contract, on 118,143 decontaminated TransPHLA pairs, DeepNeo-CL and NetMHCpan-4.1 **tie** at the fused score. NetMHCpan still holds a BA-head lead. And a second-stage rescorer that looked state-of-the-art at AUROC 0.862 collapses to 0.442 when honestly held out — a cautionary tale about transductive evaluation.

---

## 1:12 – 1:20 · End card

**Visual**: static end card — paper title, authors, pub-repo URL, QR code.

Layout:

```
┌───────────────────────────────────────────────┐
│  Efficient Protein Language Models for        │
│  Peptide–MHC Ranking                          │
│                                               │
│  A Leakage-Aware Evaluation Protocol under    │
│  Multiplicity Control                         │
│                                               │
│  Kevin Wang · Parma Nand                      │
│  Auckland University of Technology            │
│                                               │
│  github.com/KevinSimple/deepneo-pub           │
│  MDPI Information · 2026                      │
│                                               │
│            [QR code to pub repo]              │
└───────────────────────────────────────────────┘
```

No narration over end card — just a soft fade and the title card holds for 7 seconds, giving viewers time to scan the QR.

---

## Word count & timing audit

| Beat | Words | Target seconds @ 150 wpm | OK? |
|---|---|---|---|
| 0:00–0:12 (fl01) | 36 | 14.4 | ✅ (slight under-fill ok) |
| 0:12–0:24 (fl02) | 51 | 20.4 | 🟡 trim to 44 if read fast |
| 0:24–0:36 (fl03) | 44 | 17.6 | ✅ |
| 0:36–0:48 (fl04) | 52 | 20.8 | 🟡 trim to 44 if needed |
| 0:48–1:00 (fl05) | 51 | 20.4 | 🟡 trim to 44 |
| 1:00–1:12 (fl06) | 50 | 20.0 | ✅ |
| 1:12–1:20 end card | 0 | 8 | ✅ no narration |
| **Total** | **284** | **~122 s** | 🟡 **expected 90 s target — read at 190 wpm (brisk) or trim 20% per yellow beat** |

If the brisk 190 wpm pass still runs long, pre-trim option: drop the ", with allele-clustered bootstrap confidence intervals" clause in beat 5 and the ", a cautionary tale about transductive evaluation" clause in beat 6. That lands cleanly under 90 s.

---

## Vertical-crop version (YouTube Shorts)

Each FigureLab illustration is 16:9. For the 9:16 Shorts crop, use the right 70% of each illustration (which is where the cell / neural-net / Venn centre sits by design in all 6 prompts). Overlay a 60-pt sans-serif headline on the top 20% of the screen for each beat:

| Beat | Shorts headline (overlay) |
|---|---|
| 0:00 | **MHC class I displays peptides** |
| 0:12 | **Tumour cells present neoantigens** |
| 0:24 | **A ranking problem** |
| 0:36 | **Watch out: 26.9% leakage** |
| 0:48 | **Correct for 112 comparisons** |
| 1:00 | **Honest result: a tie** |
| 1:12 | **Full paper → pub repo** |

The narration audio is the same; only the headline overlay differs.
