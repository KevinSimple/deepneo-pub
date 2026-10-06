# YouTube upload metadata

Copy-paste these fields when uploading the final MP4 to YouTube.

---

## Title

```
DeepNeo-CL: A Compact PLM for Peptide–MHC Ranking — Leakage-Aware Evaluation (MDPI Information 2026)
```

## Description

```
NARRATION TRANSCRIPT:

Imagine your body as a city of billions of cells, each one holding up tiny protein fragments on its surface so the immune system can inspect what's being made inside. When something goes wrong — a virus, or a cancer mutation — those abnormal fragments get caught, and a T-cell comes along and kills the cell.

That inspection process is run by MHC class I proteins. They bind to short peptides from inside the cell and present them on the surface. Predicting which peptides a given MHC will present is one of the most important computational problems in immunology — it's the foundation of neoantigen vaccine design and cancer immunotherapy.

In our paper, we approach this as a machine-learning problem: sequence ranking under a context key. You have ten-thousand candidate peptides, one HLA allele, and you need to rank them. We built DeepNeo-CL — a compact transformer, 35 million parameters, trained on the official NetMHCpan-4.1 folds.

But the paper isn't really about the model. It's about how we evaluate.

Here's the problem. The most-cited predictor in this field, NetMHCpan, trains on peptide-HLA pairs that end up in almost every public benchmark. If you don't remove the overlap, your test set is partly a train set, and your reported gains aren't real. On top of that, every paper reports results across dozens of HLA alleles — and treats each one as an independent win, so pure chance gives you lots of "significant" results.

So we did two things. We removed every shared training pair before scoring. And we applied Holm's multiple-testing correction across the family of allele-level comparisons.

On the TransPHLA benchmark — 118-thousand clean rows after decontamination — our compact PLM matches NetMHCpan-4.1 at the fused score we deploy. Not better, not worse. Matched.

On the IEDB weekly leaderboard — 14 predictors scored over 46 weeks — we sit mid-field for binding affinity, and we lead the three-predictor eluted-ligand board.

NetMHCpan still beats us on the pure binding-affinity head. That's in Table 1. We don't hide it.

And here's the most interesting failure. We tried a second-stage rescoring head, fit by cross-validation on the evaluation benchmark itself. In-sample AUROC jumped to 0.862. Under a fair, allele-held-out protocol, it dropped to 0.442 — below chance. That's the classic transductive-overfitting trap. We withdrew the component.

The takeaway: a compact protein language model can rank peptide-MHC pairs competitively against a strong industrial baseline — when the comparison is leakage-controlled. Code and benchmark results at github.com/KevinSimple/deepneo-pub. Paper under review at MDPI Information. Thanks for watching.

———————————————————————

A 3-minute introduction to our paper:

"Efficient Protein Language Models for Peptide–MHC Ranking: A Leakage-Aware Evaluation Protocol under Multiplicity Control"

Kevin Wang · Parma Nand
School of Design and Creative Technologies, Auckland University of Technology
MDPI Information — Special Issue: Emerging Trends in Machine Learning & Natural Language Processing

WHAT THIS VIDEO COVERS:
0:00 — Hook: how immune surveillance works
0:15 — Why peptide–MHC prediction matters for cancer immunotherapy
0:45 — Framing as a sequence-ranking ML problem
1:10 — The real contribution: how we evaluate
1:30 — Two problems with the field's evaluations (train–test leakage + multiple testing)
2:05 — Our three-condition superiority rule
2:25 — Headline result: DeepNeo-CL matches NetMHCpan-4.1 on decontaminated TransPHLA
2:45 — IEDB weekly leaderboard results
3:05 — Where NetMHCpan still wins (honest reporting)
3:15 — Case study: transductive overfitting failure (0.862 → 0.442)
3:35 — Takeaway and resources

KEY RESULTS:
• 35M-parameter protein language model (ESM2 trunk + cross-attention)
• Matches NetMHCpan-4.1 at the deployed fusion level on 118K clean TransPHLA rows
• Leads the IEDB eluted-ligand board (mean rank 1.80 across 46 weeks)
• Documents a transductive-overfitting failure as a negative result

CODE & EVIDENCE:
https://github.com/KevinSimple/deepneo-pub
— 515-claim evidence audit (100% MATCH)
— Supplementary JSON ledgers for all reported numbers
— Two formal compliance reports

#DeepNeo #PeptideMHC #ProteinLanguageModel #MachineLearning #Immunoinformatics #CancerImmunotherapy #Neoantigen #Bioinformatics #NetMHCpan #MDPI
```

## Tags

```
DeepNeo-CL, peptide MHC, protein language model, MHC class I, binding prediction, neoantigen, cancer immunotherapy, NetMHCpan, immunoinformatics, bioinformatics, machine learning, deep learning, ESM2, evaluation protocol, leakage, train test leakage, multiple testing, Holm correction, TransPHLA, IEDB, AUROC, MDPI Information
```

## Category

```
Science & Technology
```

## Thumbnail

Use `thumbnail_option2.svg` (the "0.862 → 0.442" number hook — highest curiosity gap).

Convert to PNG: `rsvg-convert -w 1280 -h 720 thumbnail_option2.svg > thumbnail2.png`
Or open in browser and screenshot at 1280x720.

## Caption file

Upload `captions.srt` as English subtitles.

## Visibility

Set to **Unlisted** initially (paper under review). Switch to Public after acceptance.
