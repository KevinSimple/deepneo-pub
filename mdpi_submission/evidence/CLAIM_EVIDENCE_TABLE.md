# Claim → evidence table (MDPI *Information* pack)

**Generated / audited:** 2026-09-03 (flags A–F wording + Whalen/Joeres cites; numbers unchanged from pass 17)  
**Reproducible audits:** `latex/_pass7_audit.py` (headline claims), `latex/_traceability_audit.py` (every numeric token), `latex/_directional_audit.py` (ordering/superlative claims re-derived), `latex/_structure_audit.py` (labels, floats, Crossref/DataCite metadata, SI ledger inventory), `latex/_figure_audit.py` (numbers rendered **inside** figure PDFs + typeset Table 1), `latex/_doi_validate.py` (DOI resolution)  
**Canonical tex:** `latex/deepneo_information.tex`  
**Ledgers:** `latex/supplementary_data/`  

Legend: **MATCH** = digit matches committed JSON/CSV; **MATCH†** = rounded; **SOFT** = methods/config not in SI JSON (accepted if cited literature); **FIXED** = wording corrected this pass.

| Claim (location) | Evidence file / field | Status |
|---|---|---|
| TransPHLA clean n=118,143; 43,509 removed (26.9%) | `transphla_rescored_fusion_fixed.json` | MATCH |
| Table 1 v4.1/v4.2 AUROCs, Wilcoxon, Holm, bootstrap CIs | fusion_fixed + holm + bootstrap + score_v42 | MATCH† |
| CDF \|Δ\|=9.1×10⁻⁵ | `transphla_fusion_cdf_rescored.json` | MATCH† |
| Weekly BA 6.85 / 0.7951 / 14 r1 / 9 outright; NMP-4.0/4.1 ranks | `weekly_ranking_…_v2.json` | MATCH† |
| Weekly EL 1.80 / 0.7763 / 24 r1 / 19 outright; NMP EL peers | same | MATCH† |
| Per-ref Wilcoxon p=0.65 (15/12/19) | `weekly_perref_wilcoxon_vs_nmp41.json` | MATCH† |
| Pool 32,790; 0.7506 vs 0.7689 | `head_to_head_ba_el_split.json` | MATCH |
| Holdout 1365 / 574 / 1364 (99.93%) | `iedb_holdout_nmp42_overlap.json` | MATCH |
| Rescorer ~0.862 → 0.442 | `inductive_reranker_result.json` | MATCH† |
| Ablation ladder + step Δs + rare-allele +0.022 | `ablation_ladder.json` | MATCH |
| Official NMP-4.1 folds / negatives |~\cite{netmhcpan41} (no SI count ledger) | SOFT† **FIXED**: removed exact 207,029 / 33M / 99:1 digits not in SI |
| A100 throughput ~200 pairs/s | was BMC runtime note only | **REMOVED** this pass |
| Live predictor HTTP 200 | `https://deepneo.kevinwanglab.org/` | MATCH |

## Directional (non-numeric) claims — re-derived from ledgers, pass 14

The digit audits confirm each number matches a ledger value; they cannot confirm
the *words* around it. `latex/_directional_audit.py` recomputes each ordering.

| Directional claim | Re-derived result | Status |
|---|---|---|
| NetMHCpan-4.0 BA is the BA mean-rank consistency leader | argmin mean_rank = NMP-4.0 BA (4.9783) | MATCH |
| DeepNeo BA is mid-board, not leader (6.85) | 6.8478 vs leader 4.9783 | MATCH |
| DeepNeo hits rank-1 on more BA weeks than NMP-4.1 BA | 14 vs 11 (incl. ties) | MATCH |
| DeepNeo EL leads the three-predictor MS-EL board | argmin mean_rank = DeepNeo EL (1.8043); board size 3 | MATCH |
| No single ablation step Δ exceeds +0.005 | max step Δ = +0.0050 | MATCH |
| SupCon v2 carries a small AUROC cost | step Δ = −0.0010 | MATCH |
| Narrowest significant per-length margin is the 9mer (+0.0043) | argmin \|Δ\| at length 9 = 0.00427; all lengths 8–11 positive | MATCH |
| **Only the v4.1 BA-head survives all three conditions** | DeLong ∧ Holm ∧ CI true only for `v41_ba_head_vs_nmp_ba`; fusion-vs-fusion F/F/F, EL head T/F/F, deployed fusion T/F/T | MATCH |
| Surviving BA-head effect is a DeepNeo **deficit** | mean per-allele Δ = −0.00525 | MATCH |
| Deployed fusion's pooled lead is not Holm-robust | Holm p = 0.1511 | MATCH |
| Abstract Δ = −0.0137 (BA head) / +0.0073 (fusion) | clean_vs_41_118143 fusion-fixed deltas | MATCH |
| Fusion-vs-fusion is a tie | Δ = −0.0002, bootstrap CI includes zero | MATCH |
| Inductive rescorer is below chance | 0.4423 < 0.5 | MATCH |

Note on the two-source convention: **Table 1** point estimates come from the
fusion-fixed artefact (clean subset) while Holm/CI footnotes come from the
bootstrap pipeline on the same rows — stated explicitly in Results. (The ledger
filename `table2_holm_adjusted.json` and its `_meta.family` string say
"Table 2"; that numbering is inherited from the BMC draft. In this MDPI
manuscript the head-to-head table is **Table 1** — the only main-text table.
Do not renumber the ledger; it is a frozen artefact.) The
per-allele Wilcoxon for the deployed fusion is p=0.0504 *before* Holm, so the
"looks like a win without multiplicity control" reading rests on pooled DeLong
plus the bootstrap CI (which excludes zero), not on the per-allele test.

## References + structure (pass 14)

| Check | Result |
|---|---|
| Cite graph | **24 cited / 24 defined**, no orphans |
| doi.org HTTP | **24/24 OK** |
| Reference *metadata* (year + volume) vs Crossref | **22/22 consistent**; `iedb2019` online-first 2018 vs issue 2019 (accepted) |
| arXiv DOIs (not in Crossref) vs DataCite | **2/2 resolved** (`supcon2020` 2020, `lds2021` 2021) |
| Numeric tokens traced | **515/515** (432 main + 83 SI), 0 unverified |
| Headline claim checks | **96/96 MATCH** |
| Directional claims re-derived | **21/21** |
| Label / ref integrity | 0 dangling refs; **fixed this pass**: Figure 1 (`fig:roc`) had a label but was never cited in text |
| Graphics files present | 11/11 |
| SI cross-refs | main claims Tables S1–S2 + Figures S1–S6; supplement has exactly 2 tables + 6 figures |
| Body length | 3,053 words (3,157 with captions; 3,328 with abstract) — above MDPI's 3,000 soft floor on every measure |

## Compile + submission-readiness (pass 15)

| Check | Result |
|---|---|
| `pdflatex` compile | **SUCCESS**, 11 pages, no undefined references or citations |
| Cross-references | final after **two** passes (first pass warns "Rerun") |
| Figure 1 citation (pass-14 fix) | verified live: `fig:roc` → "Figure 1", page 5 |
| Hard TeX errors | 3, all one root cause: no Ghostscript → MDPI logo EPS→PDF fails. Cosmetic (draft logo box, Latin Modern for Palatino); absent on Overleaf. See `latex/BUILD.md` |
| Committed PDF status | **structural proof only — do not submit**; Susy PDF must come from Overleaf |
| MDPI required back matter | **9/9 present** (supplementary, authorcontributions, funding, institutionalreview, informedconsent, dataavailability, acknowledgments, conflictsofinterest, reftitle) |
| Withdrawn-claim firewall | **0 violations** across all pack `.md` + `.tex` |
| Cross-document consistency | `manuscript.md` headline table matches tex on all values; no stale numbers elsewhere |
| Main-text table count | 1 (so the head-to-head table is **Table 1**; ledger key `table2_…` is BMC numbering — **fixed** in pass-14 records this pass) |

## Rendered output — figures and typeset table (pass 16)

Source audits cannot see a compiled figure. `latex/_figure_audit.py` extracts the
text layer from each figure PDF and checks its numbers against the ledgers.

| Check | Result |
|---|---|
| Figure text layers | **9/9 included figures: 0 unverified, 0 withdrawn** |
| Typeset Table 1 (from built PDF) | 109 numeric tokens, **0 unverified** |
| Withdrawn values anywhere in built PDF | **none** |
| PDF encoding artefacts (mojibake) | **0** |
| Supplement compile | **7 pages, 0 errors, 0 undefined refs**, no >20pt overfull boxes |
| SI ledger inventory | **17/17** shipped ↔ listed (now enforced by `_structure_audit.py`) |
| SI ledgers under version control | **FIXED this pass** — a blanket `*.json` rule in `.gitignore` had left all 17 uncommitted (local-machine-only) despite being promised by Data Availability; scoped exception added, all 17 now tracked |

### The three auto_bench universes (never conflate — figures show all three)

| Universe | n | Where |
|---|---|---|
| Raw evaluation rows (before cleaning) | **38,606** | Figures S4/S6 |
| Clean rows after pair-level decontamination | **32,790** (= 38,606 − 5,816, i.e. −15.1%) | main text pooled macro-mean |
| Globally deduplicated unique pairs | **44,516** (21.4% in NMP-4.1, 22.7% in 4.2) | Figure S4; `autobench_decontam_vs_41/42.json` |

### The two weekly Wilcoxon tests (never conflate)

| Test | Result | Where |
|---|---|---|
| Per-week pooled AUROC | 13/5/28, Δ=−0.012, **p=0.0453** | Figure S3 |
| Per-reference within-allele AUROC (deployment-fair) | 15/12/19, **p=0.65** | main text; `weekly_perref_wilcoxon_vs_nmp41.json` |

**Resolved (pass 16):** `fig_data_flow.pdf` had "Table 5" baked into the graphic
(BMC numbering; no Table 5 exists here). Regenerated with the label corrected to
"Figure S4" via the pack-local `latex/_make_fig_data_flow.py` — kept separate
from the shared Phase-0 generator because "Table 5" is correct for the BMC draft.
Verified in the new PDF's text layer: "Table 5" absent, "Figure S4" present, all
numbers unchanged.

## Are the ledgers themselves right? (pass 17)

Every audit above checks one direction: does the manuscript match the ledger? A
ledger with wrong internal arithmetic would pass all of them, because the
manuscript faithfully reproduces the wrong number. `latex/_arithmetic_audit.py`
recomputes each ledger from its own raw inputs — **27 checks, 0 failures**.

| Check | Result |
|---|---|
| Holm–Bonferroni re-derived from the 4 raw Wilcoxon p-values | max \|ledger − recomputed\| = **0.00e+00** |
| Holm preserves raw p-value ordering; no adjusted p below its raw p | pass (min adj − raw = 1.26e−03) |
| Bootstrap CIs bracket their own point estimate | **4/4** |
| `excludes_zero` agrees with the printed CI bounds | **4/4** |
| Every AUROC/AUPR delta = `deepneo − comparator` (own operands) | pass, both the 161,652 and 118,143 blocks |
| Counts partition (clean + removed = full) | 118,143+43,509=161,652; 1,364+1=1,365; 9,527+34,989=44,516; 10,090+34,426=44,516; 43,245+118,407=161,652 |
| Per-length clean counts sum to `n_clean` | 118,407 = 118,407 |
| Percentages recomputed from own numerator/denominator | 26.92% (text 26.9), 99.9267% (99.93), 21.40%, 22.67%, 26.75% |
| Ablation ladder: per-step deltas sum to end-to-end gain | +0.0180 = +0.0180 |
| All AUROC/AUPR/p in [0,1]; bootstrap meta = Methods contract | pass (B=1000, allele-clustered, n=118,143) |

### Fresh-clone reproducibility (pass 17)

Pass 16 committed the Supplementary Data but never *tested* that a clean checkout
is self-sufficient. `git archive HEAD` into a clean temp tree, then the full
suite run from that tree alone:

| Check | Result |
|---|---|
| Fresh checkout contents | 17 ledgers, 13 figure PDFs, 9 audit scripts, 9-file MDPI template, both `.tex` |
| Claims / traceability / directional / rendered / structure, run in the fresh tree | pass / **0 unverified** / **21/21** / clean / clean |

**No manuscript defect found in pass 17** — the gap was in the audit apparatus
(untested reproducibility), not the paper.

## Qualitative flags A–F (2026-09-03) — wording + cites, not new numbers

Six non-numeric claims lacked adequate references or overstated what SI holds.
Fixed with approved softens + two new high-weight refs (`whalen2022`, `joeres2025`).
**All Table 1 / abstract numeric verdicts unchanged.**

| Flag | Was | Now |
|---|---|---|
| A Abstract “many comparisons omit…” | Unsourced; stronger than BMC; tension with Limitations | “ML evaluations often omit…” + `\cite{kapoor2023,whalen2022,bernett2024}` |
| B Rescorer “pass conventional paired testing” | SI paired-p artefact **MISSING** | “look strong under transductive evaluation… fail under induction” + cites; drop paired-testing claim |
| C Intro few/many/inconsistently | No pMHC survey cite | Hedged + Limitations cross-ref + Kapoor/Whalen/Bernett/Joeres |
| D “rarely modelled” cross-attention | Survey claim without survey | Design claim only (`netmhcpan41`, `esm2_2023`) |
| E “statistically powered” | No power calc in SI | Bootstrap CIs resolve tabled effects (ledger-backed) |
| F “generalise beyond this model” | Empirical overclaim | “instantiate failure modes documented across ML/biology ML” + cites |

Cite graph after edit: **26 cited / 26 defined**; both new DOIs HTTP 200.
