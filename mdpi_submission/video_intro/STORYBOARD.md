# Video Storyboard — DeepNeo-CL intro (3:45)

Scene-by-scene production guide mapping narration, slides, figures, and B-roll for the video editor.

---

## Scene 1 — HOOK (0:00 – 0:15)

| Element | Detail |
|---|---|
| **Slide** | #1 — Title card (DeepNeo-CL, authors, venue) |
| **Narration** | "Imagine your body as a city of billions of cells..." |
| **Visual notes** | Hold title 2 s → transition to slide 2 at ~0:05. Consider B-roll Clip 1 (cell/MHC animation) as background for 0:05–0:15 while narrating the biology hook. |
| **Transition** | Fade / dissolve into slide 2 |

---

## Scene 2 — WHY IT MATTERS (0:15 – 0:45)

| Element | Detail |
|---|---|
| **Slide** | #2 — "A central problem in computational immunology" |
| **Narration** | "That inspection process is run by MHC class I proteins..." |
| **Key visual** | Inline SVG diagram (MHC presenting peptide → T-cell detection). Animate or pan slowly across the 3 numbered steps. |
| **B-roll option** | Clip 1 (MHC/T-cell microscopic view) can overlay 0:15–0:20 |
| **Transition** | Cut to slide 3 |

---

## Scene 3 — FRAMING AS ML (0:45 – 1:10)

| Element | Detail |
|---|---|
| **Slide** | #3 — "Computationally, this is a sequence-ranking problem" |
| **Narration** | "In our paper, we approach this as a machine-learning problem..." |
| **Key visual** | **fig_data_flow.png** — the full pipeline diagram (training corpora → model → decontamination → benchmarks). Zoom in or pan right across the figure. |
| **Highlight** | When narration says "ten-thousand candidate peptides, one HLA allele", highlight the Input/Output card. |
| **Transition** | Cut to slide 4 |

---

## Scene 4 — MODEL (1:00 – 1:10)

| Element | Detail |
|---|---|
| **Slide** | #4 — "DeepNeo-CL — a compact PLM for pMHC-I ranking" |
| **Narration** | "We built DeepNeo-CL — a compact transformer, 35 million parameters..." |
| **Key visuals** | 8-row architecture table (left) + **fig_training_dynamics.png** (right). Brief hold — this slide is on screen for ~10 s. |
| **Highlight** | Accent the "35 M" big number. |
| **Transition** | Cut to slide 5. Consider B-roll Clip 2 (data streams) as a 2 s transition. |

---

## Scene 5 — THE PROBLEM (1:10 – 2:05)

| Element | Detail |
|---|---|
| **Slide** | #5 — "Why reported gains in this field are hard to trust" |
| **Narration** | "But the paper isn't really about the model. It's about how we evaluate." + "Here's the problem..." |
| **Key visuals** | Two red cards (leakage + multiple testing) + **fig_contamination_ledger.png** (bottom). Slow zoom into the contamination chart when narration mentions "share rows" and "26.9%". |
| **B-roll option** | Clip 2 (data contamination streams) for the 1:30–1:32 transition moment. |
| **Pacing** | This is the longest narration block (55 s). Let the slide breathe — no rapid cuts. |
| **Transition** | Cut to slide 6 |

---

## Scene 6 — OUR PROTOCOL (2:05 – 2:25)

| Element | Detail |
|---|---|
| **Slide** | #6 — "The three-condition superiority rule" |
| **Narration** | "So we did two things. We removed every shared training pair..." |
| **Key visual** | Three numbered conditions (DeLong, Holm-Wilcoxon, Bootstrap CI) + blue decontamination card. Build in the 3 items sequentially if possible (1→2→3 with 2 s delay). |
| **Transition** | Cut to slide 7 on "Here's what happens under that honest protocol." |

---

## Scene 7 — HEADLINE RESULT (2:25 – 2:45)

| Element | Detail |
|---|---|
| **Slide** | #7 — "Decontaminated TransPHLA" |
| **Narration** | "On the TransPHLA benchmark — 118-thousand clean rows..." |
| **Key visuals** | Table 1 results (left) + **fig_roc_pr_decontam.png** (right). The ROC/PR curves show the overlapping performance visually — the lines are nearly on top of each other. |
| **Highlight** | Flash the green "TIED" verdict cell when narration says "Not better, not worse. Matched." |
| **Transition** | Cut to slide 8 |

---

## Scene 8 — IEDB WEEKLY (2:45 – 3:05)

| Element | Detail |
|---|---|
| **Slide** | #8 — "IEDB auto_bench weekly" |
| **Narration** | "On the IEDB weekly leaderboard — 14 predictors scored over 46 weeks..." |
| **Key visuals** | **fig_weekly_ranking_ba.png** (top-left) + **fig_weekly_head2head_ba.png** (bottom-left) + stat cards (right). Pan across the ranking chart to show DeepNeo at 6.85. |
| **Highlight** | Green EL board card when narration says "we lead the three-predictor eluted-ligand board." |
| **Transition** | Cut to slide 9 |

---

## Scene 9 — HONEST REPORTING (3:05 – 3:15)

| Element | Detail |
|---|---|
| **Slide** | #9 — "Where NetMHCpan still wins" |
| **Narration** | "NetMHCpan still beats us on the pure binding-affinity head..." |
| **Key visuals** | Red card with the BA-head numbers (left) + **fig_holm_family.png** forest plot (right). The forest plot shows the blue dot (BA head) as the only comparison whose CI excludes zero. |
| **Pacing** | Short scene (10 s). Let the honest admission land. |
| **Transition** | Cut to slide 10 |

---

## Scene 10 — CASE STUDY (3:15 – 3:35)

| Element | Detail |
|---|---|
| **Slide** | #10 — "A documented transductive-overfitting failure" |
| **Narration** | "And here's the most interesting failure..." |
| **Key visual** | The mega-number display: **0.862 → 0.442**. This is the money shot of the video. |
| **Pacing** | SLOW DOWN on the two numbers. Let the dramatic drop sink in. Pause 1 s between "0.862" and "dropped to 0.442". |
| **Highlight** | Green → red color shift on the numbers. Consider a brief zoom or scale animation on the arrow. |
| **Transition** | Cut to slide 11 |

---

## Scene 11 — TAKEAWAY (3:35 – 3:40)

| Element | Detail |
|---|---|
| **Slide** | #11 — "What this paper actually claims" |
| **Narration** | "The takeaway: a compact protein language model can rank..." |
| **Key visual** | Three-column cards (Model / Protocol / Negatives). Brief hold — 5 s. |
| **Transition** | Cut to slide 12 |

---

## Scene 12 — CTA (3:40 – 3:45)

| Element | Detail |
|---|---|
| **Slide** | #12 — "Where to find the paper, code, and evidence" |
| **Narration** | "Code and benchmark results at github.com/KevinSimple/deepneo-pub. Paper under review at MDPI Information. Thanks for watching." |
| **Key visual** | Paper info (left) + GitHub link (right). |
| **B-roll option** | Clip 3 (zooming out from cell to network) as background loop. |
| **End card** | Hold slide 12 for 3 s after narration ends. Add YouTube end screen elements (subscribe, next video) in the final 5 s if desired. |

---

## Figures used in deck (summary)

| Slide | Figure file | What it shows |
|---|---|---|
| 3 | `fig_data_flow.png` | End-to-end pipeline: training → model → decontamination → benchmarks |
| 4 | `fig_training_dynamics.png` | Loss curves and validation AUROC across epochs |
| 5 | `fig_contamination_ledger.png` | Training-set membership overlap per benchmark |
| 7 | `fig_roc_pr_decontam.png` | ROC and PR curves on decontaminated TransPHLA |
| 8 | `fig_weekly_ranking_ba.png` | IEDB weekly leaderboard: mean rank + rank-1 counts |
| 8 | `fig_weekly_head2head_ba.png` | DeepNeo vs NMP-4.1: win/tie/loss breakdown + rank-1 |
| 9 | `fig_holm_family.png` | Forest plot: Δ AUROC with 95% CI and Holm p-values |

## Figures available but not in deck

| Figure file | Potential use |
|---|---|
| `fig07_ablation_grid.png` | Ablation study — could add as bonus slide |
| `fig_S1_calibration.png` | Calibration plot — supplementary |
| `fig_per_length_decontam.png` | Per-peptide-length decontamination — supplementary |
| `fig_pooled_h2h_ba.png` | Pooled head-to-head bar chart — alternative to forest plot |
| `fig_rare_allele.png` | Rare allele performance — could add as bonus slide |
| `fig_weekly_paired_scatter.png` | Weekly paired scatter — alternative IEDB viz |

---

## Production checklist

- [ ] Record narration (7 blocks, ~525 words)
- [ ] Screen-record slides in Chrome fullscreen (arrow-key advance)
- [ ] Generate B-roll clips (3 prompts in OPENART_PROMPTS.md) — optional
- [ ] Sync narration to slide transitions in editor
- [ ] Add captions (upload captions.srt to YouTube)
- [ ] Pick thumbnail (recommend option 2 — "0.862 → 0.442" number hook)
- [ ] Export 1080p H.264 MP4
- [ ] Upload to YouTube with title, description, tags
