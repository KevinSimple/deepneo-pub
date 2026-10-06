# Narration script — DeepNeo-CL intro video (3:45)

**Target length:** 3 min 45 s · ~525 words at ~140 words-per-minute
**Register:** measured, confident, no boastful adjectives · plain English for a mixed CS+biology YouTube audience
**Delivery tip:** read each `[time]` block, breathe between blocks

---

**[0:00 – 0:15] HOOK**

Imagine your body as a city of billions of cells, each one holding up tiny protein fragments on its surface so the immune system can inspect what's being made inside. When something goes wrong — a virus, or a cancer mutation — those abnormal fragments get caught, and a T-cell comes along and kills the cell.

**[0:15 – 0:45] WHY IT MATTERS**

That inspection process is run by MHC class I proteins. They bind to short peptides from inside the cell and present them on the surface. Predicting which peptides a given MHC will present is one of the most important computational problems in immunology — it's the foundation of neoantigen vaccine design and cancer immunotherapy.

**[0:45 – 1:10] FRAMING AS ML**

In our paper, we approach this as a machine-learning problem: sequence ranking under a context key. You have ten-thousand candidate peptides, one HLA allele, and you need to rank them. We built DeepNeo-CL — a compact transformer, 35 million parameters, trained on the official NetMHCpan-4.1 folds.

**[1:10 – 1:30] PIVOT TO THE REAL CONTRIBUTION**

But the paper isn't really about the model. It's about how we evaluate.

**[1:30 – 2:05] THE PROBLEM WITH THE FIELD'S EVALUATIONS**

Here's the problem. The most-cited predictor in this field, NetMHCpan, trains on peptide-HLA pairs that end up in almost every public benchmark. If you don't remove the overlap, your test set is partly a train set, and your reported gains aren't real. On top of that, every paper reports results across dozens of HLA alleles — and treats each one as an independent win, so pure chance gives you lots of "significant" results.

**[2:05 – 2:25] OUR PROTOCOL**

So we did two things. We removed every shared training pair before scoring. And we applied Holm's multiple-testing correction across the family of allele-level comparisons. Here's what happens under that honest protocol.

**[2:25 – 2:45] HEADLINE RESULT — TRANSPHLA**

On the TransPHLA benchmark — 118-thousand clean rows after decontamination — our compact PLM matches NetMHCpan-4.1 at the fused score we deploy. Not better, not worse. Matched.

**[2:45 – 3:05] IEDB WEEKLY**

On the IEDB weekly leaderboard — 14 predictors scored over 46 weeks — we sit mid-field for binding affinity, and we lead the three-predictor eluted-ligand board.

**[3:05 – 3:15] HONEST — WHERE NETMHCPAN WINS**

NetMHCpan still beats us on the pure binding-affinity head. That's in Table 1. We don't hide it.

**[3:15 – 3:35] CASE STUDY — TRANSDUCTIVE OVERFITTING**

And here's the most interesting failure. We tried a second-stage rescoring head, fit by cross-validation on the evaluation benchmark itself. In-sample AUROC jumped to 0.862. Under a fair, allele-held-out protocol, it dropped to 0.442 — below chance. That's the classic transductive-overfitting trap. We withdrew the component.

**[3:35 – 3:45] TAKEAWAY + CTA**

The takeaway: a compact protein language model can rank peptide-MHC pairs competitively against a strong industrial baseline — when the comparison is leakage-controlled. Code and benchmark results at github.com/KevinSimple/deepneo-pub. Paper under review at MDPI *Information*. Thanks for watching.

---

## Delivery notes

- Pace: ~140 wpm overall. Slow down on the two numbers that matter most: **0.862** → **0.442** (section 3:15-3:35).
- Breathing: pause 0.5 s between the `[time]` blocks. The slide changes happen on those pauses.
- Tone: conversational-formal. Not reading-aloud rigid, not casual. Think "lab meeting voice".
- Avoid: "umm", "like", upspeak on statement endings. The claims are confident; let them land.

## What to record

Record one take of each block separately if you can — easier to re-record a bad block than redo everything. 7 blocks total. Descript's "fix flubs" feature makes this painless.
