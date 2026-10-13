# Talk pack — DeepNeo-CL · MDPI *Information* submission (Oct 2026)

Conference-style deck (~12 min) + 60–90 s short trailer, sharing a single family of 6 FigureLab-generated biology illustrations. Both deliverables target a **CS audience that needs real-but-accessible biology context** (correct vocabulary, glossary tooltips, no hand-wave analogies).

## Files

| File | Purpose | Status |
|---|---|---|
| `FIGURELAB_PROMPTS.md` | 6 publication-quality biology-illustration briefs for figurelab.ai. Each is paste-ready; each is cross-referenced to the deck slide and trailer beat that consumes it | ✅ ready |
| `TRAILER_SCRIPT.md` | 90-second narration script with timing marks. Written against the 6 FigureLab illustrations as background plates | ✅ ready |
| `DECK_OUTLINE.md` | 15-slide outline (title + 14) with speaker notes, timings, and figure/illustration cross-refs for a 10–12 min conference talk | ✅ ready |
| `figures_input/` | Drop FigureLab outputs here as `fl01_mhc_presentation.png`, `fl02_normal_vs_cancer.png`, … (filenames fixed in the prompts) | 📂 awaiting outputs |
| `figures_paper/` | Symlinked/copied real paper figures (ROC/PR, decontam ledger, head-to-head bars) that round out the deck | 📂 to populate |

## Usage order (fastest path)

1. **FigureLab (20 min)** — open [figurelab.ai](https://figurelab.ai), paste the 6 prompts from `FIGURELAB_PROMPTS.md` one at a time, download each as PNG at the filename given in the prompt header, drop into `figures_input/`.
2. **Record trailer narration (10 min)** — read `TRAILER_SCRIPT.md` into any voice recorder. 90 seconds total.
3. **Build the deck (45 min)** — follow `DECK_OUTLINE.md` slide by slide in your tool of choice (PowerPoint, Keynote, or extend the existing [`../video_intro_2026-10-06/slides.html`](../video_intro_2026-10-06/slides.html)). Each slide specifies: title, headline, visual, speaker-note, timing.
4. **Assemble trailer (20 min)** — Descript or iMovie: 6 illustration plates with narration over them + a 2-sec end card.

## Audience-tuning rules (binding — the same ones applied to the paper)

- Real biology vocabulary (peptide, HLA, MHC class I, cross-presentation, T-cell receptor). Glossary tooltip or on-slide sidebar for first use.
- **No "analogy wash"**: do NOT reduce MHC to "a type system" or peptide ranking to "a search engine". Those metaphors are inaccurate and reviewers will notice.
- Every numeric claim must trace to the frozen set below.
- Honest-tie framing throughout: NetMHCpan-4.1 is the comparator we match, not beat. "DeepNeo-CL BA = fusion" always (never "fusion vs BA head" as separate rows).

## Frozen numbers (do not change)

| Claim | Value | Source |
|---|---|---|
| TransPHLA decontam-rescore fusion vs fusion | 0.9573 vs 0.9575 (Δ = −0.0002, Tied) | SI `transphla_rescored_fusion_fixed.json` |
| NetMHCpan BA-head retains lead | Δ = −0.0137, Wilcoxon p = 7.2×10⁻⁴, Holm 1.7×10⁻³ | SI `table2_holm_adjusted.json` |
| IEDB weekly BA rank | 6.85 / 14 | SI `weekly_ranking_v41_2020_2026_singlecol_v2.json` |
| EL panel mean rank | 1.80 (3-predictor MS-EL board) | SI (same) |
| Decontaminated n | 118,143 (from 161,652; 43,509 removed; 26.9%) | SI `transphla_decontam_vs_42.json` |
| Transductive-fit case study | 0.862 (in-sample) → 0.442 (held-out) | SI `inductive_reranker_result.json` |
| ECE | 0.091 (DeepNeo) vs 0.202 (NetMHCpan-4.1) | SI `fig_S1_calibration.pdf` |
| Successor-corpus overlap case study | 99.93% of author-constructed holdout inside NetMHCpan-4.2 training pairs | SI `iedb_holdout_nmp42_overlap.json` |

## Not for this pack

- No clinical efficacy claims
- No MHC class II / TCR specificity claims
- No "best model" / "state of the art" / ">10σ" / "superior to MHCflurry" wording (all withdrawn 2026-07-14 per DEPLOYMENT-SAFE FREEZE)
- No pocket-rescorer deployment claims (withdrawn — the 0.862 is the in-sample headline of a cautionary case study, not a result)
