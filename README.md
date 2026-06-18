# Covariate Reconstruction in Individual Patient Data

This repository contains research code for studying uncertainty in reconstructed individual patient data (IPD) derived from published clinical trial summaries.

Rather than treating a reconstructed dataset as a single fixed object, this project investigates the collection of all feasible patient-level datasets that satisfy published subgroup constraints and summary statistics. The central objective is to understand how treatment-effect estimates vary across the feasible reconstruction space and to develop methods for identifying both typical and extremal solutions.

**Author:** Jonathan Ma, Sijia Zhu

---

## Aim

Published clinical trials frequently report subgroup-level summaries without releasing the underlying patient-level data. Existing reconstruction methods can recover approximate patient-level datasets from Kaplan-Meier curves, subgroup summaries, and aggregate trial information. However, many different patient-level assignments may be consistent with the same published constraints.

This project studies the following question:

> Given reconstructed IPD and published subgroup constraints, what is the geometry of the feasible reconstruction space?

The long-term goal is to characterize uncertainty induced by subgroup reconstruction and determine how treatment-effect conclusions change across the set of all feasible patient-level datasets.

---

## Data Sources

### Synthetic Survival Data

Initial development uses simulated survival datasets with known subgroup labels. These experiments provide a controlled environment where the true subgroup assignment is available for evaluation and benchmarking.

### Reconstruction Methods

The repository currently incorporates code and methodology from:

- CEN-KM
- VEC-KM
- RESOLVE-IPD
- MAPLE

These methods provide reconstructed patient-level datasets that serve as inputs to the feasible-space analysis.

### Clinical Trial Publications

Complete pipeline testing will be performed on published subgroup analyses, including:

- ATTRACTION-3
- KEYNOTE-181
- ESCORT

Additional clinical trial case studies may be added as the framework develops.

---

## Methodology

The workflow begins with a reconstructed patient-level dataset obtained from Kaplan-Meier reconstruction methods and published subgroup summaries. Given these inputs, we construct the set of feasible subgroup assignments that satisfy reported constraints and evaluate how treatment-effect estimates vary across this feasible region.

The initial focus of the project is on extremal-search methods. Standard Monte Carlo sampling provides a baseline estimate of the feasible treatment-effect distribution, while optimization-based approaches attempt to identify boundary solutions that may be rarely encountered through random sampling alone.

Current approaches include:

### Monte Carlo Sampling

Randomly generate feasible subgroup assignments satisfying published constraints and estimate the resulting treatment-effect distribution.

### Simulated Tempering

Perform constrained label swaps while preserving feasibility, searching for subgroup assignments that maximize or minimize treatment effects.

### Extremal Optimization

Use patient-level fitness heuristics to identify influential subgroup assignments and explore extreme regions of the feasible solution space.

### Constraint Verification

All candidate assignments are validated against published subgroup constraints to ensure feasibility.

---

## Repository Structure

```text
covar-recon-IPD/
├── notebooks/
│   ├── 01_maple_integration_test.ipynb
│   ├── 02_simple_extremal_search.ipynb
│   └── ...
│
├── resolve-ipd/
│   └── maple/
│       ├── main.R
│       ├── sa.R
│       ├── target.R
│       ├── simdata.R
│       ├── loss.R
│       └── ...
│
├── results/
│   ├── figures/
│   ├── tables/
│   └── maple_outputs/
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── reconstructed/
│
├── docs/
│   ├── CHANGELOG.md
│   ├── R_git.md
│   └── Python_git.md
│
├── requirements.txt
├── LICENSE
└── README.md
```

## Future Directions

- Single-Covariate Reconstruction: Develop methods that efficiently characterize the full feasible treatment-effect space, with particular emphasis on identifying extremal treatment effects that satisfy published subgroup constraints.
- Agentic Reconstruction: Develop and benchmark AI agents that reconstruct subgroup assignments directly from published summaries and evaluate their ability to recover feasible treatment-effect regions.
- Generative Reconstruction: Investigate diffusion models, copula-based methods, GANs, and other generative approaches for learning and sampling from the feasible assignment distribution.
- Joint Covariate Reconstruction: Extend the framework from a single binary subgroup to multiple correlated covariates while preserving published marginal and dependency constraints.