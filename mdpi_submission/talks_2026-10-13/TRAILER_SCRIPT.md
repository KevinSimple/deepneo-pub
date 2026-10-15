# Trailer script — DeepNeo-CL · 90 seconds

Target: short promo for the MDPI *Information* submission. YouTube Shorts (vertical crop), Twitter/X (16:9), pub-repo README banner.

**Honest-tier framing** (binding — matches the paper's actual value tier):
- Lead with the **real** findings (26.9% leakage ledger, calibration, SI evidence pack)
- Headline the fusion match as a **tie**, not a win
- De-emphasize the two case studies — they're not novel findings, they're concrete ledgers for known traps

**Visual plates**: 4 FigureLab plates (fl01, fl02, fl04, fl06) + 2 real paper figures (fig_S1_calibration, fig_roc_pr_decontam) + end card.

**Pacing**: 90 s total. Narration deliberately under-fills so the images breathe.

---

## 0:00 – 0:12 · The biology (what the paper is about)

**Visual**: `fl01_mhc_presentation.png` (MHC class I presentation pathway).

**Narration**:

> Every cell in your body displays short protein fragments — **peptides** — on its surface, bound to a molecule called **MHC class I**. This is how CD8+ T-cells know what's happening inside the cell.

---

## 0:12 – 0:22 · Why we care computationally

**Visual**: `fl02_normal_vs_cancer.png` (healthy vs tumour display).

**Narration**:

> Tumour cells display **neoantigens** — mutation-derived peptides. Predicting which peptides a given HLA allele will present is central to neoantigen vaccine design. The industry reference is **NetMHCpan-4.1**.

---

## 0:22 – 0:38 · The real finding — 26.9% leakage

**Visual**: `fl04_leakage_venn.png` (train/test Venn).

**Narration**:

> We built DeepNeo-CL on NetMHCpan's own folds and compared on the TransPHLA holdout. **Then we checked for leakage** — and found **26.9 percent** of the holdout was already in the training set. Forty-three thousand five hundred and nine pairs removed. Every number in the paper is on the clean subset: **n = 118,143**.

---

## 0:38 – 0:52 · The honest headline — a tie

**Visual**: `figures_paper/png/fig_roc_pr_decontam.png` (ROC + PR on decontaminated TransPHLA).

**Narration**:

> On the clean subset, under exact decontamination plus **Holm-adjusted** per-allele tests, DeepNeo-CL and NetMHCpan-4.1 **tie** at the fused score — 0.9573 versus 0.9575. NetMHCpan keeps the BA-head lead. We report both. We don't claim a win.

---

## 0:52 – 1:06 · The quiet win — calibration

**Visual**: `figures_paper/png/fig_S1_calibration.png` (reliability diagram).

**Narration**:

> One thing DeepNeo-CL actually wins cleanly: **calibration**. On the TransPHLA EL set, expected calibration error 0.091 versus 0.202 — less than half NetMHCpan's. Nobody else has reported calibration on this benchmark. Matters practically for anyone thresholding scores in a vaccine pipeline.

---

## 1:06 – 1:20 · The evidence pack + end card

**Visual**: static end card (title + authors + QR + pub-repo link); overlay the three "receipts" bullets briefly at 1:06-1:12.

**Narration**:

> **Every substantive numeric claim** in the paper traces to one of **17 public SI JSON ledgers**. A committed audit script shows 43 of 43 headline-claim checks match. Reviewers can re-check every digit. Full paper and evidence pack: in the link below.

Then fade to end card and hold 4-6 seconds for QR scan.

---

## Word count & timing audit

| Beat | Words | Target seconds @ 180 wpm | OK? |
|---|---|---|---|
| 0:00–0:12 (fl01)             | 32 | 11 | ✅ |
| 0:12–0:22 (fl02)             | 31 | 10 | ✅ |
| 0:22–0:38 (fl04 leakage)     | 48 | 16 | ✅ |
| 0:38–0:52 (ROC/PR tie)       | 42 | 14 | ✅ |
| 0:52–1:06 (calibration)      | 42 | 14 | ✅ |
| 1:06–1:20 (ledger + end card)| 38 | 13 | ✅ (fade pad = 1s) |
| **Total**                    | **233** | **~78 s** | ✅ brisk @ 180 wpm fits 90 s with pads |

---

## Vertical-crop version (YouTube Shorts)

Each FigureLab plate and paper figure is 16:9. For 9:16 Shorts crop, use the centre 60% of each image (which is where the main content sits in all 6 plates). Overlay a 60-pt sans-serif headline on the top 20% of the screen for each beat:

| Beat | Shorts headline (overlay) |
|---|---|
| 0:00 | **MHC class I displays peptides** |
| 0:12 | **Predicting neoantigens** |
| 0:22 | **26.9% leakage: exposed** |
| 0:38 | **Honest result: a tie** |
| 0:52 | **The quiet win: ½ the calibration error** |
| 1:06 | **17 SI JSON ledgers · committed audit script · all public** |

---

## What changed from the earlier draft

**Dropped from the 90 s cut:**
- The 0.862 → 0.442 transductive-collapse beat (compressed to one line in the ledger beat if space allows — or omitted entirely from the 90 s)
- The ranking-task beat (saved words for the real findings)
- The multiplicity/Holm beat (folded into the "under exact decontamination plus Holm-adjusted" line in the headline beat)

**Promoted to the 90 s cut:**
- Calibration (previously only in the extended cut — this is probably the paper's strongest finding and was buried)
- The SI evidence pack (previously only in cover-letter prose — this is a real contribution to the sub-field)

**Honest-tie framing stays:** no "beats NetMHCpan". The 0.9573 vs 0.9575 tie is the headline.
