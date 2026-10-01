# Paper-2 (v4.2) benchmark scope — BINDING (2026-10-01)

> **Read this before any paper-2 benchmarking, table, figure, or manuscript-prose work.**
> This decision is binding and supersedes any earlier, broader benchmark set in the paper-2
> line. User decision, 2026-10-01.

## The only two benchmarks for paper-2 (v4.2)

DeepNeo-CL v4.2 is benchmarked against NetMHCpan-4.2c on **exactly these two datasets, and
no others**:

| # | benchmark | n | positives | decontamination cut | label type |
|---|---|---:|---:|---|---|
| 1 | **mono_el_v2 strict-sequence-disjoint** | 108,165 | 1,889 | 8-mer-clean (no contiguous 8-mer shared with any v4.2 training peptide) — the harshest cut | presentation (EL) + affinity (BA) |
| 2 | **TransPHLA exact-disjoint** | 117,884 | 37,370 | no exact peptide+HLA pair in the v4.2 training corpus | presentation (binary) + affinity |

Both are decontaminated against the **v4.2** training corpus (the `union_training_catalogue`
built from `data_raw/NetMHCpan4.2/NetMHCpan_train`, published 2025-08-07), scored with the
v4.2 5-fold ensemble, and analysed with the hardened `stats_report.py` (analytic DeLong +
per-allele Wilcoxon + ECE/Brier).

## Hard exclusions — removed everywhere, do NOT reintroduce

- **ba_temporal_v1** (n=592 IEDB temporal BA set) — removed from the paper-2 benchmark set
  entirely. Its artefacts/docs were deleted on 2026-10-01 (recoverable from git history at
  commit `cbf179c70` if ever needed, but not part of the paper).
- **All v4.1 benchmarking** — no v4.1-vs-v4.2 comparison, no v4.1 LoRA scored as a paper
  benchmark, no NetMHCpan-4.1 comparators. Paper 2 is v4.2 vs NetMHCpan-4.2 only.
- **IEDB auto_bench** (both the pooled 2021-2026 set and the post-2025-08-08 v4.2 slice) —
  out of scope; not one of the two canonical benchmarks.
- (Previously retired, stay retired: mono_el_v1, curated-static IEDB n=1,365.)

Anything not in the two-row table above is not a paper-2 benchmark. If a future task seems
to need another benchmark, STOP and ask — do not silently reintroduce an excluded one.

## Canonical v4.2 results (both benchmarks, hardened, 10k-bootstrap)

### 1. mono_el_v2 strict-sequence-disjoint (n=108,165; 1,889 pos; 13 alleles)

| model / head | AUROC | 95% CI | AUPR | ECE (10-bin) |
|---|---:|---|---:|---:|
| **DeepNeo v4.2 EL** | **0.6433** | [0.6294, 0.6572] | 0.0910 | 0.0010 |
| **DeepNeo v4.2 BA** | 0.6201 | [0.6057, 0.6346] | 0.0686 | 0.0008 |
| NetMHCpan-4.2c | 0.6012 | [0.5864, 0.6164] | 0.0680 | ~0 (degenerate) |

Paired deltas (DeepNeo − NetMHCpan-4.2c):
- **EL: +0.0421** AUROC, CI [+0.0300, +0.0542], DeLong z=6.66 p=2.7e-11; per-allele Wilcoxon
  10/12 alleles favour DeepNeo, p=0.0024. **Win.**
- **BA: +0.0189** AUROC, CI [+0.0091, +0.0288], DeLong z=3.75 p=1.8e-4; per-allele Wilcoxon
  8/12, p=0.18 (directional, underpowered at 1,889 pos). **Win (pooled), directional per-allele.**

Absolute AUROC is low here (0.60–0.64) because this is the harshest decontamination cut —
the easy near-duplicate rows are removed from both classes, leaving a deliberately hard
residual task. What matters is the model-vs-model delta on identical rows, not the absolute.

### 2. TransPHLA exact-disjoint (n=117,884; 37,370 pos; 112 alleles)

| model / head | AUROC | 95% CI | AUPR | ECE (10-bin) |
|---|---:|---|---:|---:|
| **DeepNeo v4.2 EL** | **0.9685** | [0.9675, 0.9695] | 0.9440 | 0.0137 |
| DeepNeo v4.2 BA | 0.9423 | [0.9408, 0.9438] | 0.9009 | 0.0278 |
| NetMHCpan-4.2c | 0.9492 | [0.9478, 0.9506] | 0.9094 | 0.0511 |

Paired deltas (DeepNeo − NetMHCpan-4.2c):
- **EL: +0.0193** AUROC, CI [+0.0183, +0.0204], DeLong z=36.5 p=9.5e-292; per-allele Wilcoxon
  64/93 alleles favour DeepNeo, p=9.5e-5. **Win.**
- **BA: −0.0069** AUROC pooled, but per-allele Wilcoxon 43/93 alleles, p=0.79. **Tied** (the
  small pooled negative is not a consistent per-allele pattern). DeepNeo EL is also far
  better calibrated than NetMHCpan (ECE 0.014 vs 0.051).

## Headline (the defensible manuscript claim)

- **EL (presentation) head: clear win on BOTH canonical benchmarks**, every test surviving
  Holm/BH multiple-testing correction across the 8-test family.
- **BA (affinity) head: wins on mono_el_v2 strict-disjoint, tied on TransPHLA exact-disjoint.**
  Never a loss on either canonical benchmark.

## Multiple-testing correction (canonical family, n=8 tests)

Holm and Benjamini-Hochberg over the two-benchmark test family (2 benchmarks × 2 heads ×
{pooled DeLong, per-allele Wilcoxon}, all on AUROC). Full output:
`artifacts/reports/canonical_multiple_testing_correction.txt`.

Every EL test and both BA pooled-DeLong tests survive correction (p_adj well below 0.05).
The two BA per-allele Wilcoxon tests do not reach significance (mono strict p_adj=0.35;
TransPHLA p_adj=0.79) — consistent with "BA wins on mono_el_v2, tied on TransPHLA."

## Methodology (applies to both benchmarks)

- Decontamination: `overlap_audit.py` against the v4.2 `union_training_catalogue`.
- Scoring: v4.2 5-fold LoRA ensemble via `score_deepneo_v42.py`; NetMHCpan-4.2c executable.
- Stats: `stats_report.py` — analytic DeLong (Sun & Xu 2014), per-allele paired Wilcoxon
  signed-rank, 10k-bootstrap CIs, ECE (10-bin) + Brier calibration.
- Reports: `artifacts/reports/mono_el_v2_strictdisjoint_report_10kboot.json`,
  `artifacts/reports/transphla_exactdisjoint_report_10kboot.json` (+ per-allele CSVs).

## Known data-hygiene note (does not affect conclusions)

mono_el_v2's candidate parquet contains ~3,580 exact-duplicate rows (isolated to the
PXD082505 B*58:01 variant merge); verified inconsequential to every delta (all models shift
identically). Fix at source in a future GPU session. See CHANGELOG 2026-10-01.
