# MDPI *Information* intro video — slide pack

Public, iterable pack for a 3:45 YouTube intro video on the MDPI *Information* manuscript:

> **Efficient Protein Language Models for Peptide–MHC Ranking: A Leakage-Aware Evaluation Protocol under Multiplicity Control**
> Kevin Wang · Parma Nand · MDPI *Information* · SI *Emerging Trends in Machine Learning and Natural Language Processing*

This folder is a self-contained slide pack: HTML deck, narration script, B-roll prompts, captions, and three thumbnail options. It is intended for iteration by a cloud agent or a manual editor.

---

## Contents

| File | Purpose |
|---|---|
| `slides.html` | Self-contained 12-slide HTML deck with 7 integrated paper figures. Open in Chrome → F to fullscreen → arrow keys to advance. Dark/light auto. |
| `NARRATION_SCRIPT.md` | 525-word narration script with timing marks (0:00 – 3:45) in 7 blocks |
| `STORYBOARD.md` | **Scene-by-scene production guide**: maps narration → slides → figures → B-roll → transitions for the video editor |
| `YOUTUBE_METADATA.md` | **Ready-to-paste YouTube upload fields**: title, description with timestamps, tags, category, thumbnail and caption instructions |
| `OPENART_PROMPTS.md` | 3 optional B-roll clip prompts for OpenArt Video (opening, mid, outro) |
| `captions.srt` | 26-entry SRT caption file for YouTube auto-upload |
| `thumbnail_option1.svg` | Thumbnail A — headline-claim style |
| `thumbnail_option2.svg` | Thumbnail B — 0.862 → 0.442 number hook (**recommended** — highest curiosity gap) |
| `thumbnail_option3.svg` | Thumbnail C — question-based opener |
| `figures/` | 14 PNG renders of the paper's figures; 7 are integrated into the slide deck |

---

## 12-slide structure

| # | Slide | Section tag | Narration block |
|---|---|---|---|
| 1 | Title + authors + venue | — | HOOK (0:00) |
| 2 | A central problem in computational immunology | 1 / Context | WHY IT MATTERS (0:15) |
| 3 | Computationally — sequence ranking under a context key | 2 / Problem framing | FRAMING AS ML (0:45) |
| 4 | DeepNeo-CL architecture (8-row table) | 3 / Model | PIVOT (1:10) |
| 5 | Why reported gains in this field are hard to trust | 4 / The evaluation problem | THE PROBLEM (1:30) |
| 6 | Three-condition superiority rule | 5 / Our evaluation contract | OUR PROTOCOL (2:05) |
| 7 | Decontaminated TransPHLA — Table 1 reproduction | 6 / Headline result · TransPHLA | HEADLINE RESULT (2:25) |
| 8 | IEDB `auto_bench` weekly leaderboard | 7 / IEDB weekly leaderboard | IEDB WEEKLY (2:45) |
| 9 | Where NetMHCpan still wins (BA-head) | 8 / Honest reporting | HONEST (3:05) |
| 10 | A documented transductive-overfitting failure | 9 / Case study · evaluation-leakage failure | CASE STUDY (3:15) |
| 11 | What this paper actually claims (3 cards) | 10 / Takeaway | TAKEAWAY (3:35) |
| 12 | Resources + CTA | Resources | CTA (3:40) |

---

## Design principles baked into the deck

Research-backed (NeurIPS / ICML presentation conventions + the assertion-evidence model):

- **Progress bar** at top (12 segments, filled as you advance)
- **Section tags** (upper-left per slide)
- **Paper footer** (bottom, every slide): title + venue + page number
- **Assertion-evidence per slide** — each slide makes one named claim, backed by a table / figure / SVG / inline citation
- **Low-text, high-density** — few words but substantial supporting detail
- **Colour-coded cards** — amber = accent, blue = method, green = positive result, red = problem / negative
- **Inline source citations** — every data slide names the SI JSON file at the bottom
- **Light/dark auto** — slides respect OS preference

---

## Hybrid record-and-compile recipe (~45 min)

1. **Open `slides.html`** in Chrome. Press F to fullscreen. Flip through once to verify figures load.
2. **Record narration** (~10 min). Use Descript (recommended for its built-in teleprompter), or any screen+mic recorder. Record each `[time]` block from `NARRATION_SCRIPT.md` separately.
3. **Screen-record the slides** (~10 min). Advance each slide roughly at the timing in the script.
4. **(Optional) Generate B-roll** (~5 min). Paste the 3 prompts from `OPENART_PROMPTS.md` into openart.ai.
5. **Compile in Descript / iMovie / Veed** (~15 min). Export MP4 1080p H.264.
6. **Upload to YouTube** (~5 min). Attach `captions.srt`. Pick a thumbnail (recommend option 2).

---

## Data provenance

Every number shown in the deck traces to a committed Supplementary-Data JSON ledger in `../evidence/supplementary_data/`:

| Slide | Numbers | Source |
|---|---|---|
| 7 | Table 1 AUROCs, Wilcoxon p, Holm, bootstrap CIs | `transphla_rescored_fusion_fixed.json` + Holm/bootstrap SI ledgers |
| 8 | Weekly 6.85 / 14 / 0.7951 / rank-1 count | `weekly_ranking_v41_2020_2026_singlecol_v2.json` |
| 9 | BA-head Δ = −0.0137, Holm 1.7×10⁻³, CI | Table 1 row 2 + `paired_bootstrap_ci.json` |
| 10 | Rescorer 0.862 → 0.442 | `inductive_reranker_result.json` |

Full claim-to-evidence mapping: `../evidence/CLAIM_EVIDENCE_TABLE.md` · 515/515 claims MATCH per 2026-09-03 audit, re-verified 2026-10-04.

---

## For an iterating agent

If you are a cloud agent working in this folder:

- The deck is **one self-contained HTML file**. Edit `slides.html` directly.
- Images in `figures/` are referenced relatively; preserve the filenames or update the `<img src>` paths.
- Narration script and captions are **not auto-linked** — if you change narration or slide ordering, update `NARRATION_SCRIPT.md`, `captions.srt`, and the slide-to-narration table above.
- Thumbnails are standalone SVGs; export to PNG with `rsvg-convert` or similar for YouTube.
- All frozen manuscript numbers must stay unchanged. Verify against `../evidence/CLAIM_EVIDENCE_TABLE.md`.
