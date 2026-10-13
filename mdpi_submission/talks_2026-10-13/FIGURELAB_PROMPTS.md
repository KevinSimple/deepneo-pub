# FigureLab prompts — 6 biology illustrations for the talk pack

**Target tool**: [figurelab.ai](https://figurelab.ai) (works for AI-biology-figure peers too — BioRender, Figshare, etc.).
**Shared style tokens** (paste into every prompt): *clean editorial scientific-illustration style, pastel accent palette (deep navy #0b4f8a + amber #ffb000 + sage #2e8540), minimal gradients, labelled, 300 dpi, 16:9 landscape unless stated, no stock-photo humans, no logos, no text in-image except the biology labels specified.*

Each prompt begins with a **filename** header. Save the FigureLab download under that exact name into `figures_input/` so the deck and trailer scripts find it.

---

## `fl01_mhc_presentation.png` — The MHC class I presentation pathway

**Where it's used**: Deck slide 2 ("The biology in 60 seconds"); Trailer beats 0:00–0:12 (opening hook).

**Prompt (paste into FigureLab)**:

> A single nucleated human cell shown in cutaway cross-section, filling the right 60% of the frame. Inside the cell: (1) a cytosolic protein being chopped by a **proteasome** (barrel-shaped complex) into short **peptide** fragments; (2) a peptide being transported through **TAP** (a two-component transmembrane transporter in the ER membrane) into the endoplasmic reticulum; (3) the peptide loading into an **MHC class I** molecule (α-chain + β2-microglobulin) in the ER; (4) the MHC-I/peptide complex trafficking via vesicle to the plasma membrane and displayed on the cell surface, holding the 8–11-residue peptide like a flag. Outside the cell, on the left: a **CD8+ T-cell** approaching, with a **T-cell receptor (TCR)** making contact with the surface MHC-I/peptide. Label every structure in small sans-serif text with a short leader line. Deep-navy outline on amber MHC-I molecules, sage T-cell. Pure white background. Editorial scientific-illustration style, no cartoonishness, no faces on the T-cell.

**Negative tokens**: cartoon, selfie, hospital, medical professional, textbook watermark, blurry.

---

## `fl02_normal_vs_cancer.png` — Normal vs tumour peptide display

**Where it's used**: Deck slide 3 ("Why it matters"); Trailer beat 0:12–0:24.

**Prompt**:

> Side-by-side comparison of two nucleated cells, same style as fl01 but simplified (no proteasome/TAP interior detail — surface only). **Left panel**: a healthy cell displaying MHC class I molecules on its surface, each holding a **green "self" peptide**. A CD8+ T-cell approaches and passes by without engaging (small arrow labelled "tolerated"). **Right panel**: a cancer cell with an irregular outline, displaying MHC class I molecules holding both green self-peptides AND **red neoantigen peptides** (from mutated or tumour-specific proteins). A CD8+ T-cell is docking onto one of the red neoantigen-presenting MHC-I complexes (small arrow labelled "cytotoxic recognition"). Label the two cells "healthy" and "tumour". Use the amber for MHC-I, green for self peptides, red for neoantigen peptides. Clean editorial style, pure white background.

**Negative tokens**: gore, blood, patient imagery, text overlays beyond the labels specified.

---

## `fl03_ranking_task.png` — The computational ranking task

**Where it's used**: Deck slide 4 ("What our model actually does"); Trailer beat 0:24–0:36.

**Prompt**:

> A clean flowchart in a left-to-right horizontal composition on 16:9 white background. **Left (input)**: a tall stacked list labelled "10²–10⁴ candidate peptides" rendered as a cloud of ~40 small chip-like shapes each holding a 9-letter amino-acid string ("SIINFEKL"-style, visually varied). **Centre (model)**: a single abstract neural-network block (just a stylised transformer silhouette — stacked rectangles labelled "ESM2 trunk") taking the peptides AND a single pseudo-sequence rectangle labelled "HLA pseudo-sequence (34 aa)" as inputs. **Right (output)**: the same ~40 chips now arranged as a vertical ranked list, with the top 5 highlighted in amber and labelled "top candidates for experimental validation". A dashed arrow from the top of the ranked list reaches a small wet-lab icon (an Eppendorf tube or MS instrument silhouette). Use navy, amber, sage palette. No photorealism. Editorial scientific illustration.

**Negative tokens**: realistic computer screens, cables, lab coats, hands.

---

## `fl04_leakage_venn.png` — Train/test leakage via public corpora

**Where it's used**: Deck slide 6 ("Problem 1: leakage"); Trailer beat 0:36–0:48.

**Prompt**:

> Two large overlapping circles in a Venn-style composition on white 16:9. **Left circle** (deep navy, 40% opacity fill, labelled above "NetMHCpan-4.1 training pairs — ~X million (peptide, HLA)"): filled with small blue dots representing peptide–HLA pairs. **Right circle** (amber, 40% opacity, labelled above "Author-reported holdout — n = 161,652"): filled with amber dots. **Overlap region** (large, labelled in red "leakage region — 26.9% exact match"): dots in the overlap are rendered as half-blue-half-amber. Below the Venn, a horizontal arrow pointing out of the overlap to the right, labelled "removed by exact (peptide, HLA) decontamination", pointing to a smaller circle labelled "clean subset n = 118,143". Minimalist, editorial, no stock imagery.

**Negative tokens**: data-breach imagery, padlocks, hackers, generic cybersecurity visuals.

---

## `fl05_multiplicity_holm.png` — Holm family-wise correction across the 4 Table 2 comparisons

**Where it's used**: Deck slide 7 ("Problem 2: multiple testing"); Trailer beat 0:48–1:00.

**IMPORTANT (corrected 2026-10-14)**: The paper's Holm family is **4** (the four TransPHLA Table 2 comparisons), **not 112 alleles**. The 112-ish alleles are the sample for the per-allele Wilcoxon test *within* each row; that test rolls up to one p-value per row, and Holm acts on the four resulting p-values. An earlier version of this prompt incorrectly specified Holm across 112 alleles and produced an image with p-values > 1.0 (mathematically impossible — Holm's formula clips at 1).

**Prompt**:

> A 16:9 white editorial-illustration canvas showing exactly **four** horizontal comparison bars arranged in two stacked rows (not 112). The four bars represent the paper's four TransPHLA Table 2 comparisons:
>
> ① "v4.1 fus vs fus" · ② "v4.1 BA vs NMP BA" · ③ "v4.1 EL vs NMP EL" · ④ "v4.1 deployed fus vs NMP BA"
>
> **Top row header**: "Per-allele Wilcoxon p-values (raw)" — bars labelled with:
> ① p = 0.253 (grey) · ② p = 0.00042 (amber) · ③ p = 0.386 (grey) · ④ p = 0.050 (amber, borderline)
>
> **Between the rows**: a downward sage/navy arrow labelled "Holm family-wise correction (family size m = 4 comparisons)".
>
> **Bottom row header**: "Holm-adjusted p-values" — bars labelled with:
> ① p = 0.505 (grey) · ② p = 0.0017 (amber) · ③ p = 0.505 (grey) · ④ p = 0.151 (grey)
>
> Takeaway caption at the bottom in small text: "Only the NetMHCpan BA-head advantage (Δ = −0.0137) survives Holm correction across the family of 4 TransPHLA comparisons."
>
> **CRITICAL math constraint**: Holm's formula is `min(p × k, 1)`. Every Holm-adjusted p-value MUST be ≤ 1.000. Never show p > 1. All four Holm values above are already correct and bounded.
>
> Clean editorial scientific-illustration style, navy outlines, amber fill for significant bars, grey fill for non-significant, pure white background. No stock graphs, no Excel UI, no bell curves. Do NOT show per-allele breakdown (do not show 112 or 84 alleles — that structure rolls up into each row's Wilcoxon p via rank test, which happens upstream and is not depicted here).

**Negative tokens**: Excel UI, generic statistics stock images, bell curves, 112 bars, per-allele chips, p-values greater than 1.

---

## `fl06_transductive_collapse.png` — The 0.862 → 0.442 case study

**Where it's used**: Deck slide 9 ("Case study — a cautionary tale"); Trailer beat 1:00–1:12.

**Prompt**:

> A clean before/after comparison on 16:9 white. **Left panel ("Fitted on the eval set — looks great")**: a small AUROC bar chart with one amber bar reaching 0.862, labelled "pocket rescorer, 5-fold CV on IEDB BA eval set". A thought-bubble above it reads "SOTA?". **Right panel ("Deployed held-out — collapses")**: the same bar chart but the amber bar is now at 0.442, which is **below** a dashed horizontal line labelled "chance = 0.5". A thought-bubble above it reads "below chance". A large curved arrow sweeps from left panel to right panel, labelled "same model, now applied inductively to held-out alleles". Below both panels, a one-sentence takeaway in small text: "transductive CV on the evaluation set is not a benchmark." Deep-navy accent, amber bars, red for the "below chance" line. Minimalist editorial.

**Negative tokens**: emoji, cartoon faces, generic shock reactions, stock images of warnings or sirens.

---

## Quality-check pass before using any output

For every illustration FigureLab returns:

1. **Vocabulary audit** — the labels in the image must say *peptide*, *HLA*, *MHC class I*, *CD8+ T-cell*, *TCR*, *proteasome*, *TAP*. No "antigen-presenting molecule" vagueness, no made-up acronyms.
2. **Biology audit** — MHC class I presents to CD8+ T-cells, never CD4+. Peptides are 8–11 residues (never longer in this paper's scope). Proteasome is cytosolic, TAP is in the ER membrane. If any of these is reversed in the output, discard and re-prompt.
3. **Palette audit** — amber for MHC-I, green for self-peptides, red for tumour/neoantigen, navy for T-cells. Consistent across all 6 so the deck feels like one asset family.
4. **No-text audit** — the illustration must not have hallucinated extra text (titles, equations, URLs). The deck will overlay all headlines; the illustration carries only the biology labels specified.

If FigureLab refuses or produces something unusable, fall back order:
1. BioRender manual build using the same brief
2. Hand-drawn in Figma using the biology-vocabulary audit above
3. OpenArt/Midjourney with cinematic style (lower biology fidelity but still usable for the trailer)
