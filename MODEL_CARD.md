# Model card — DeepNeo-CL v4.2

## Identity

| Field | Value |
|---|---|
| Model | DeepNeo-CL v4.2 |
| Task | MHC-I peptide **binding affinity (BA)** + **eluted-ligand / presentation (EL)** prediction |
| Base encoder | ESM2-35M (`facebook/esm2_t12_35M_UR50D`), public, frozen |
| Adaptation | parameter-efficient fine-tuning (LoRA) on the frozen trunk + peptide × HLA cross-attention; multitask BA + EL heads |
| Inference unit | 5-fold ensemble (mean of per-fold sigmoids) |
| Reference predictor (benchmarks) | NetMHCpan-4.2c (version-pinned DTU executable, unmodified) |

> Full architecture and training details are **withheld pending peer-reviewed publication.**
> The information above establishes the model's identity; the hashes below establish provenance.

## Training data provenance

| Field | Value |
|---|---|
| Training archive | NetMHCpan-4.2 official supplementary `NetMHCpan_train` |
| Archive SHA-256 | `4f8393e19e781c40340f25effadb86364082063e6a65bb8676ceb728e7a40386` |
| Source publication | Nilsson et al., *Frontiers in Immunology*, 7 Aug 2025 (DOI 10.3389/fimmu.2025.1616113) |
| Partition | official 5-fold (c000–c004) |

DeepNeo-CL v4.2 was trained **only** on this public archive — the same public data available to
any NetMHCpan-4.2 user — which is what makes the post-cutoff, decontaminated head-to-head a fair
test of generalization rather than of data access.

## Trained-checkpoint SHA-256 (weights NOT distributed)

Each checkpoint file is 145,476,945 bytes. These hashes are published to establish provenance
and a verifiable timestamp; the weight files themselves are withheld pending publication.

| Fold | SHA-256 |
|---|---|
| c000 | `e66a6876ee24a63e8dd6cd76aad7a58d26bc018df7990dd102a649c34f7e2542` |
| c001 | `19adc4a2e813dc21cbad80430d3b12589a3617b17bf2806bd80de324b6c489dd` |
| c002 | `f97176ab9e86d589554aa2d52948c753a5bb0a0a5658157abde0b3a6e42cf7fd` |
| c003 | `8693546ca84e46cb6256f534a26e0a4a61901f2141a7201e2ae1216ccf1a7d0e` |
| c004 | `57ebbbdd19de55f88088915daad5f18aab466a3d7663b281b618a1a5b7b67820` |

## Evaluation

See [`BENCHMARK_SCOPE.md`](BENCHMARK_SCOPE.md) and [`results/`](results/) for the two canonical
benchmarks, full statistics, and per-allele tables. Live model: https://deepneo.kevinwanglab.org/v42/

## Intended use & limitations

- Research use: ranking candidate MHC-I peptides by predicted binding / presentation.
- Not a clinical tool. Coverage is limited to the HLA-A/B alleles present in the benchmark
  studies; performance on unseen alleles is not characterized here.
- The reference comparison is NetMHCpan-4.2c only; no claim is made against other predictors.
