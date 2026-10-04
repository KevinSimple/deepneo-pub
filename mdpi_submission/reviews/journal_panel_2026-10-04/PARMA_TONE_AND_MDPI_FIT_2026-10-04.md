# For Parma — tone options + what already meets MDPI *Information*

**Date:** 2026-10-04  
**Manuscript:** `latex/deepneo_information.tex`  
**Purpose:** Separate three questions that have been getting mixed together:

1. Does the Article **satisfy MDPI *Information* Article-type rules** (sections, abstract shape, keywords, back matter, COI)?
2. Will a **CS / ML reader of this Special Issue** understand the argument?
3. Are there still **scientific revisions** before Susy (prior art, live URL, a few claim-wording fixes)?

Those are different bars. (1) is largely yes. (2) is a tone choice — four options below, **numbers frozen**. (3) is real and listed at the end; it is not “the prose is too hard.”

No number, verdict, or citation is changed in any tone option.

---

## 1. There is no MDPI-specific “tone skill”

Closest installed tools (now in this pack under `.claude/skills/`):

| Tool | What it does | What it does *not* do |
|---|---|---|
| `academic-humanizer` | Shorter sentences, fewer stacked clauses, no em-dashes, verbs matched to evidence | Does not invent a house style called “MDPI” |
| `academic-paper` writing-quality check | Flags vague words (*leverage, robust, novel…*) and throat-clearing | Not a journal template |
| `academic-paper-reviewer` Journal-Fit seat | Would an *Information* SI editor send this out? | Not a copy-editor |
| `paper-writer` | Grounded drafting from committed artefacts | Does not set MDPI tone |

MDPI *Information* does **not** publish a “write simply for CS” style guide. Official Instructions ask for: one-paragraph abstract (~200 words), IMRaD, 3–10 keywords, CRediT, Data Availability, Conflicts. They do **not** ask for a popular-science register.

The Special Issue (*Emerging Trends in Machine Learning and Natural Language Processing*) expects applied-ML readers: transformers, leakage, multiple testing, domain adaptation. That *is* the CS audience for this venue. It is not “CS undergrad with no ML,” and it is not “immunology journal.”

---

## 2. What the journal-ready panel already said about writing

Five-seat `academic-paper-reviewer` panel, 2026-10-04 (`editorial_decision.md`). Same model family — treat overlapping comments as one defect, not five votes.

| Seat | Recommendation | What they said about **prose / CS readability** |
|---|---|---|
| Journal-Fit (*Information* SI editor persona) | Major Revision | **Writing Quality: MEETS.** “Prose is controlled and hedges where it should. The problem is framing order, not unreadable English.” |
| R1 Methodology | Major Revision | Did not flag CS incomprehension. Defects are statistical-family wording. |
| R2 Domain | Major Revision | Missing Hashemi 2023; one Methods gloss (motif deconvolution). Not “too complex.” |
| R3 Responsible-ML | Major Revision | Live URL vs PDF honesty. Writing Quality: MEETS. |
| Devil’s Advocate | 0 CRITICAL | Attacks novelty / title *Efficient* / URL. Not readability. |

**Consensus Major Revision is not “rewrite because CS readers will bounce.”** It is: add the closest PLM prior (Hashemi 2023), freeze the cited demo URL, and stop selling wins the three-condition rule already withdrew.

If the worry is “I (domain outsider) get lost in Methods,” that is a **supervisor-as-CS-reader** signal. The right fix is a **plainer Abstract + Intro** (options B–D), not another pass that adds more protocol vocabulary.

---

## 3. MDPI *Information* Article checklist (format — already met)

From official Instructions + `SCOPE_AND_GUIDELINES.md`. Journal-Fit seat confirmed the skeleton.

| Required item | Status now |
|---|---|
| Title, authors, ORCIDs, affiliation, corresponding author | Present |
| Abstract, single paragraph, ~200 words, background → methods → results → close | Present (at the cap; trim 1–5 words if the office enforces 200 strictly) |
| Keywords 3–10 | **7** (protein language models; transformers; sequence ranking; train–test leakage; multiple testing; peptide–MHC; evaluation protocol) |
| Introduction | Present |
| Materials and Methods | Present |
| Results | Present |
| Discussion | Present |
| Conclusions | Present (optional; we included it) |
| Supplementary Materials | Present |
| Author Contributions (CRediT) | Present |
| Funding | Present |
| Institutional Review / Informed Consent | Not applicable (public de-identified data) |
| Data Availability | Present (NetMHCpan folds not redistributed; SI JSON shipped) |
| Acknowledgments | Present |
| Conflicts of Interest | Present — P.N. named as SI Guest Editor; recusal stated |
| Cover letter: SI fit, not under consideration elsewhere, all authors approve | Present (`COVER_LETTER.md`; fill `[SUBMISSION DATE]` at upload) |
| English-text NLP claim | **Not made** — honest SI mapping (protein LM as sequence encoder) |

**Free-format at first submission** is official MDPI policy. Appearance-order bibliography can wait for production.

**Honest limit:** “Meets MDPI Article *format*” ≠ “ready to upload with zero scientific edits.” The panel still wants Hashemi + URL freeze + a few claim-wording fixes. Those do not change the CS-readability question.

---

## 4. How to talk about complexity without a fight

A useful split for the conversation:

| Feeling | What it usually is | What to do |
|---|---|---|
| “I don’t follow the immunology” | Expected: you are CS. MHC / HLA / EL need one gloss, then the paper should stay in ranking / leakage / multiple testing. | Pick Tone B or D for Abstract + Intro. Do not simplify Table 1. |
| “Too many protocol words” | The evaluation contract *is* the SI contribution. Cutting it makes the paper a Bioinformatics bake-off, which you already said you do not want. | Keep the three-condition rule; put it in one short box; do not repeat it in Abstract, Intro, Discussion, and Conclusions. |
| “ChatGPT’s abstract felt clearer” | That draft led with ranking + leakage and hid the biology. We already did that pass (26–29 Sep Style A). | If it still feels dense, the leftover density is **Methods/Results**, not the opener. Tone B/D only on Abstract + first Intro page. |

We should **not** tell you the paper is “already simple.” We should tell you: an *Information* SI editor-style review did **not** mark complexity as a defect; they marked title-word *Efficient*, contribution order, and the live URL.

---

## 5. Four tones — Abstract + opening Introduction only

All four keep the same facts:

- Task: rank ~100–10,000 peptides for one HLA context, before experiments.
- Method: compact transformer (ESM2-35M), trained on official NetMHCpan-4.1 BA and EL folds.
- Protocol: remove shared training pairs; predeclared multiple-testing rule.
- Results: fused TransPHLA **match**; IEDB weekly BA **mid-field**; small EL panel **lead**; NetMHCpan **keeps the BA-head lead**.
- Failure mode: a second-stage head fit on the evaluation set can look strong and then fail on held-out contexts.
- Close: competitive under a leakage-controlled comparison; not sold as uniformly better.

**Tone A** = current manuscript (already in the `.tex`).  
**Tones B–D** = alternatives for you to pick. If you pick one, we swap only Abstract + Intro opener; Table 1 stays.

---

### Tone A — Current (task, then ML)  
*Already in the file. This is the 26–29 Sep pass that followed your ChatGPT note.*

**Abstract (current).**  
Predicting which short peptides bind to and are presented by MHC class I proteins is an important step in neoantigen prioritisation and immunopeptidomics research, and a canonical biological sequence-ranking task: sort 100–10,000 peptide candidates against a fixed HLA allele, upstream of experimental validation. Pretrained protein language models (PLMs) are a natural encoder, but published gains are hard to read when test pairs already overlap the public training corpus or when many per-allele comparisons are counted as independent wins. We introduce DeepNeo-CL, a compact transformer ranker trained on the official NetMHCpan-4.1 binding-affinity (BA) and eluted-ligand (EL) folds, and compare it with NetMHCpan-4.1 after removing shared training pairs and applying a predeclared multiple-testing rule across alleles (Methods). In that setting DeepNeo-CL matches NetMHCpan-4.1 on the large third-party TransPHLA benchmark at the fused score we deploy, sits mid-field on the IEDB weekly BA board, and leads a small EL panel; NetMHCpan keeps the BA-head lead. A second-stage head fitted on the evaluation set itself can look strong in-sample and then fail on held-out contexts. A small PLM can therefore be a competitive sequence ranker against a strong industrial baseline when the comparison is leakage-controlled, without being sold as uniformly better.

**Intro opener (current).**  
Predicting which short peptides bind to and are presented by MHC class I proteins is an important step in neoantigen prioritisation and immunopeptidomics research pipelines. It is also an instance of a recurring machine-learning pattern: *ranking under a context key*, where a model scores many short candidates for one fixed conditioner.

*Feel:* honest, still dense. Two jobs in one sentence (biology + ML).  
*Risk:* a CS reader who does not know MHC hits the wall in sentence 1.

---

### Tone B — Plain CS (recommended if the complaint is “I get lost”)  
*`academic-humanizer` register: short sentences, every acronym glossed once, no stacked dashes.*

**Abstract.**  
This paper is a sequence-ranking study. The model scores many short amino-acid strings against one fixed context (an HLA protein) so that a later experiment can start from a shorter list. We use a small pretrained protein language model (ESM2, 35 million parameters) as the encoder. Published gains in this area are hard to trust when the test pairs already appear in the public training set, or when many contexts are tested and each small win is counted separately. We train DeepNeo-CL on the official NetMHCpan-4.1 binding-affinity and presentation folds, then compare it with NetMHCpan-4.1 after those shared pairs are removed and a predeclared multiple-testing rule is applied. On that protocol DeepNeo-CL matches NetMHCpan-4.1 on the large third-party TransPHLA set at the fused score we deploy, sits mid-field on the IEDB weekly binding board, and leads a three-predictor presentation panel. NetMHCpan remains ahead on the binding-affinity head. A second-stage head fitted on the evaluation set can look strong in-sample and then fail on held-out contexts. A small language model can therefore be competitive with a strong industrial baseline when the comparison is leakage-controlled. We do not claim that it is better on every cut.

**Intro opener.**  
A ranker scores many short candidates for one fixed context. Here the candidates are peptides (short amino-acid strings) and the context is an HLA protein. Two scores are used before any wet experiment: binding affinity, and presentation (whether the peptide was seen as an eluted ligand). We treat amino-acid strings as a discrete alphabet and encode them with a pretrained transformer (ESM2). Lists of 100–10,000 candidates are common, so a small ranking error wastes experimental budget.

*Feel:* a CS colleague can read the Abstract without Wikipedia.  
*Cost:* “neoantigen / immunopeptidomics” drop out of the first sentence (they stay in Methods / Limitations).  
*MDPI:* still one paragraph, same results clause.

---

### Tone C — SI-first (evaluation lesson leads)  
*What the Journal-Fit seat asked for: portable ML lesson first, pMHC as the worked example.*

**Abstract.**  
Train–test overlap and unadjusted multiple testing make published ranking gains hard to read. We study that evaluation problem on a biomedical sequence-ranking task: score 100–10,000 short peptides for one HLA context with a compact protein language model (DeepNeo-CL; ESM2-35M), trained on the official NetMHCpan-4.1 folds. After shared training pairs are removed and a predeclared multiple-testing rule is applied, DeepNeo-CL matches NetMHCpan-4.1 on the large third-party TransPHLA set at the fused score we deploy, sits mid-field on the IEDB weekly binding board, and leads a three-predictor presentation panel. NetMHCpan keeps the binding-affinity-head lead. A second-stage head fitted on the evaluation set can look strong in-sample and fail on held-out contexts — the usual transductive-overfitting failure. The contribution is the protocol as much as the model: a small language-model ranker can be competitive with an industrial baseline under leakage control, without being sold as uniformly better.

**Intro opener.**  
This article is about how to compare two rankers that were trained on the same public corpus. The running example is peptide–HLA ranking. The transferable pieces are pair-level decontamination, a predeclared multiple-testing rule, and a warning about second-stage heads fitted on the evaluation set.

*Feel:* reads as an *Information* SI paper.  
*Cost:* a biology-first reader waits one paragraph for MHC. You have previously wanted the concrete task first — this inverts that.  
*Use if:* you want the SI editor to see “evaluation integrity” in sentence 1.

---

### Tone D — Ultra-plain (one idea per sentence)  
*For a 15-minute read-through. Almost lecture notes. Still the same verdicts.*

**Abstract.**  
We compare two computer models that rank short protein fragments. The fragments are peptides. The context is one HLA protein. The encoder is a small protein language model (35 million parameters). We train it on the same official splits as NetMHCpan-4.1. Before we score, we delete any test pair that already appears in that training set. We also correct for testing many HLA types at once. After those two controls, our model matches NetMHCpan-4.1 on the large TransPHLA set when we use the fused score we actually deploy. On the public IEDB weekly binding board it sits in the middle of the field. On a three-model presentation board it ranks first. NetMHCpan is still better at the binding-affinity head. If we fit an extra head on the test data, the extra head looks strong and then fails on new HLA types. So a small language model can compete with the industrial tool when the test is fair. It is not better at everything.

**Intro opener.**  
Think of a ranking problem. You have one context and many short strings. The model must put the useful strings at the top of the list. In this paper the strings are peptides and the context is an HLA protein. Everything else is standard machine-learning evaluation: do not test on training pairs, and do not treat twenty related tests as twenty independent wins.

*Feel:* a CS student can follow it.  
*Cost:* some MDPI/SI readers will find it *too* plain for an Article (it can read as a blog). Use only if Tone B is still “too much.”  
*Do not* use Tone D in Methods or Table 1.

---

## 6. Suggested decision

| If Parma says… | Pick |
|---|---|
| “I still get lost in the first sentence” | **Tone B** for Abstract + Intro opener only |
| “This must look like an ML/NLP SI paper, not immuno” | **Tone C** |
| “Give me something I can read aloud in a meeting” | **Tone D** as a *cover note*; keep Tone B in the PDF |
| “The ChatGPT pass was fine; stop rewriting” | **Tone A** (current) |

Table 1, Holm, and the two case studies stay as they are. Complexity there is the science, not the tone.

---

## 7. What we should *not* claim in an email to Parma

Do **not** write: “The paper already meets all MDPI requirements and is ready to upload.”

Do write:

- The **Article-type format** (sections, keywords, CRediT, COI, Data Availability) **meets** the official *Information* Instructions.
- A Journal-Fit review aimed at this SI marked **writing quality as MEETS**. The remaining Major Revision items are prior art, the live URL, and a few claim sentences — not “CS readers will not understand.”
- We can swap Abstract + Intro to Tone B, C, or D **without changing a number**, if that makes the CS read easier.

---

## 8. Draft email (short)

Subject: MDPI draft — format is in place; please pick an Abstract/Intro tone

Hi Parma,

Quick split, because “too complex” and “not MDPI-ready” are different issues.

1. **MDPI *Information* Article format is in place** — required sections, ~200-word single-paragraph abstract, 7 keywords, CRediT, Data Availability, and the Guest-Editor COI line. Official Instructions do not ask for a popular-science register. This Special Issue’s readers are applied ML (transformers, leakage, multiple testing).

2. **A journal-fit review for this SI did not flag the English as the problem.** It said the prose is controlled. The remaining work is: cite the closest protein-LM prior paper, freeze the demo URL so it does not advertise a later model, and keep the Discussion aligned with Table 1 (we already call several comparisons ties). None of that is “add more explanation.”

3. **If the first page still feels heavy, that is a tone choice.** I drafted four Abstract + Intro versions with the **same numbers**. A is what is in the file now. B is plain CS (I recommend this if the opener is the pain). C leads with the evaluation lesson (more SI-shaped). D is ultra-plain, probably too informal for the PDF but useful as a read-aloud.

Could you mark A / B / C / D for the Abstract? I will not touch Table 1.

Thanks,  
Kevin
