# Instructions for the cloud agent

You are a cloud agent working in the `mdpi_submission/video_intro/` folder of the public `deepneo-pub` repo. Your job is to **generate CS-friendly pop-sci content for the slide deck and integrate it into `slides.html`**.

## 1. Context (read these first)

| File | What it tells you |
|---|---|
| `README.md` | Overall workflow for the 3:45 YouTube video + slide-to-narration mapping |
| `PROMPT_FOR_CONTENT_AI.md` | The exact prompt to send to a content-generating AI (if you are that AI, follow it directly) |
| `NARRATION_SCRIPT.md` | 525-word narration script. The slide content you generate must align with this |
| `slides.html` | The 12-slide HTML deck. Your output integrates into the existing slide markup |
| `../evidence/CLAIM_EVIDENCE_TABLE.md` | Every quantitative claim in the paper → the SI JSON file that backs it. Any number you insert into a slide must trace to this table |
| `../compliance/ACADEMIC_CONTENT_CLAIMS_COMPLIANCE_REPORT_2026-10-04.pdf` | The two formal compliance verdicts (PASS). Do not introduce new claims that would require re-auditing |

## 2. Workflow

### Step A — Generate content

Follow `PROMPT_FOR_CONTENT_AI.md` as your task spec. Return 11 markdown blocks (slide 2 through slide 12), each with:

- **Background** — one 3–5 sentence paragraph
- **Analogies** — 1–2 biology → CS mappings
- **Jargon translation** — a short glossary
- **Visual** — one specific diagram/illustration recommendation
- **Factual guardrails** — things not to claim

Keep each slide under 250 words across the five sub-sections.

### Step B — Integrate into `slides.html`

The deck has 12 `<section class="slide">` blocks. For each slide 2–12:

1. Keep the existing section-tag, h2 heading, and visual structure (progress bar, footer, etc.).
2. Inside each slide's **card content**, replace or augment the body text with your pop-sci paragraph. Keep text under 30 words per card to maintain visual balance.
3. Add any suggested visual as either:
   - An inline SVG (if simple diagram — see slide 2's existing SVG as the template)
   - An `<img src="figures/<filename>.png">` referencing an image you generate / request
   - A description `TODO: visual — <description>` comment for a later diagram-generation pass
4. Preserve `<p class="cite">` source citations under every data slide (slides 7, 8, 10 especially).
5. Do not alter the colour-coded card classes (`card-accent`, `card-blue`, `card-green`, `card-red`) — they encode semantic meaning.

### Step C — Sanity-check against frozen numbers

Before saving, open `../evidence/CLAIM_EVIDENCE_TABLE.md` and verify every number you have introduced into the slides traces to one of its rows. If you introduce a number not in that table, either:
- Remove it, or
- Mark it `TODO: verify against SI JSON` and leave for human review

**Frozen headline numbers (never change)**:
- TransPHLA fusion match: v4.1 fusion vs fusion AUROC 0.9573 vs 0.9575 (Δ = −0.0002, Tied)
- BA-head loss: Δ = −0.0137, Wilcoxon p = 7.2×10⁻⁴, Holm 1.7×10⁻³
- EL panel lead: DeepNeo mean rank 1.80 in 3-predictor MS-EL board
- IEDB weekly BA: mean rank 6.85 among 14 ranking-eligible predictors
- Transductive-fit case study: 0.862 → 0.442
- Decontamination: n = 118,143 (from 161,652; 43,509 removed, 26.9%)

### Step D — Update companion files

If your slide edits meaningfully change what the narrator says, also update:
- `NARRATION_SCRIPT.md` — keep timing marks consistent
- `captions.srt` — regenerate timing if the narration changes
- `README.md` slide-to-narration mapping table

### Step E — Commit

Commit messages should be of the form:
```
mdpi_submission/video_intro: <specific change> (<slides touched>)
```

Example: `mdpi_submission/video_intro: integrate CS-friendly biology background (slides 2-4)`.

## 3. Hard constraints (do not violate)

1. **No new quantitative claims** that are not already in `../evidence/CLAIM_EVIDENCE_TABLE.md`.
2. **No clinical / Class II MHC / PTM / TCR-specificity claims** (see paper scope restrictions in `PROMPT_FOR_CONTENT_AI.md`).
3. **No reference to paper-2 or any model not evaluated in this paper**.
4. **No tone-rule word violations**: avoid `fails`, `survives`, `do not solve`, `shortfall`, `for an ML/NLP audience`, `crucial`, `pivotal`, `revolutionary`, `groundbreaking`.
5. **Keep the deck self-contained**: no external script tags, no CDN links beyond what is already there (nothing — current deck has zero external deps).
6. **Do not touch** `../compliance/` or `../evidence/` folders. Those are the ground-truth audit record.
7. **Do not touch** anything outside `mdpi_submission/video_intro/`.

## 4. Deliverables you should produce

- Updated `slides.html` with integrated pop-sci content
- Optional: additional inline SVGs where cards benefit from a diagram
- Updated `NARRATION_SCRIPT.md` and `captions.srt` if the narration changes
- A short `CHANGES_FROM_AGENT.md` log at the end of your pass describing what you changed and why

## 5. If you are stuck

- The paper is at: `github.com/KevinSimple/deepneo-pub` (this repo) — the top-level `README.md`, `MODEL_CARD.md`, and `BENCHMARK_SCOPE.md` carry additional context about the project.
- The two formal compliance reports in `../compliance/` describe the paper's structure and claims and are the fastest way to orient yourself if you only have 10 minutes.
- The 515-claim-to-SI-file mapping in `../evidence/CLAIM_EVIDENCE_TABLE.md` is the single source of truth for every number.

Good luck.
