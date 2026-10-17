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
  - MUNIS — "Deep learning enhances the prediction of HLA class I-presented CD8+
    T cell epitopes in foreign pathogens." Nature Machine Intelligence 2024.
    https://www.nature.com/articles/s42256-024-00971-y  ·  PMC11847706
    Search-engine summary reports:
      "over 65% of positive epitopes in the evaluation dataset are also present in
       the training sets of existing predictors like TransPHLA and BigMHC"
      "Previous methodologies removed only matched HLA-I-peptide pairs from the
       training set, resulting in substantial overlap between test set epitopes and
       training sets, whereas a stricter approach involved removing all epitopes used
       in model evaluation from training sets, regardless of HLA-I restriction"

VERDICT:   WEAKENED  (possibly REFUTED — needs primary-source check)
EVIDENCE:  SECONDARY  (search-engine summary only; the primary abstract could not be
           retrieved — PubMed returned 0 for the MUNIS query, and the Nature page was
           not fetched in full this session)

NARROWED:  Pending primary-source check. If the MUNIS summary is accurate, then:
             - TransPHLA contamination HAS been quantified before (at ~65% under a
               stricter peptide-level criterion, vs our 26.9% under exact-pair)
             - our exact-(peptide,HLA)-pair protocol is the WEAKER criterion that
               MUNIS explicitly argues against
           The surviving honest framing would be:
             "we report an exact-pair decontamination ledger for TransPHLA against
              the NetMHCpan-4.1 training union, and ship it as machine-readable SI;
              stricter peptide-level criteria (e.g. MUNIS) remove more and are
              discussed in Limitations."
           Note the manuscript ALREADY concedes the lower-bound point at
           deepneo_information.tex:134-135 — the paper is internally honest; it is
           the cover letter's novelty framing that is at risk.

ACTION:    1. Retrieve MUNIS primary text and confirm/deny the 65% figure and the
              stricter-protocol description.
           2. Rewrite COVER_LETTER.md contribution #1 to drop the "not previously
              published" assertion.
           3. Consider citing MUNIS in Related Work (tex:82) and acknowledging the
              stricter-decontamination line of work.
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
| 1 | Calibration novelty | **REFUTED** | PRIMARY | ❌ must remove |
| 2 | Decontam-ledger novelty | **WEAKENED** | SECONDARY | ❌ must rewrite; primary check pending |
| 3 | "Most papers skip multiplicity control" | UNRESOLVED | none | ✅ paper's hedged form is fine |
| 4 | "Reproducibility unusual in sub-field" | UNRESOLVED | none | ⚠️ soften to factual |

## Literature gaps found (reviewer-visible risk)

Neither of these appears in the manuscript's 26-entry bibliography:

| Missing citation | Why it matters |
|---|---|
| **MHCVision** (Bioinformatics 2021, doi:10.1093/bioinformatics/btab479) | Directly prior art for probability calibration of NetMHCpan class-I output |
| **MUNIS** (Nat. Mach. Intell. 2024, s42256-024-00971-y) | Directly prior art for TransPHLA/BigMHC contamination quantification and for stricter peptide-level decontamination |

Suggested reviewers Bernett and Kalinina both work in biological-ML leakage methodology and are plausible readers of MUNIS.
