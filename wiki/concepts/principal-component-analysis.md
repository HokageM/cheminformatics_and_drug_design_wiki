---
title: "Principal component analysis (PCA)"
type: concept
tags: [qsar, statistics, dimensionality-reduction, pca]
created: 2026-09-30
updated: 2026-09-30
sources: ["[[sources/ciw-05-pharmacophores-qsar-and-docking]]"]
status: solid
---

# Principal component analysis (PCA)

A variable-reduction method: determine an orthogonal basis z₁, z₂, … oriented along the
**directions of greatest variance**, and keep only the first few.

## Why it matters

[[concepts/comfa]] produces tens of thousands of grid variables for a few dozen molecules.
Regression is impossible until the dimensionality is cut. PCA is the standard answer — and
the lecture immediately shows why it is the *wrong* answer here, motivating
[[concepts/partial-least-squares]].

## Goal and constraints

```text
GOAL: reduction of the dimensionality while RETAINING THE VARIANCE

CONSTRAINTS:
  - z_1..z_s are linear combinations of the data vectors x_i
  - z_i, z_i'  are orthogonal for i ≠ i'
  - the variance σ_i² is falling with i and each maximal
        equivalently:  minimise  || X − X' Z ||
```

## Computation

```text
ALGORITHM PCA
INPUT   data matrix D (rows = molecules, columns = variables), target dimension k
OUTPUT  basis vectors z_1..z_k

1. covariance matrix        C := Dᵀ D
2. determine eigenvalues / eigenvectors    λ_i z_i    with λ_0 > λ_1 > ...
3. the z_i are the corresponding basis vectors
4. TAKE THE FIRST k VECTORS
5. project the data:  D' := D · [z_1 ... z_k]
```

```mermaid
flowchart LR
    D["Data matrix D"] --> C["Covariance DᵀD"]
    C --> E["Eigen-decomposition"]
    E --> Z["z_1 ... z_n sorted<br/>by eigenvalue"]
    Z --> K["Keep first k"]
    K --> P["Projected data"]
```
*The first principal component is the direction in which the molecules differ the most — which is not necessarily the direction in which their activities differ.*

```text
        y ^            1. PC
          |          /
          |     ****/
          |   *****
          | ****
          +-----------------> x
   the cloud's long axis becomes z_1
```

## The decisive disadvantage

> The basis vectors are determined **without consideration of the bound (biological) data**:
> correlating data may not be found.

PCA is unsupervised. If the activity happens to vary along a low-variance direction — a
small but consistent electrostatic difference, say — PCA discards precisely that direction
first. This is the entire motivation for PLS.

## Caveats

- Sensitive to scaling: variables with large numeric range dominate the covariance matrix.
- The principal components are linear combinations of *all* original variables, so
  interpretability is lost.
- Choosing k is itself a model-selection problem.

## See also

- [[concepts/partial-least-squares]]
- [[concepts/comfa]]
- [[concepts/3d-qsar]]
- [[concepts/clustering-of-molecules]]

## Sources

- [[sources/ciw-05-pharmacophores-qsar-and-docking]] (p. 20)
