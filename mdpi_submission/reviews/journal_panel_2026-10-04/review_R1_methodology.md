# Peer Review Report — R1 Methodology

**Recommendation:** Major Revision · **Confidence:** 5 · **Date:** 2026-10-04 · Round 1  
`criteria_binding_unavailable`

## Summary
v4.1 Table 1 digits match the ledgers (fusion tie; NMP BA-head lead; fus-vs-NMP-BA not Holm-robust). The contract is not applied uniformly: v4.2 rows sit under a three-condition caption without a Holm family or clustered CIs; row-level DeLong contradicts “allele as inferential unit”; Wilcoxon (91 alleles) and Holm (84) are different tests; ablation is on leaked n=161,652; Discussion says “without the two confounders” while Methods call cleaning a lower bound; length “leads” reuse the non-Holm-robust contrast; main text reports IEDB p=0.65 and withholds per-week p=0.0453; 0.442 is IEDB BA only.

## Major weaknesses
W1 v4.2 rows under three-condition caption without Holm/CI  
W2 Allele-as-unit vs required row-level DeLong  
W3 Wilcoxon 91-allele vs Holm 84-allele  
W4 “Without the two confounders” vs lower-bound pair cleaning  
W5 Dirty-set ablation used to explain clean-set tie  
W6 Length “leads” on fus-vs-NMP-BA (Holm 0.15)  
W7 Per-week Wilcoxon p=0.0453 omitted from Results  
W8 0.442 generalised; TransPHLA inductive AUROCs 0.87/0.89 omitted
