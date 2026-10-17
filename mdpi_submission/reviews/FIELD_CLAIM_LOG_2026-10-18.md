# Field-claim verification log — 2026-10-18

Per `.claude/skills/evidence-verified-review` → **Field-Claim Protocol**. Every claim about the *state of the literature* that appears (or was proposed to appear) in a submission artefact must be logged here with its search record and verdict.

Tools used this session: Consensus (semantic search over Semantic Scholar / OpenAlex / PubMed), PubMed E-utilities, WebSearch.

---

## CLAIM 1 — calibration novelty

```
CLAIM:     "No pMHC-I predictor paper has previously reported calibration
            on this benchmark."
           (was live in COVER_LETTER.md contribution #2 and in slides.html slide 7)

QUERIES:   [consensus]  "calibration expected calibration error peptide MHC class I
                         binding prediction neural network"
           [websearch]  'MHC peptide binding prediction "expected calibration error"
                         OR "calibration" probability outputs NetMHCpan MHCflurry'
           [websearch]  'MHCVision false discovery rate posterior error probability
                         NetMHCpan calibration beta mixture model'
           [websearch]  'MHCVision bioinformatics 2021 "calibrated" probability
                         NetMHCpan class I what does it calibrate percentile rank'
           [pubmed]     '(peptide MHC OR pMHC OR neoantigen) AND (calibration OR
                         "calibrated probability" OR "reliability diagram")'  (date_from 2019)
           [pubmed]     'MHCVision estimation global local false discovery rate
                         MHC class I peptide binding prediction'

TOOLS:     consensus, pubmed, websearch

HITS:
  - MHCVision — Pearngam P, Sriswasdi S, Pisitkun T, Jones AR.
    "MHCVision: estimation of global and local false discovery rate for MHC class I
     peptide binding prediction." Bioinformatics 2021;37(21):3830-3838.
    DOI 10.1093/bioinformatics/btab479  ·  PMID 34196671  ·  PMC8570816
    Abstract (verbatim, from PubMed):
      "it is difficult to evaluate statistically the probability of an individual
       peptide binding prediction to be true or false solely considering predicted
       scores. Therefore, statistics describing the overall global false discovery
       rate (FDR) and local FDR, also called posterior error probability (PEP) are
       required to give statistical context to the natively produced scores."
    Method: two-component beta mixture model + modified EM, applied to NetMHCpan output.
    → This is a dedicated probability-calibration method for NetMHCpan class I.

  - NetMHCpan's own percentile-rank calibration: '%Rank' is produced by comparing a
    peptide's score against the score distribution of a large random peptide set,
    explicitly so that scores are comparable across HLA molecules. (NetMHCpan-4.0 /
    4.1 documentation + papers already cited in our bibliography as netmhcpan40 /
    netmhcpan41.)

  - "Calibrated Abstention for Reliable TCR–pMHC Binding Prediction under Epitope
    Shift" — arXiv 2604.13254. Adjacent (TCR-pMHC, not pMHC-I binding) but squarely
    calibration work in the pMHC space.

  - PubMed count for the broad calibration query: 887 records.

VERDICT:   REFUTED
EVIDENCE:  PRIMARY (MHCVision abstract retrieved in full from PubMed)

NARROWED:  The only surviving form is
             "no prior pMHC-I paper reports 10-bin expected calibration error with
              reliability diagrams on the TransPHLA EL set."
           This is novelty-by-over-specification (novelty defined by a specific
           metric x specific benchmark intersection). NOT RECOMMENDED for use as a
           novelty claim. The ECE measurement itself remains a legitimate reported
           result; only the "nobody has done this" framing is dead.

ACTION:    COVER_LETTER.md contribution #2 novelty sentence must be removed or
           rewritten. slides.html slide 7 bullet "No other pMHC predictor paper has
           reported calibration on this benchmark" must be removed.
           Consider citing MHCVision in Related Work.
```

---

## CLAIM 2 — decontamination-ledger novelty

```
CLAIM:     "This decontamination rate on this specific benchmark has not been
            previously published; future papers using TransPHLA now have a specific
            decontam ledger to point to."
           (live in COVER_LETTER.md contribution #1)

QUERIES:   [consensus]  "data leakage train test overlap peptide MHC binding
                         prediction benchmark contamination NetMHCpan"
           [websearch]  "TransPHLA benchmark independent dataset overlap NetMHCpan
                         training data decontamination percentage"
           [websearch]  'comparative study MHC class I predictors data contamination
                         overlap "TransPHLA" "BigMHC" percentage test set cleaned
                         evaluation'
           [websearch]  'MUNIS "Deep learning enhances the prediction of HLA class I-
                         presented CD8+ T cell epitopes" decontamination removed all
                         epitopes training regardless HLA restriction 65%'
           [pubmed]     'MUNIS deep learning HLA class I presented CD8 T cell epitopes
                         foreign pathogens'  → 0 results (not indexed under this query)

TOOLS:     consensus, pubmed, websearch

HITS:
  - MUNIS — Wohlwend J, Nathan A, Shalon N, Crain CR, Tano-Menka R, Goldberg B,
    Richards E, Gaiha GD, Barzilay R.
    "Deep learning enhances the prediction of HLA class I-presented CD8 T cell
     epitopes in foreign pathogens."
    Nature Machine Intelligence 2025;7(2):232-243.
    DOI 10.1038/s42256-024-00971-y  ·  PMID 40008296  ·  PMC11847706
    (MIT CSAIL / Jameel Clinic — Barzilay lab — with Ragon Institute / Gaiha lab.
     NOTE: cite as 2025, not 2024. Online-first late 2024; issue is 7(2) 2025.)

    VERBATIM, retrieved from PMC full text 2026-10-18:
      (a) "over 65% of positive epitopes in the evaluation dataset are also present
           in the training sets of existing predictors, excluding MUNIS where we
           ensure a 0% overlap."
      (b) "This is a far stricter approach to data filtering than previous
           methodologies where only matched HLA-I-peptide pairs were removed from
           the training set, resulting in substantial overlap between test set
           epitopes and training sets."
      (c) "all epitopes used in model evaluation were removed from training sets,
           regardless of HLA-I restriction."

VERDICT:   WEAKENED — but NOT for the reason first assumed
EVIDENCE:  PRIMARY (PMC full text retrieved 2026-10-18)

CORRECTION TO THE 2026-10-18 FIRST PASS:
  The first pass recorded, from a search-engine summary, that MUNIS named
  "TransPHLA and BigMHC" with contamination percentages. The PRIMARY text does NOT
  name those predictors in quote (a) — it says "existing predictors" generically.
  The TransPHLA/BigMHC attribution was the search engine's gloss and must not be
  repeated as MUNIS's wording.

  Further: the two numbers are NOT comparable.
    - MUNIS 65%  = their curated epitope evaluation set vs various predictors'
                   training sets, under HLA-agnostic peptide removal
    - ours 26.9% = TransPHLA holdout vs the NetMHCpan-4.1 training-pair union,
                   under exact (peptide, HLA) pair removal
  Neither supersedes the other numerically. Our 26.9% figure is NOT scooped.

THE ACTUAL EXPOSURE (sharper and more serious than "someone published our number"):
  MUNIS quote (b) explicitly names the criterion this manuscript uses — exact
  (peptide, HLA) pair removal — as the INSUFFICIENT prior approach, and
  demonstrates a stricter alternative. A high-profile 2025 Nat Mach Intell paper
  therefore stands as a published argument against our decontamination design.

  The manuscript ALREADY concedes the point conceptually at
  deepneo_information.tex:134-135:
    "This is a lower bound on cross-model contamination: it does not remove
     peptide-sequence similarity to training peptides, peptide-allele neighbourhood
     leakage, shared upstream MS/BA assays, or private/unenumerated training sets
     of non-NetMHCpan competitors."
  So the SCIENCE is honest. What is missing is the CITATION — we describe the gap
  without pointing at the paper that closes it. To a reviewer who knows MUNIS this
  reads as unfamiliarity with the literature, which is worse than either knowing
  or not knowing.

NARROWED:  Surviving honest framing for the cover letter (already applied):
             "we report an exact-pair decontamination ledger for TransPHLA against
              the NetMHCpan-4.1 training union and ship it as machine-readable SI;
              exact-pair removal is a lower bound, and stricter peptide-level
              criteria remove more."

ACTION:    1. DONE — COVER_LETTER.md contribution #1 rewritten; "has not been
              previously published" removed; lower-bound acknowledgement added.
           2. OPEN — cite MUNIS in Related Work (tex:82) and in the Limitations
              lower-bound paragraph (tex:134-135). Manuscript is under a no-edit
              directive; text drafted but not applied.
           3. CLOSED — primary-source verification complete.
```

---

## CLAIM 3 — "most pMHC papers use pooled AUROC without multiplicity control"

```
CLAIM:     Appears in conversation and in slide framing; a hedged version appears in
           the manuscript at deepneo_information.tex:84 ("in the pan-allele
           literature, allele-clustered intervals on the headline Delta and
           NetMHCpan-matched pair decontamination are often inconsistently applied").

QUERIES:   not independently searched this session

TOOLS:     none

VERDICT:   UNRESOLVED
EVIDENCE:  none

NOTE:      The MANUSCRIPT already handles this correctly. Limitations
           (deepneo_information.tex:265) states verbatim:
             "Informal observations that many prior pMHC papers omit CI/decontamination
              reporting are qualitative, not a systematic review."
           That is the right posture and needs no change. The error was in
           conversational value-claims that went beyond what the paper asserts —
           no submission artefact carries an unhedged version.

ACTION:    none required for the submission. Do not let this claim harden into an
           unhedged form in future derivative material without a systematic survey.
```

---

## CLAIM 4 — "17 SI JSON ledgers + re-runnable audit scripts is unusual in the sub-field"

```
CLAIM:     Live in COVER_LETTER.md contribution #3: "This level of machine-checkable
           reproducibility is unusual in the sub-field."

QUERIES:   not searched this session

TOOLS:     none

VERDICT:   UNRESOLVED
EVIDENCE:  none

NOTE:      Plausible but unverified. No survey has been done of what fraction of
           pMHC-I predictor papers ship per-claim machine-readable ledgers. The
           count itself (17 JSON files) IS verified by `ls latex/supplementary_data/
           *.json | wc -l` = 17, and the re-runnability IS verified by running
           `_claim_evidence_audit.py` (43/43 OK, 0 FAIL, re-run 2026-10-15 and
           2026-10-18). Only the comparative word "unusual" is unverified.

ACTION:    Either (a) soften to a factual statement with no comparative claim
           ("the pack ships 17 machine-readable SI ledgers and a re-runnable audit
            script covering 43 headline numeric claims"), or (b) run a survey of
           ~20 recent pMHC-I predictor papers and record the result here.
           Option (a) costs nothing and removes the exposure.
```

---

## Summary table

| # | Claim | Verdict | Evidence | Ships? |
|---|---|---|---|---|
| 1 | Calibration novelty | **REFUTED** | PRIMARY | ❌ removed 2026-10-18 |
| 2 | Decontam-ledger novelty | **WEAKENED** | **PRIMARY** (confirmed 2026-10-18) | ❌ rewritten 2026-10-18 |
| 3 | "Most papers skip multiplicity control" | UNRESOLVED | none | ✅ paper's hedged form is fine |
| 4 | "Reproducibility unusual in sub-field" | UNRESOLVED | none | ✅ softened to factual 2026-10-18 |

## Literature gaps found (reviewer-visible risk — OPEN)

Neither of these appears in the manuscript's 26-entry bibliography:

| Missing citation | Why it matters |
|---|---|
| **MHCVision** — Pearngam et al., *Bioinformatics* 2021;37(21):3830–3838, doi:10.1093/bioinformatics/btab479, PMID 34196671 | Directly prior art for probability calibration (FDR/PEP) of NetMHCpan class-I output. Our SI reports ECE on the same kind of problem without acknowledging this line of work. |
| **MUNIS** — Wohlwend et al., *Nat. Mach. Intell.* 2025;7(2):232–243, doi:10.1038/s42256-024-00971-y, PMID 40008296 | Explicitly names exact-(peptide,HLA)-pair removal — **our criterion** — as the insufficient prior approach, and demonstrates stricter HLA-agnostic epitope removal. Our Limitations concedes the gap conceptually but cites nobody. |

Suggested reviewers **Bernett** and **Kalinina** both work in biological-ML leakage methodology; MUNIS is a 2025 *Nature Machine Intelligence* paper in exactly that space from the Barzilay lab. Probability they know it: high.

## Recommended citation text (drafted, NOT applied — manuscript under no-edit directive)

**For Related Work (`deepneo_information.tex:82`, after the BigMHC sentence):**

> Decontamination criteria themselves vary across this literature: Wohlwend et al. remove every evaluation epitope from training regardless of HLA restriction, a strictly stronger criterion than the matched-pair removal used here and in most prior comparisons~\cite{munis2025}.

**For the lower-bound paragraph (`deepneo_information.tex:134-135`, appended):**

> This matched-pair criterion is weaker than HLA-agnostic epitope removal~\cite{munis2025}; we report it as a lower bound rather than as a sufficient decontamination guarantee.

**For the calibration figure caption (`supplement.tex:100`, appended):**

> Probability calibration for class-I predictors has previously been approached through FDR/posterior-error-probability estimation on NetMHCpan output~\cite{mhcvision2021}; the diagram here is a paired reliability comparison rather than a calibration method.

**Bibliography entries to add:**

```latex
\bibitem{munis2025}
Wohlwend, J.; Nathan, A.; Shalon, N.; et~al. Deep learning enhances the prediction of
HLA class~I-presented CD8 T cell epitopes in foreign pathogens.
\emph{Nat.~Mach.~Intell.} \textbf{2025}, \emph{7}, 232--243.
https://doi.org/10.1038/s42256-024-00971-y

\bibitem{mhcvision2021}
Pearngam, P.; Sriswasdi, S.; Pisitkun, T.; Jones, A.R. MHCVision: estimation of global
and local false discovery rate for MHC class~I peptide binding prediction.
\emph{Bioinformatics} \textbf{2021}, \emph{37}, 3830--3838.
https://doi.org/10.1093/bioinformatics/btab479
```

Cost: 2 bibliography entries + 3 sentences. Zero numbers change. Closes the single most likely reviewer objection.
