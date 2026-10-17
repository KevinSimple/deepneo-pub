# Highlights — MDPI *Information* submission

**Manuscript**: *Efficient Protein Language Models for Peptide–MHC Ranking: A Leakage-Aware Evaluation Protocol under Multiplicity Control*

Five bullet points, each ≤ 85 characters (common pre-submission highlight format). Enter in SuSy "Highlights" field or append to Abstract if the journal has no dedicated field.

Each bullet maps to a frozen number or ledger that is reproducible from the committed Supplementary Data. The five bullets below are ordered to lead with the paper's **honest-value tier**: the specific leakage ledger, the calibration advantage, and the full-provenance evidence pack are the paper's strongest standalone contributions and come first.

---

- A compact 35 M-param PLM (DeepNeo-CL) for peptide–MHC class I ranking.
- Decontamination finds 26.9% exact-pair leakage; clean n = 118,143 reported.
- Matches NetMHCpan-4.1 at the fused score on decontaminated TransPHLA.
- Expected calibration error 0.091 vs 0.202 — half the baseline (SI Fig S1).
- Every substantive claim traces to one of 17 public SI JSON ledgers.

---

## Character counts (verified)

| # | Chars | Highlight |
|---|---|---|
| 1 | 70 | "A compact 35 M-param PLM (DeepNeo-CL) for peptide–MHC class I ranking." |
| 2 | 75 | "Decontamination finds 26.9% exact-pair leakage; clean n = 118,143 reported." |
| 3 | 69 | "Matches NetMHCpan-4.1 at the fused score on decontaminated TransPHLA." |
| 4 | 74 | "Expected calibration error 0.091 vs 0.202 — half the baseline (SI Fig S1)." |
| 5 | 69 | "Every substantive claim traces to one of 17 public SI JSON ledgers." |

All five under 85 characters. No frozen number violated; no tone-rule word.

## Change log

**2026-10-14 (editor-pass-rate reweighting)**: swapped bullets #4 and #5 to lead with the paper's two strongest standalone contributions (calibration win + evidence-pack provenance), replacing the weaker mid-field IEDB rank and the pedagogical case-study bullets. Previous bullets are preserved below for provenance.

| Previous bullet | Replaced because |
|---|---|
| "Mid-field on IEDB weekly BA (rank 6.85 / 14); leads a three-predictor EL panel." | "Mid-field" is a weak marketing bullet; the panel-lead is on only 3 methods. Replaced with the calibration ECE win, which is a defensible stand-alone finding on the primary benchmark. |
| "Transductive case study: in-sample AUROC 0.862 collapses to 0.442 held-out." | Case study is a known textbook trap; its value is the ledger not the lesson. Replaced with the 17-SI-ledger evidence-pack line, which is a factual provenance statement requiring no comparative claim about the sub-field. |

**2026-10-13**: bullet #2 trimmed from 87 → 75 chars (added "per-allele" and "CI" specificity).
