# Executable Documentation for Geometry Benchmarks — Anonymous Artifact Repo

This repository contains an updated release of the dataset and analysis code accompanying the submission
"Executable Documentation for Geometry Benchmarks" (ICML 2026, under review).

It includes:
- an expanded dataset release with **108 unique problems**,
- the construction-pattern coverage analysis code, and
- generated coverage tables supporting the reported **44.3%** coverage metric.

## Repository structure

  - `jgex_dataset.csv` — dataset (one row per problem, with annotations and JGEX fields)
  - `compute_construction_coverage.py` — computes construction-pattern coverage and writes a table
  - `coverage_summary.txt` — summary with observed/possible and fill ratio

## Construction coverage metric (summary)

Each problem is annotated with construction tokens drawn from the vocabulary:
`{bisector, circle, line, polygon, ray, segment}`.
Polygon subtypes (triangle/quadrilateral/etc.) are normalized to `polygon`. The token `point` is excluded from
coverage because it appears in nearly all problems and is non-discriminative (it is retained in the dataset).

A naive universe contains all non-empty subsets of the 6-token vocabulary: $2^6 - 1 = 63$.
We restrict to semantically valid combinations using the implications:
- `bisector => line`
- `polygon => segment`

This yields 35 valid combinations. Coverage is computed separately for `numerical_concept ∈ {yes,no}`,
doubling the valid universe to 70 combinations. In the current dataset, **31/70** combinations appear at least
once, giving **44.3% coverage**.


### Requirements
- Python 3.10+ (tested)
- `polars`
