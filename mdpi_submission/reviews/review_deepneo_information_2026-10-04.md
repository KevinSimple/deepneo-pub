# Pre-submission review — `latex/deepneo_information.tex`

2026-10-04 · 5 segments + Stage 3.5 + claim-verifier · 6 reviewers · findings after deduplication

**Target:** `publication/MDPI_Information_Manuscript/latex/deepneo_information.tex` (canonical MDPI Article; Style-A / CS-register text as of 2026-09-29).  
**Skills:** project `paper-reviewer` (PAT) + `claim-verifier` + MDPI *Information* / SI checklist (`SCOPE_AND_GUIDELINES.md` + official Instructions page).  
**Previous audits:** `CLAIM_EVIDENCE_TABLE.md` (2026-09-03, 515/515 MATCH); `READINESS_REVIEW.md` (2026-08-30). Sep 26–29 edits claimed no number moves.

**Segmentation (announced before dispatch)**

| Segment | Lines | Budget |
|---|---|---|
| Framing (Abstract / Intro / Conclusions) | 54, 76–96, 268–270 | LOW |
| Related work + MDPI SI / journal-fit | 80–86, 28–56, 273–290 | LOW |
| Method / data / stats contract | 99–149 | HIGH |
| Results + numbers | 152–242 + SI JSON | HIGH |
| Discussion / limitations | 245–265 | MEDIUM |
| Language signature | whole `.tex` | Stage 3.5 |

---

## Verdict

Nothing in the current digits **blocks** a scientific claim: claim-verifier re-ran the 2026-09-03 ledger checks and reported **no MISMATCH / no UNSOURCED / no withdrawn-headline leak**. Abstract and Conclusions still match Table 1 on the four load-bearing verdicts (fusion tie; NMP BA-head lead; fus-vs-NMP-BA not Holm-robust; IEDB BA mid-field + 3-predictor EL lead).

What **does** block a clean Susy upload is wording and venue hygiene, not a new number. Four HIGH defects should be fixed first: (1) Related Work still omits the closest ESM–pMHC antecedent (Hashemi et al., *Front. Bioinform.* 2023); (2) the live URL now advertises a v4.2 12/12 win this Article does not claim; (3) “Efficient” in the title / contribution (1) is not backed by any compute metric; (4) Discussion treats the dirty-set ablation and the per-length “leads” as if they explained the clean, multiplicity-controlled match. The 29 Sep CS-register glosses also introduced a **new scientific error** in Methods (motif deconvolution is not assay-side). Required MDPI Article sections and the Guest-Editor COI disclosure are present.

Recommended editorial stance: **major revision before upload**, not reject.

---

## Errors

### [HIGH] Closest PLM–pMHC prior art is absent
**Where:** `latex/deepneo_information.tex:82`  
**Text:** "Parallel deep-learning and transformer-style systems---including MHCflurry-2.0, MHCfovea, TransPHLA, and BigMHC---typically report strong external AUROCs."  
**Defect:** For a title and SI framed on efficient protein language models, Related Work cites ESM2 only as a general encoder. It does not cite prior ESM/PLM peptide–MHC predictors already compared to NetMHCpan-4.1. TransPHLA is a from-scratch transformer, not a pretrained PLM.  
**Confidence:** CONFIRMED — Hashemi et al., *Front. Bioinform.* 2023, 3:1207380 (DOI 10.3389/fbinf.2023.1207380) fine-tunes ESM1b/ESM2 on the NetMHCpan-4.1 train/test sets and claims to outperform NetMHCpan-4.1. Located 2026-10-04.  
**I would be wrong if:** the authors treat TransPHLA as sufficient transformer prior art and place ESM-fine-tune pMHC papers outside this Article’s evaluation-integrity scope.  
**Suggested fix:** Add a short paragraph: prior PLM–pMHC work (Hashemi 2023; later TransHLA / ESMpHLA if you cite them) already uses ESM vs NetMHCpan-4.1; this Article’s increment is the leakage-aware / multiplicity-controlled *evaluation contract* on a compact 35M trunk, not “first PLM for pMHC.”  
**Status vs prior audits:** NEW for this SI framing (the 09-03 number audit did not check Related Work completeness).

### [HIGH] “Often inconsistently applied” is a frequency claim later withdrawn
**Where:** `latex/deepneo_information.tex:84` (caveat at 265)  
**Text:** "in the pan-allele literature, allele-clustered intervals on the headline Δ and NetMHCpan-matched pair decontamination are often inconsistently applied."  
**Defect:** The motivating gap is stated as a field-wide frequency fact. Limitations later say the same observation is “qualitative, not a systematic review.” The same sentence also hangs “unadjusted multiple testing remain common” on Kapoor/Whalen/Bernett/Joeres, which document leakage, not Holm/multiplicity. Holm 1979 is not in the bibliography.  
**Confidence:** CONFIRMED — both sentences are in this manuscript; those four papers are leakage/split papers.  
**I would be wrong if:** a systematic pMHC CI/decontamination survey is in the Supplement, or one of the four cited papers has a multiplicity section that was missed.  
**Suggested fix:** Move the frequency claim to the already-honest Limitations wording (“informal observation, not a systematic review”). Cite Holm 1979 for the adjustment itself. Keep Kapoor et al. for leakage only.  
**Status:** RECUR (honesty flag existed; Related Work still overclaims).

### [HIGH] Length “gains” / “leads” restate the non-Holm-robust fusion-vs-NMP-BA row
**Where:** `latex/deepneo_information.tex:196` and `:251`  
**Text:** "per-length ΔAUROC confidence intervals exclude zero at 8--, 9--, 10--, and 11-mers; the smallest absolute gain is at 9mers (+0.0043), not an ``exact tie''" / "DeepNeo leads at every length 8--11 with CIs excluding zero, and the narrowest significant margin is on the dominant 9mer class (+0.0043)."  
**Defect:** `per_figure_provenance.json` `fig_per_length_decontam` is DeepNeo vs NetMHCpan-4.1 BA — Table 1’s deployed-fusion-vs-NMP-BA row, already judged “not Holm-robust (0.15).” The sentence never names that comparator. Discussion then upgrades it to “leads” / “significant margin.” Those CIs are recorded as B=500, not the Methods B=1000 allele-clustered family.  
**Confidence:** CONFIRMED — weighted length Δ ≈ +0.007 matches fusion-fixed +0.0073 vs NMP-BA, not fusion-vs-fusion (−0.0002). Claim-verifier tagged the Discussion wording SOFT S06.  
**I would be wrong if:** the length figure used a different contrast, or the three-condition rule were defined to include per-length CIs.  
**Suggested fix:** Name the comparator (“vs NetMHCpan-4.1 BA, the same contrast Table 1 marks not Holm-robust”). Drop “leads” / “significant margin.” Keep the 9mer-not-an-exact-tie rebuttal as a descriptive split of a *non-robust* pooled edge.  
**Status:** NEW wording risk after the CS-register Discussion pass (digits unchanged).

### [HIGH] Dirty-set ablation used to explain the clean-set match
**Where:** `latex/deepneo_information.tex:251` (protocol only at Results `:232`)  
**Text:** "The ablation (Figure 3; Supplementary Table S1) shows several small gains along orthogonal axes… Under the leakage-controlled protocol, that stack is competitive… on clean TransPHLA the deployed fusion is tied… without any single component being solely responsible for the match."  
**Defect:** Component shares are measured on full-set TransPHLA EL (n=161,652). Results already say a decontaminated re-ablation is deferred. Discussion then treats those dirty-set Δs as the reason for the leakage-controlled fusion tie.  
**Confidence:** CONFIRMED — Results 232 vs Discussion 251.  
**I would be wrong if:** Table S1 were recomputed on the clean 118,143 rows and the same distributed-gain story held.  
**Suggested fix:** In Discussion, restrict the ladder to “component accretion on the *full* TransPHLA EL set; it does not attribute the *clean* fusion tie.” Or re-ablate on n=118,143.  
**Status:** RECUR (caveat exists in Results; Discussion still over-interprets).

### [HIGH] Title / contribution “efficient” is not an efficiency result
**Where:** `latex/deepneo_information.tex:28`, `:96`, `:240–242`  
**Text:** "Efficient Protein Language Models for Peptide--MHC Ranking" / "an efficient PLM-based peptide--MHC ranker" / "The efficiency claim is therefore a modest one: under this protocol a 35M-parameter trunk is already competitive… which says nothing about whether a larger trunk would extend the margin."  
**Defect:** The only Results block that could underwrite the title reports no latency, memory, FLOPs, or throughput (the old ~200 pairs/s note was removed). Efficiency is equated with fusion-level accuracy competitiveness of a 35M trunk. SI cover letter still sells “efficiency (lite PLM).”  
**Confidence:** CONFIRMED — subsection contains no compute metric; `CLAIM_EVIDENCE_TABLE.md` records the throughput claim as REMOVED.  
**I would be wrong if:** naming ESM2-35M vs a deferred 150M redux is accepted as the paper’s efficiency result.  
**Suggested fix:** Retitle toward the evaluation contract (“Leakage-Aware Evaluation of a Compact PLM…”), or restore one measured efficiency number from a committed artefact. Soften contribution (1) to “compact 35M PLM ranker.”  
**Status:** RECUR (throughput removed; title not updated).

### [HIGH] Live predictor page contradicts this Article
**Where:** `latex/deepneo_information.tex:253` (tense clash at `:286`)  
**Text:** "A live predictor is available at https://deepneo.kevinwanglab.org/"  
**Defect:** Fetched 2026-10-04, the landing page calls v4.1 “older” / “Superseded by v4.2” and states v4.2 “beats NetMHCpan-4.2 on 12/12 supported alleles.” Table 1’s v4.2 rows are fusion pooled-NMP / within-allele tied, BA NMP higher. Data Availability already hedges (“was available at submission”); Discussion does not.  
**Confidence:** CONFIRMED — HTTP fetch of the cited URL.  
**I would be wrong if:** the landing page were scoped to the submitted v4.1 model and made no 12/12 superiority claim.  
**Suggested fix:** Point the manuscript at a submission-frozen v4.1 URL, or put a one-line disclaimer on the landing page that the 12/12 board is paper-2 / v4.2 and not this Article. Align Discussion tense with Data Availability.  
**Status:** NEW (site evolved after the 09-03 audit).

---

## Improvements

### Sep 29 MS motif-deconvolution gloss is scientifically wrong
**Where:** `:105`  
**Text:** "upstream mass-spectrometry (MS) motif-deconvolution protocol (an assay-side label-assignment step that maps each MS peptide to one HLA allele from a multi-allele cell line)"  
**Defect:** Reynisson et al. 2020 (`netmhcpan41`) describes NNAlign_MA as *training-time* iterative pseudo-labelling of the multi-allele EL fraction, on a corpus that also contains single-allele EL — not an assay-side assignment of every MS peptide.  
**Confidence:** CONFIRMED against the already-cited paper.  
**I would be wrong if:** the released 4.1 folds were produced by wet-lab allele assignment of every eluted peptide.  
**Suggested fix:** “training-time motif deconvolution that iteratively assigns a single allele to multi-allele MS-EL peptides (NNAlign_MA), as released; DeepNeo-CL does not re-deconvolve.”  
**Status:** NEW — introduced by the 2026-09-29 CS-register P0-a gloss.

### Sep 29 pocket-rescorer gloss overstates 3-D cleft geometry
**Where:** `:118`  
**Text:** "a small residual MLP fit on 3-D descriptors of the peptide-binding cleft of the MHC molecule, taken from crystal templates"  
**Defect:** The withdrawn head is still correctly marked not-deployed, but “3-D descriptors of the cleft” reads as geometric structure features. The implementation is a high-dimensional sequence-physchem vector at crystal-defined contact positions.  
**Confidence:** PLAUSIBLE as a false scientific claim; CONFIRMED as CS-reader ambiguity.  
**Suggested fix:** “sequence-physicochemical descriptors at crystal-defined peptide–cleft contact positions.”

### Table 1 Wilcoxon column and Holm footnote are different tests
**Where:** `:170`, `:177`  
**Text:** Wilcoxon 0.038 … not Holm-robust (0.15) / Holm p: 0.505 / 0.0017 / 0.505 / 0.151  
**Defect:** Printed 0.038 is fusion-fixed `within_allele_wilcoxon_p=0.0377` (91 alleles). Holm 0.15 is `holm_adjusted_p=0.1511` from a different raw p=0.0504 (84 alleles). Line 157 discloses point estimates vs Holm/CI, not this p-split. Recurs from the Aug 31 two-source note.  
**Confidence:** CONFIRMED.  
**Suggested fix:** Print the Holm-pipeline raw p (0.0504) in the Wilcoxon column, or add “Wilcoxon p from fusion-fixed 91-allele test; Holm family uses the 84-allele filter.”  
**Status:** RECUR.

### Three-condition rule written as every signed Δ, but Holm/CI are v4.1-only
**Where:** `:139–144` vs Table 1 v4.2 BA “NMP higher”  
**Suggested fix:** State that the three-condition gate applies to the four v4.1 TransPHLA rows; v4.2 rows are matched-corpus descriptive controls.

### Abstract “leads a small EL panel” can be read as TransPHLA EL
**Where:** `:54` vs `:270`  
**Defect:** “In that setting” is TransPHLA pair-removal + multiplicity; Table 1 EL is Holm-tied. Conclusions correctly names the IEDB three-predictor MS-EL board. Abstract word count measured 201 (whitespace tokens; range as one word) — at or 1 over the MDPI ~200 cap (Sep-27 changelog claimed exactly 200).  
**Suggested fix:** “leads the three-predictor IEDB weekly EL board.” Cut ~5 words (`(Methods)` plus one clause) to sit safely under 200.

### Conclusions invents “lite ensemble”
**Where:** `:270`  
**Suggested fix:** “The ESM2-35M five-fold ensemble…”

### Case-study first/second reverses Results A/B
**Where:** `:247–249`  
**Defect:** Results A = overlap, B = rescorer; Discussion says “In the first (rescorer)… In the second (overlap)…”  
**Suggested fix:** Keep Results order, or drop “first/second.”

### “Successor looks strong” is not a measured 4.2 score
**Where:** `:247`  
**Suggested fix:** Keep the Results wording: overlap rate, not “looks strong.”

### “Much larger domain model” / “orthogonal axes” / SupCon listed as a gain
**Where:** `:251` vs `:232`, `:263`  
**Suggested fix:** Drop unsourced size comparison. Do not call an un-ablated accretion “orthogonal.” Name SupCon as a small AUROC cost kept for rare-allele AUPR.

### IEDB within-allele tie (p=0.65) absent from Discussion
**Where:** Results `:208` vs Discussion silence  
**Suggested fix:** Restate the deployment-fair per-ref tie and point the complementary per-week p=0.0453 to Figure S3, so a referee cannot treat rank-1 count as the win.

### MDPI production hygiene
- References are **not** in order of appearance (first cites `ott2017, tesla2020, esm2_2023`; first `\bibitem` is `esm2_2023`). Official *Information* Instructions require appearance order. Medium: free-format may waive at first submission; do it before production.
- `\supplementary` should list “Figure S1: title, Table S1: title, …” not a nickname list.
- Data Availability does not say whether **code** is available (official Materials and Methods asks authors to make this clear).
- `COVER_LETTER.md` still has `Date: [SUBMISSION DATE]`.
- Keywords = 7 (legal 3–10). Required back-matter 9/9 present, including P.N. Guest-Editor COI + independent handling.
- SI interpretability / XAI is an SI keyword this paper explicitly does not claim — honest, but a Journal-Fit referee may still ask for one attribution figure or a clearer “out of scope” sentence in the Introduction.
- Primary board is 8–11mers; Limitations name alphabet and MHC class, not the length window.
- Allele-inclusion rule for Wilcoxon / Holm / bootstrap (84 vs 91 vs 112) is not in Methods.

---

## Language signature (Stage 3.5)

Measured on the English `.tex` only, with `lexicons-en.md`. These markers **do not prove AI authorship**.

Criteria A1, A2, and A4 do not fire; they are removable by find-and-replace and are therefore **non-diagnostic when they pass**; the low count licenses no inference.

Fires (writing defects only):

- **A3** em-dash density (paired interpolations at 82, 90, 223, 251) — LOW.
- **B1** Discussion three ~200-word paragraphs (CV 3.3%) — MEDIUM.
- **B2** verbatim 8–16 word chains (shared-corpus cleaning; Holm-non-robust clause; rescorer collapse) — MEDIUM.
- **B5** contrastive-correction frame (“X, not Y” / “rather than”) in 16/40 paragraphs — MEDIUM. The honesty register is doing this on purpose; still flatten a few.
- **B7 / B9** Conclusions and Discussion paragraph 2 retell Results — LOW / MEDIUM.

B3, B6, B8 do not fire (counts only; not a cleanliness certificate).

---

## Checked and clean

- **Digits.** Claim-verifier + Results reviewer: Table 1 v4.1/v4.2 AUROCs, Wilcoxon, Holm, bootstrap CIs; n=118,143 / 43,509 / 26.9%; weekly BA 6.85 / 0.7951 / 14 r1 / 9 outright; EL 1.80 / 0.7763 / 24/19; per-ref 15/12/19 p=0.65; pool 32,790 / 0.7506 / 0.7689; holdout 1,365 / 574 / 1,364 / 99.93%; rescorer ≈0.862 → 0.442; ablation ladder +0.005 steps and rare-allele +0.022 AUPR — all MATCH named SI JSON. No withdrawn 0.9767 / 0.8583 / >10σ / p=0.014 / 0.978 ceiling.
- **Sep 27 Abstract rewrite.** Digits were removed from the Abstract (09-03 table still listed Δ=−0.0137 / +0.0073 there). Directional wording still MATCHES the ledgers. Δ=−0.0137 remains in Conclusions.
- **Honesty flags.** Fusion tie; NMP BA-head lead; fus-vs-NMP-BA not Holm-robust; pocket rescorer withdrawn; MHCflurry not a TransPHLA co-primary; no clinical / Class II / TCR claim. Tone-rule strings `survive` / `shortfall` / `do not solve` / `for an ML/NLP audience` are absent.
- **MDPI Article skeleton.** Title, authors, ORCIDs, affiliation, corresponding author, abstract, 7 keywords, IMRaD + Conclusions, Supplementary, CRediT, Funding, IRB N/A, Consent N/A, DAS, Acknowledgments, COI (GE disclosure), 26/26 cites with DOI strings.
- **Cite graph.** 26 cited = 26 defined; no orphans in this pass.
- **Case A overlap.** 99.93% is framed as a train–test overlap rate, not an accuracy (Results 223). Keep that wording; Discussion “looks strong” is the regression.

**Stale census note:** 2026-09-03 `CLAIM_EVIDENCE_TABLE.md` said 515/515 (432+83). Current traceability audit reports 434 main + 145 SI and one ORCID token unverified. Re-run and refresh that table before Susy so the pack does not advertise an old 515/515.

---

## New vs recurrent

| Finding | New after Sep 26–29? |
|---|---|
| Hashemi 2023 missing | NEW (literature, not a number) |
| Live URL v4.2 12/12 | NEW |
| Sep 29 deconvolution / 3-D glosses | NEW |
| Discussion “leads at every length” | NEW wording on an old row |
| Case A/B order flip | NEW |
| Abstract 201 vs claimed 200 | NEW (cap drift) |
| “Often” vs qualitative Limitations | RECUR |
| Dirty ablation → clean tie | RECUR |
| Title “Efficient” / no throughput | RECUR |
| Wilcoxon 0.038 vs Holm 0.15 two-source | RECUR |
