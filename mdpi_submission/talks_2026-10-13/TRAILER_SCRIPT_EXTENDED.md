# Extended trailer script — DeepNeo-CL · 2:30 explainer

Target: longer-form explainer for YouTube main-feed, Twitter long-form, LinkedIn posts, pub-repo landing-page embed, and the MDPI SI promo. CS audience; real biology vocabulary; more breathing room than the 90-second cut.

**Companion**: the 90 s cut lives in `TRAILER_SCRIPT.md` and remains the Shorts/Twitter version.

**Visual family (shared with the 90 s cut, 2 new asset types added)**:
- 🧬 Six FigureLab plates `fl01`–`fl06` (same as 90 s cut; see `FIGURELAB_PROMPTS.md`)
- 📊 Three real paper figures: `latex/figures/fig_data_flow.pdf` · `latex/figures/graphical_abstract.svg` (middle panel) · `latex/figures/fig_pooled_h2h_ba.pdf`
- 🖼 Three static text slides (built in Keynote/PowerPoint, 1920×1080): **Pipeline card** · **Architecture card** · **Honest-tie card**

**Pacing**: 10 beats across 2:30, roughly 12–18 s per beat. Narration runs ~180 words/min (brisk-but-natural) at a target of ~400 total words.

---

## 0:00 – 0:15 · The biology opener

**Visual**: 🧬 `fl01_mhc_presentation.png` (full-frame, slow Ken-Burns zoom from the T-cell inward to the MHC-I/peptide complex on the cell surface).

**Narration** (~45 words):

> Every nucleated cell in your body is constantly chopping its own proteins into short fragments — **peptides** — and displaying them on its surface, bound to a molecule called **MHC class I**. This is how CD8+ T-cells know what's happening inside a cell they can't see into.

---

## 0:15 – 0:30 · Why it matters (healthy vs tumour)

**Visual**: 🧬 `fl02_normal_vs_cancer.png` (crossfade from fl01 at 0:15; hold both panels side-by-side).

**Narration** (~40 words):

> Healthy cells present **self peptides**, and the immune system ignores them. Tumour cells also present **neoantigens** — fragments of mutated or abnormal proteins. If a CD8+ T-cell sees a neoantigen on an MHC class I molecule, it kills the cell.

---

## 0:30 – 0:45 · Where this prediction sits in cancer-vaccine design

**Visual**: 🖼 **Pipeline card** — a static slide showing a 5-stage horizontal flow:
`① Patient tumour DNA/RNA-seq  →  ② Mutation calls  →  ③ Candidate peptides  →  ④ MHC-presentation prediction (DeepNeo-CL)  →  ⑤ Peptide/mRNA vaccine`
Stage ④ highlighted in amber with a subtle "you are here" caret.

**Narration** (~45 words):

> Here's where machine learning enters. Personalised cancer-vaccine pipelines sequence a patient's tumour, call the mutations, generate a list of candidate neoantigen peptides, and then need to predict which ones the patient's HLA alleles will actually present. That upstream prediction is what DeepNeo-CL does.

---

## 0:45 – 1:00 · The task, formally

**Visual**: 🧬 `fl03_ranking_task.png` (candidate peptides → model → ranked list).

**Narration** (~40 words):

> Computationally, this is a **ranking problem**. Take ten-thousand candidate peptides, score each one against one HLA allele, and sort — the top of the list goes to expensive experimental validation. The output has two heads: binding affinity, and eluted-ligand presentation probability.

---

## 1:00 – 1:15 · The model, briefly

**Visual**: 📊 Middle panel of `latex/figures/graphical_abstract.svg` (ESM2 trunk → cross-attention → BA + EL heads → 5-fold ensemble). Alternatively `latex/figures/fig_data_flow.pdf` cropped to the model block.

**Narration** (~45 words):

> DeepNeo-CL is deliberately compact: a 35-million-parameter protein language model, ESM2, as the trunk, with one cross-attention layer letting each peptide position attend over the HLA's binding-pocket pseudo-sequence. Two heads, trained as a five-fold ensemble on the official NetMHCpan-4.1 folds.

---

## 1:15 – 1:30 · Problem 1 — leakage via a shared public corpus

**Visual**: 🧬 `fl04_leakage_venn.png`.

**Narration** (~50 words):

> But here's the first catch. Most public benchmarks for this task overlap NetMHCpan-4.1's own training corpus. On one widely-used holdout we checked, **26.9 percent** of the pairs were already in the training set. If you don't remove them, you're grading on the training data — and every PLM looks state-of-the-art.

---

## 1:30 – 1:45 · Problem 2 — multiplicity across 112 alleles

**Visual**: 🧬 `fl05_multiplicity_holm.png`.

**Narration** (~45 words):

> The second catch. The benchmark covers 112 HLA alleles. Report one pooled "win" without correcting for the 112 comparisons and random noise alone will manufacture about six wins at α = 0.05. We predeclare Holm-adjusted per-allele Wilcoxon tests, with allele-clustered bootstrap confidence intervals.

---

## 1:45 – 2:00 · The honest result

**Visual**: 🖼 **Honest-tie card** — large text slide:
```
On decontaminated TransPHLA (n = 118,143)

DeepNeo-CL fusion         0.9573
NetMHCpan-4.1 fusion      0.9575
                           Δ = −0.0002  Tied

NetMHCpan-4.1 BA-head keeps a Holm-robust Δ = −0.0137 lead.
```
Palette: navy headline on white, amber for DeepNeo row, sage for NetMHCpan.

**Narration** (~45 words):

> Under that honest contract, on 118,143 decontaminated TransPHLA pairs, DeepNeo-CL and NetMHCpan-4.1 **tie** at the fused score we deploy. NetMHCpan keeps a small but Holm-robust lead on the BA head. We report both, and we don't claim a win.

---

## 2:00 – 2:15 · The cautionary case study

**Visual**: 🧬 `fl06_transductive_collapse.png`.

**Narration** (~45 words):

> One cautionary tale we think the field needs. We fitted a second-stage pocket rescorer with cross-validation on the IEDB BA evaluation set. CV AUROC: 0.862 — looks state-of-the-art. When we deployed it to held-out alleles: 0.442, **below chance**. Transductive CV on the evaluation set is not a benchmark.

---

## 2:15 – 2:30 · Takeaway + end card

**Visual**: 🖼 Static end card (same layout as the 90 s cut):

```
Efficient Protein Language Models for
Peptide–MHC Ranking

A Leakage-Aware Evaluation Protocol under
Multiplicity Control

Kevin Wang · Parma Nand
Auckland University of Technology

github.com/KevinSimple/deepneo-pub
MDPI Information · 2026

[QR code to pub repo]
```

**Narration** (~30 words, delivered calmly before the fade):

> The paper's main contribution isn't a bigger model — it's an evaluation contract portable to any shared-corpus ranking task. Full paper, evidence ledgers, and compliance pack: in the link below.

Then fade to end card and hold 7 s with no narration (QR scan time).

---

## Word count & timing audit

| Beat | Words | Target seconds @ 180 wpm | OK? |
|---|---|---|---|
| 0:00–0:15 (fl01)                            | 45 | 15 | ✅ |
| 0:15–0:30 (fl02)                            | 40 | 13 | ✅ (2 s pad) |
| 0:30–0:45 (🖼 Pipeline card)                | 45 | 15 | ✅ |
| 0:45–1:00 (fl03)                            | 40 | 13 | ✅ (2 s pad) |
| 1:00–1:15 (📊 architecture)                 | 45 | 15 | ✅ |
| 1:15–1:30 (fl04)                            | 50 | 17 | 🟡 trim to 45 if read fast |
| 1:30–1:45 (fl05)                            | 45 | 15 | ✅ |
| 1:45–2:00 (🖼 Honest-tie card)              | 45 | 15 | ✅ |
| 2:00–2:15 (fl06)                            | 45 | 15 | ✅ |
| 2:15–2:30 (🖼 end card + QR hold)           | 30 | 10 | ✅ (fade pad = 5 s silence) |
| **Total**                                   | **430** | **~143 s** | 🟡 **expected 150 s target — read briskly at 180 wpm or trim 1-2 words/beat** |

If the brisk pass still overshoots, pre-trim option: drop "and every PLM looks state-of-the-art" from beat 6, and "about six wins at α = 0.05" from beat 7. Lands cleanly under 2:30.

---

## Shot list / editor notes

**Pacing rules (binding — the audience is CS, they don't want the biology hand-wavy):**

- Each FigureLab plate held full-screen with slow Ken-Burns (10–15% zoom over its beat). No fast cuts in biology sections.
- Text cards (pipeline / honest-tie / end card) stay static — no animation. Let the viewer read.
- `fig_data_flow.pdf` or the architecture panel can have a subtle highlight-sweep over the three blocks (ESM2 → cross-attention → heads) across its 15 s.
- Transitions: 0.3 s crossfade between every beat. No swipes, no slides, no cute animations.
- Caption / subtitle: hard-burn captions for YouTube silent-autoplay audiences. Font: SF Pro / Inter, 36 pt white on 60%-opacity navy bar at the bottom 15% of the frame.

**Audio:**

- Narration recorded in one take per beat (10 clips). Compile in Descript / Audacity.
- Background music: ambient / minimal (no bed drops, no risers). −18 LUFS integrated, duck under narration to −24 LUFS. Example matches: "Kiasmos — Blurred", "Nils Frahm — Says", or any royalty-free piano-pad from Epidemic Sound / Pixabay Music.
- Final mix: narration peaks at −6 dBFS; bed at −24 dBFS integrated.

**Deliverables from the edit:**

| File | Spec | Target home |
|---|---|---|
| `trailer_extended_1080p.mp4` | 1920×1080, 24 fps, H.264, ≤ 200 MB | YouTube main-feed, LinkedIn |
| `trailer_extended_square.mp4` | 1080×1080 centre-crop, same length | Twitter, LinkedIn embed |
| `trailer_extended_captions.srt` | WebVTT also acceptable | YouTube caption upload |
| `trailer_90s.mp4` (from the 90 s cut) | 1920×1080 and 1080×1920 Shorts versions | YouTube Shorts, Twitter |

---

## Where this file sits in the pack

- `README.md` — orchestration (unchanged)
- `FIGURELAB_PROMPTS.md` — the 6 biology-illustration briefs (unchanged; this script re-uses all 6)
- `TRAILER_SCRIPT.md` — the 90 s Shorts/Twitter cut (unchanged, still the primary short version)
- **`TRAILER_SCRIPT_EXTENDED.md`** — this file, 2:30 explainer cut
- `DECK_OUTLINE.md` — the 15-slide conference talk outline (unchanged)

No paper content touched. No new biology scenes introduced — the 2 new "card" slides are static text + the real paper architecture figure, consistent with the pack's stated visual family.
