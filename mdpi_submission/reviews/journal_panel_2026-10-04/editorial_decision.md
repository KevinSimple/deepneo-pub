# Editorial Decision

## Manuscript Information
- **Title**: Efficient Protein Language Models for Peptide–MHC Ranking: A Leakage-Aware Evaluation Protocol under Multiplicity Control
- **Manuscript ID**: not assigned
- **Decision Date**: 2026-10-04
- **Review Round**: Round 1
- **Target**: MDPI *Information*, SI *Emerging Trends in Machine Learning and Natural Language Processing* (author-confirmed)
- **Source**: `academic-paper-reviewer` five-seat panel. Cards in `00_field_analysis.md`. Full seat texts in conversation; condensed cards in this folder.

## Review Panel Provenance

Role-separated cards only. Not an independence claim.

| Seat | Role ID | Actor type | Peer outputs visible | Model family | Provider | Human reviewer ID |
|---|---|---|---|---|---|---|
| Journal-Fit | EIC | AI subagent | no | same as panel | same | none |
| R1 Methodology | R1 | AI subagent | no | same | same | none |
| R2 Domain | R2 | AI subagent | no | same | same | none |
| R3 Perspective | R3 | AI subagent | no | same | same | none |
| Devil's Advocate | DA | AI subagent | no | same | same | none |

- **Role-separated**: true
- **Blind to peer outputs**: true (separate dispatches)
- **Model-family distinct**: false
- **Provider distinct**: false
- **Human-reviewer distinct**: false
- **Binary independence claim**: Not computed. Persona diversity proves only `role_separated`.
- **Correlated-error disclosure**: Same model family and provider. Consensus on Major Revision may be correlated. Treat overlapping HIGH items as one defect, not five independent votes.

`criteria_binding_unavailable` — no #684 Target Criteria Binding. Venue used as author-confirmed metadata only.

---

## Decision

### Major Revision

Repairable in one cycle. No new training run required. Not Reject: Table 1 three-condition verdicts still stand and DA found no CRITICAL that invalidates them. Not Minor: Related Work, public URL, title adjective, and contract-vs-table gaps need substantive rewrite and a site freeze.

---

## Blocking Issues (immutable source order)

| Transport | Blocking issue | Source | Evidence anchor | Resolving item |
|---|---|---|---|---|
| R1 | Closest PLM–pMHC prior art (Hashemi 2023) omitted; contribution (1) reads as introducing a PLM ranker | R2, DA-M1, EIC-W1 | Related Work L80–86; contribution L96 | REV-1 |
| R2 | Cited live URL advertises v4.2 “12/12” / p≈0; this Article claims ties | R3-W1, DA-M5 | L253, L286; https://deepneo.kevinwanglab.org/ | REV-2 |
| R3 | Evaluation contract not applied where Discussion still sells a win (dirty ablation; length “leads”; v4.2 under three-condition caption; “without the two confounders”) | R1-W1–W7, DA-M3–M4, R3-W2 | L170, L196, L232, L247, L251 | REV-3 |

---

## Reviewer Summary

| Reviewer | Role | Recommendation | Confidence |
|---|---|---|---|
| Journal-Fit | *Information* SI associate editor | Major Revision | 4 |
| Reviewer 1 | IEDB / DeLong / Holm methodologist | Major Revision | 5 |
| Reviewer 2 | pMHC-I / ESM–pMHC domain | Major Revision | 5 |
| Reviewer 3 | Responsible-ML / public-claim integrity | Major Revision | 4 |
| Devil's Advocate | Fixed adversarial seat | N/A — no CRITICAL; six MAJOR | N/A |

**Consensus:** 4/4 card-backed seats = Major Revision.

**Disagreement (adjudicated):**
- **GE as corresponding author.** EIC: Major (appearance). DA: Minor (MDPI SI Guidelines permit GE submissions if an Editorial Board member handles the file; disclosure is present). **Editorial ruling:** not a blocker for this venue. Recusal sentence stays. Moving `\corres` to K.W. is recommended, not required.
- **Title Efficient.** EIC/DA/R2: Major. **Ruling:** blocker via REV-3/REV-4 (same repair as dropping the adjective or adding a measured cost).
- **DeLong as a necessary condition.** R1 only. **Ruling:** methods clarification (REV-3), not a new experiment.

**DA CRITICAL vs Accept:** 0 validated CRITICAL. No `[DA-CRITICAL-VS-ACCEPT]` escalation.

---

## What the panel agrees is already honest

- Fusion-versus-fusion tie; NMP BA-head lead; fus-vs-NMP-BA not Holm-robust (digits MATCH SI JSON).
- Pocket rescorer withdrawn; 99.93% framed as overlap not accuracy.
- TransPHLA EL = binder labels; decontamination scoped as a lower bound in Methods.
- No clinical / Class II / TCR claim; no withdrawn >10σ headlines.

---

## Revision Roadmap (immutable core)

| ID | Action | Resolves |
|---|---|---|
| REV-1 | Cite Hashemi et al., *Front. Bioinform.* 2023, 3:1207380 (and preferably MHCRoBERTa 2022 / ImmunoBERT 2021). Rewrite contribution (1) as compact-trunk + leakage/Holm contract vs those PLMs, not “a PLM ranker.” Separate from-scratch transformers (TransPHLA) from pretrained PLMs. Optional: disambiguate the DeepNeo name vs Kim et al. NAR 2023. | R1 blocker; R2-W1; DA-M1 |
| REV-2 | Freeze or fork the URL cited in L253/L286 to the evaluated v4.1 ensemble and this Article’s tabled verdicts. Do not leave a 12/12 or p≈0 banner on the cited landing page. Reconcile `/` (12/12) vs `/v42/` (10/12). Align Discussion “is available” with DAS “was available at submission.” | R2 blocker; R3-W1; DA-M5 |
| REV-3 | Align claim language to the contract already in Methods. (a) Name v4.2 Table 1 rows as matched-corpus controls *outside* the four-row Holm family, or expand Holm+clustered CI to those rows. (b) Drop Discussion “without the two confounders”; use the lower-bound sentence. (c) Quarantine or re-run ablation on n=118,143; do not use dirty-set Δs to explain the clean tie. (d) Rewrite length “leads” / “significant margin” as a descriptive slice of the *non-Holm-robust* fus-vs-NMP-BA row. (e) Put IEDB per-week p=0.0453 next to per-ref p=0.65. (f) Restrict 0.442 to the IEDB BA probe; report TransPHLA inductive AUROCs if the ledger is cited. (g) One allele-inclusion rule for Wilcoxon / Holm / bootstrap, or disclose 91 vs 84 vs 112. | R3 blocker; R1-W1–W8; DA-M3–M4 |
| REV-4 | Retitle without Efficient, **or** add one measured cost (latency / memory / throughput vs NetMHCpan) from a committed artefact. Soften “competitive with NetMHCpan-4.1” to the TransPHLA fusion tie. | EIC-W2; R2-W3; DA-M2 |
| REV-5 | Fix the 29 Sep CS gloss: motif deconvolution is training-time NNAlign_MA (Alvarez 2019; Reynisson 2020), not assay-side. Soften pocket-rescorer “3-D cleft” to sequence-physchem at crystal contact positions. Rename “Deployed BA” → deployed fusion. | R2-W2/W4; DA-M6 |

Non-blocking (do if cheap): invert contribution order so the evaluation contract leads (EIC); replace “often” with qualitative wording (R3); say XAI is out of scope in Contributions; Holm 1979 cite; abstract ≤200 words; bib in appearance order; cover-letter date; DAS code sentence; optional move of corresponding authorship to K.W.

---

## Author questions the panel wants answered in the response letter

1. After Hashemi 2023, what is DeepNeo-CL’s increment?
2. Will the cited URL be frozen to v4.1 and this Article’s verdicts?
3. Which IEDB universe is primary (per-ref p=0.65 vs per-week p=0.0453)?
4. Will ablation be recomputed on n=118,143 or quarantined?

---

## Attachment: Acronym Check

Did not run (`scripts/check_acronyms.py` not invoked this session). Advisory only; not a reviewer finding.
