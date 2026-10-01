# DeepNeo-CL v4.2 — public benchmark & model card

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23073342.svg)](https://doi.org/10.5281/zenodo.23073342)

A LoRA-adapted protein language model for **MHC-I peptide binding & presentation** prediction,
benchmarked head-to-head against **NetMHCpan-4.2c** on two independently decontaminated,
post-training-cutoff test sets.

**Live interactive dashboard:** https://deepneo.kevinwanglab.org/v42/
*(predict peptides online, and explore every benchmark chart — ROC/PR per allele, per-allele
scatter, calibration, decontamination audit)*

> This repository is a **public, citable record of the benchmark results and model card**.
> It deliberately does **not** contain model weights or training code (see
> *Availability* below). Trained-checkpoint SHA-256 hashes are published here to establish
> provenance and a verifiable timestamp.

---

## Headline result

DeepNeo-CL v4.2 was trained only on the public **NetMHCpan-4.2 supplementary training archive**
(published 2025-08-07) and evaluated against **four field-standard reference predictors** —
**NetMHCpan-4.2c** (2025), **MHCflurry-2.0** (2020), **BigMHC** (2023), and **MixMHCpred v3**
(2024) — on identical rows of two benchmarks.

**Presentation task — AUROC:**

| Model | mono_el_v2 strict-disjoint *(fair primary)* | TransPHLA exact-disjoint *(secondary)* |
|---|---:|---:|
| **BigMHC (2023)** | **0.6803** | 0.9583 |
| DeepNeo v4.2 EL | 0.6433 | **0.9685** |
| MHCflurry-2.0 presentation | 0.6389 | **0.9715** |
| NetMHCpan-4.2c | 0.6012 | 0.9492 |
| MixMHCpred v3 (2024) | 0.5970 | 0.9456 |

**In one sentence (honest, no cherry-picking):** DeepNeo-CL v4.2 is a **consistent top-tier
presentation predictor — clearly superior to NetMHCpan-4.2c and MixMHCpred, on par with
MHCflurry-2.0, and trading the lead with BigMHC** (behind BigMHC on the fair 2026 mono-allelic
benchmark, ahead of it on TransPHLA). **BigMHC is the single strongest model on the genuinely
fair benchmark; no model dominates both.** All significant results survive Holm / Benjamini–
Hochberg correction. (Binding-affinity head: MHCflurry-2.0's affinity predictor leads; DeepNeo
BA still beats NetMHCpan-4.2c on the strict mono-allelic set.)

### Fairness — which benchmark to trust, and the limits of decontamination

No head-to-head can *guarantee* a peptide was never seen by a third-party model whose full
training set is not public (immunopeptidome peptides recur across datasets). We control for this
three ways, strongest first:

1. **Temporal gate.** mono_el_v2's three PRIDE studies are all **2026** — after every model
   version (NetMHCpan-4.2 2025, MixMHCpred 2024, BigMHC 2023, MHCflurry 2020). No model could
   have trained on these specific studies ⇒ **mono_el_v2 is the fair primary benchmark.**
2. **Shared-public-well decontamination** against a 17.6M union catalogue including IEDB + CEDAR
   (the common training source) removes most recurring pairs for *all* models, not just DeepNeo.
3. **BigMHC double-decontamination (direct test).** Using BigMHC's own public 17M-pair training
   set, we built a subset (n=70,400) **neither DeepNeo nor BigMHC trained on**: BigMHC **0.6726**
   vs DeepNeo **0.6304** (DeLong *p*=1.5e-15) — the gap is unchanged, so **BigMHC's advantage is
   real, not a contamination artifact.**

**TransPHLA (2022)** predates the 2023+ models, so it is *temporally confounded* for them and is
reported only as a secondary benchmark. **Residual limitation:** only DeepNeo's training is fully
controlled; any residual overlap in a baseline's private data biases *toward the baseline*, so
DeepNeo's standing here is conservative.

Full numbers, CIs, per-allele Wilcoxon, and DeLong tests are in [`results/`](results/)
(`multiway_*.json` = 5-model comparisons; `multiway_mono_doubledisjoint_bigmhc.json` = the fair
BigMHC cut).

---

## What's in this repository

| Path | Contents |
|---|---|
| [`BENCHMARK_SCOPE.md`](BENCHMARK_SCOPE.md) | Definition of the two canonical benchmarks + full canonical numbers |
| [`MODEL_CARD.md`](MODEL_CARD.md) | Model identity, training-data provenance, checkpoint SHA-256 hashes |
| [`results/*_report_10kboot.json`](results/) | Full statistical reports (AUROC/AUPR + 10k-bootstrap CIs, per-allele tables, calibration ECE/Brier, paired DeLong + Wilcoxon) |
| [`results/multiway_*.json`](results/) | 5-model comparison (DeepNeo / NetMHCpan-4.2c / MHCflurry-2.0 / BigMHC / MixMHCpred) per benchmark, incl. `multiway_mono_doubledisjoint_bigmhc.json` = the fair DeepNeo-vs-BigMHC cut |
| [`results/threeway_*.json`](results/) | earlier 3-way comparison (DeepNeo vs NetMHCpan-4.2c vs MHCflurry-2.0), superseded by the multiway reports |
| [`results/*_per_allele.csv`](results/) | Per-allele AUROC/AUPR for both models, both benchmarks |
| [`results/canonical_multiple_testing_correction.txt`](results/canonical_multiple_testing_correction.txt) | Holm + Benjamini-Hochberg correction over the test family |

Every number on the live dashboard and in this README is reproducible from these JSON files.

---

## Methodology (summary)

- **Decontamination.** Each benchmark's peptides are audited against a 17.6 M-row union
  catalogue assembled from NetMHCpan-4.2's public training partitions, keyed on both the exact
  (peptide, HLA) pair and any contiguous 8-mer sub-string. Two locked cuts: *exact-disjoint*
  (no exact pair in training) and *strict-sequence-disjoint* (no shared 8-mer at all). The
  mono_el_v2 benchmark is reported at the **strict** cut — the harshest available.
- **Temporal gate.** Mono-allelic eluted-ligand positives come from three post-cutoff PRIDE
  immunopeptidomics studies (first-public date after the NetMHCpan-4.2 release), so neither
  model could have trained on them.
- **Scoring.** DeepNeo is a 5-fold ensemble; **NetMHCpan-4.2c** is the unmodified DTU
  executable; **MHCflurry-2.0** is the openvax `Class1PresentationPredictor` (presentation +
  affinity). All three score identical rows.
- **Statistics.** AUROC/AUPR with 10,000-iteration bootstrap CIs; paired significance via the
  analytic DeLong test; a per-allele paired Wilcoxon signed-rank test (so a win reflects a
  consistent per-allele pattern, not just a large pooled n); calibration via 10-bin ECE +
  Brier; Holm/BH correction across the full test family.

---

## Honest caveats

- **Absolute AUROC on the strict mono_el_v2 cut is low (~0.60–0.64) by design** — the strict
  8-mer-disjoint cut removes every near-duplicate from both classes, leaving a deliberately
  hard residual task. The meaningful quantity is the *model-vs-model delta on identical rows*,
  not the absolute value. (The same alleles score ~0.84 on the easier full set.)
- **mono_el_v2 strict-disjoint has few positives per allele** (13 alleles; several with
  <20 positives) — those per-allele AUROCs are high-variance and are shown as the smallest
  points on the dashboard scatter.
- **Coverage.** 13 HLA-A/B alleles for mono_el_v2 (limited by which mono-allelic cell lines the
  source studies profiled); HLA-B*07:01 is unsupported by NetMHCpan-4.2 and excluded from
  paired comparisons.
- **TransPHLA** is a balanced classic benchmark decontaminated at the exact-pair level
  (72.9% of rows retained); it is reported as a second, independent corroboration of the
  mono-allelic result.

---

## Availability

- **Results & model card:** this repository (open).
- **Interactive model:** the live dashboard lets anyone run predictions online —
  https://deepneo.kevinwanglab.org/v42/
- **Model weights and training code:** *withheld pending peer-reviewed publication.* The
  five trained-checkpoint SHA-256 hashes are published in [`MODEL_CARD.md`](MODEL_CARD.md) to
  establish provenance and a verifiable timestamp without releasing the weights.

---

## License

The benchmark results, model card, documentation, and data files in this repository are
licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)** —
see [`LICENSE`](LICENSE). You may share and adapt the material, including commercially,
provided you give appropriate credit. (Model weights and training code are not included and
are not covered by this license.)

## Citation

> Wang, K. *DeepNeo-CL v4.2: a LoRA-adapted protein language model for MHC-I peptide binding
> and presentation — benchmark & model card.* 2026. Zenodo.
> https://doi.org/10.5281/zenodo.23073342
>
> *(Concept DOI — always resolves to the latest version. This specific release, v1.0.0, is
> 10.5281/zenodo.23073343.)*

---

*Research record maintained by [@KevinSimple](https://github.com/KevinSimple). NetMHCpan-4.2 is
by Nilsson et al. (Frontiers in Immunology, 2025); it is used here only as a version-pinned
reference predictor on identical rows.*
