# DeepNeo-CL v4.2 — public benchmark & model card

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
(published 2025-08-07) and evaluated against the version-pinned NetMHCpan-4.2c executable on
two benchmarks, each decontaminated against the v4.2 training corpus:

| Benchmark | n | positives | DeepNeo v4.2 EL AUROC | NetMHCpan-4.2c AUROC | Δ (EL) | DeLong p | per-allele Wilcoxon |
|---|---:|---:|---:|---:|---:|---:|---|
| **mono_el_v2 strict-sequence-disjoint** | 108,165 | 1,889 | **0.6433** [0.6294, 0.6572] | 0.6012 [0.5864, 0.6164] | **+0.042** | 2.7e-11 | 10/12 alleles, p=0.002 |
| **TransPHLA exact-disjoint** | 117,884 | 37,370 | **0.9685** [0.9675, 0.9695] | 0.9492 [0.9478, 0.9506] | **+0.019** | 9.5e-292 | 64/93 alleles, p=9.5e-5 |

**Binding-affinity (BA) head:** wins on mono_el_v2 strict-disjoint (ΔAUROC +0.019, DeLong
p=1.8e-4) and is **statistically tied** with NetMHCpan-4.2c on TransPHLA (per-allele Wilcoxon
p=0.79).

**In one sentence:** DeepNeo-CL v4.2's **presentation (EL) head consistently beats
NetMHCpan-4.2c on both decontaminated benchmarks**, at every level of sequence-identity
stringency including the strictest 8-mer-disjoint cut; the binding head is competitive-to-ahead.
All reported significant results survive Holm / Benjamini-Hochberg multiple-testing correction.

---

## What's in this repository

| Path | Contents |
|---|---|
| [`BENCHMARK_SCOPE.md`](BENCHMARK_SCOPE.md) | Definition of the two canonical benchmarks + full canonical numbers |
| [`MODEL_CARD.md`](MODEL_CARD.md) | Model identity, training-data provenance, checkpoint SHA-256 hashes |
| [`results/*.json`](results/) | Full statistical reports (AUROC/AUPR + 10k-bootstrap CIs, per-allele tables, calibration ECE/Brier, paired DeLong + Wilcoxon) |
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
- **Scoring.** DeepNeo is a 5-fold ensemble; NetMHCpan-4.2c is the unmodified DTU executable.
  Both score identical rows.
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
> and presentation — benchmark & model card.* 2026. GitHub: KevinSimple/deepneo-pub.
> *(A Zenodo DOI will be minted from a release of this repository — add it here once issued.)*

---

*Research record maintained by [@KevinSimple](https://github.com/KevinSimple). NetMHCpan-4.2 is
by Nilsson et al. (Frontiers in Immunology, 2025); it is used here only as a version-pinned
reference predictor on identical rows.*
