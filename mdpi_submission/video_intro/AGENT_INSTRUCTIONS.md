# Agent instructions — slide deck content workflow

> **For**: a cloud agent (Claude Code, Cursor, Codex, etc.) working in this folder.
> **Goal**: regenerate or update the slide deck content while preserving quantitative integrity.

---

## Prerequisites

Before starting, confirm you have access to:
- `slides.html` — the self-contained 12-slide HTML deck
- `PROMPT_FOR_CONTENT_AI.md` — the content-generation prompt with frozen ground truth
- `NARRATION_SCRIPT.md` — the 525-word narration script (7 time-blocked sections)
- `YOUTUBE_METADATA.md` — YouTube upload fields
- `captions.srt` — 26-entry SRT caption file
- `../evidence/supplementary_data/*.json` — SI JSON ledgers (source of truth for all numbers)
- `../evidence/CLAIM_EVIDENCE_TABLE.md` — 515-claim evidence audit

---

## 5-step workflow

### Step 1: Generate content blocks

Feed `PROMPT_FOR_CONTENT_AI.md` verbatim to a content-generation model. The prompt is self-contained: it encodes all paper ground truth, scope restrictions, tone rules, and audience definition.

**Expected output**: 11 markdown blocks (slides 2–12), each with a key claim, supporting text, data points, and narration cue.

### Step 2: Integrate into `slides.html`

Edit `slides.html` directly. The deck is one self-contained HTML file.

Rules:
- Preserve the existing CSS design system (variables, classes, layout patterns)
- Preserve the 12-slide structure and section tags
- Preserve inline SVG diagrams — they are hand-tuned and should not be regenerated
- Preserve figure references in `figures/` — if you change a figure path, verify the file exists
- Keep the progress bar, footer, section-tag, and keyboard-navigation JS untouched
- Use the existing card classes: `.card-navy`, `.card-accent`, `.card-green`, `.card-red`

### Step 3: Sanity-check every number

Cross-check every quantitative claim in the updated deck against the SI JSON ledgers:

| Slide | Numbers to verify | Ledger file |
|---|---|---|
| 7 | Table 1 AUROCs, Δ, verdicts, Holm p, bootstrap CI | `transphla_rescored_fusion_fixed.json` + `table2_holm_adjusted.json` + `paired_bootstrap_ci.json` |
| 8 | Mean rank, AUROC, rank-1 counts, head-to-head W/T/L | `weekly_ranking_v41_2020_2026_singlecol_v2.json` |
| 9 | BA-head Δ = −0.0137, Holm p = 1.7×10⁻³, CI bounds | `table2_holm_adjusted.json` + `paired_bootstrap_ci.json` |
| 10 | Rescorer 0.862 → 0.442 | `inductive_reranker_result.json` |

**If any number does not match, do not commit.** Fix the discrepancy first.

### Step 4: Update companion files

If you changed narration-relevant content or slide ordering, update **all** of:

1. **`NARRATION_SCRIPT.md`** — timing marks and narration text
2. **`captions.srt`** — SRT entries (must match narration word-for-word)
3. **`YOUTUBE_METADATA.md`** — description timestamps and transcript
4. **`STORYBOARD.md`** — scene-by-scene mapping (if it exists)

If you did not change narration or ordering, skip this step.

### Step 5: Commit and push

```bash
git add mdpi_submission/video_intro/slides.html
git add mdpi_submission/video_intro/NARRATION_SCRIPT.md    # if changed
git add mdpi_submission/video_intro/captions.srt           # if changed
git add mdpi_submission/video_intro/YOUTUBE_METADATA.md    # if changed
git commit -m "video_intro: update slide deck content (agent workflow)"
git push -u origin <branch-name>
```

---

## Hard constraints

These are non-negotiable. Violating any one is a blocking error.

### No new quantitative claims

Every number in the deck must trace to a committed SI JSON ledger. You may not:
- Compute new statistics from raw data
- Round, interpolate, or extrapolate existing numbers
- Cite numbers from the manuscript text that are not also in a JSON ledger

### No clinical claims

The paper is computational. You may not claim or imply:
- Clinical utility or patient outcomes
- Vaccine efficacy or therapeutic benefit
- Regulatory relevance

### No banned tone words

Do not use: "groundbreaking", "revolutionary", "state-of-the-art", "novel", "pioneering", "cutting-edge", "game-changing", "breakthrough", "outperforms", "superior", "best", "first-ever".

### Scope boundaries

- MHC class I only (no class II)
- Canonical 8–11-mer peptides only (no PTM, no spliced peptides)
- No TCR-specificity claims
- No NetMHCpan-4.2 comparisons in main results (4.2 data exists in SI but is not the paper's primary comparison)

### Preserve frozen manuscript numbers

The following numbers are frozen and must appear exactly as listed:

| Number | Context |
|---|---|
| 35 M | Model parameters |
| 118,143 | Clean TransPHLA rows |
| 161,652 | Total TransPHLA rows |
| 26.9% | Contamination fraction removed |
| −0.0002 | Fusion Δ AUROC (TransPHLA) |
| 0.9573 / 0.9575 | DeepNeo / NMP fusion AUROC |
| −0.0137 | BA-head Δ AUROC (TransPHLA) |
| 1.7 × 10⁻³ | BA-head Holm-adjusted p |
| 6.85 | DeepNeo BA mean rank (IEDB weekly) |
| 1.80 | DeepNeo EL mean rank (IEDB weekly) |
| 0.862 | Transductive rescorer AUROC |
| 0.442 | Inductive rescorer AUROC |

---

## Design reference

The deck follows these conventions (do not break them):

- **Progress bar** at top (12 segments, filled as you advance)
- **Section tags** (upper-left per slide, e.g. "1 / Context")
- **Paper footer** (bottom, every slide): title + venue + page number
- **Assertion-evidence** per slide — one named claim, backed by data
- **Colour-coded cards** — accent = amber, method = blue/navy, positive = green, problem/negative = red
- **Inline source citations** — every data slide names the SI JSON file
- **Light/dark auto** — CSS respects `prefers-color-scheme`

---

## Troubleshooting

| Issue | Fix |
|---|---|
| Figure not loading | Check `figures/` directory; filenames are case-sensitive |
| SVG layout broken | Inline SVGs use `viewBox`; do not change `viewBox` dimensions without testing |
| Slide overflow | Use `max-height: Xvh` on figures and `overflow: visible` on `.figure-wrap` |
| Dark mode broken | All colours must use CSS variables (`var(--navy)`, etc.) |
| Numbers don't match | Re-read the SI JSON ledger; do not round |
