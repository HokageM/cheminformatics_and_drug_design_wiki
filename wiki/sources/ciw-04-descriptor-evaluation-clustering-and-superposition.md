---
title: "CiW 04 — Descriptor Evaluation, 3D Descriptors, Clustering, Molecular Superposition"
type: source
tags: [source, lecture, ciw-04]
created: 2026-09-30
updated: 2026-09-30
raw: raw/ciw_4.pdf
pages: 27
status: ingested
---

# CiW 04 — Descriptor Evaluation, 3D Descriptors, Clustering, Molecular Superposition

Scanned handwritten German summary, 27 pages. Completes chapter 3 (sections 3.2–3.5) and
covers the whole of chapter 4 (structural superposition of molecules), with exercise **Ex 5
task 5-2** in between.

## Page map

| Pages | Content |
|---|---|
| 1 | §3.2 Comparing similarity measures: enrichment factors, %MAEF |
| 2 | Comparing models: ROC curves, confusion matrix, AUC |
| 3 | §3.3 3D descriptors: pharmacophores, pharmacophore points, PPPs |
| 4 | Geometric atom-pair descriptors |
| 5 | Atom-triplet descriptors; the conformation problem |
| 6 | USR (Ultrafast Shape Recognition); shape signatures |
| 7 | §3.4 Further descriptors: autocorrelation vectors, affinity fingerprints, SEA |
| 8 | §3.5 Clustering of molecules: taxonomy of algorithms |
| 9 | Hierarchical agglomerative clustering; the four classical linkages |
| 10 | Ward's method, Lance–Williams recursion, Jarvis–Patrick clustering |
| 11 | k-means clustering |
| 12 | Exercise 5, task 5-2 (partitional vs hierarchical clustering) |
| 13 | **Chapter 4** Structural superposition: the overlay problem |
| 14 | Modelling by Gaussian functions; Carbó and Hodgkin similarity indices |
| 15 | SEAL — rigid superposition |
| 16 | §4.2 Spatial structure: constitution, configuration, conformation, geometric parameters |
| 17 | VSEPR model |
| 18 | Deviations from ideal geometry; bond lengths and angles; LCP model |
| 19 | Further geometry parameters: planarity at double bonds and amides; conclusion |
| 20 | §4.2.1 Conformation generation: goals, conceptual problems, data-driven methods |
| 21 | CORINA; torsion-angle libraries; conformational ensembles |
| 22 | §4.3 Flexible superposition: genetic algorithms, GASP |
| 23 | GASP genetic operators; FlexS interaction model |
| 24 | FlexS scoring and incremental construction |
| 25 | §4.4 Superposition of point sets: RMSD, optimising the translation |
| 26 | Optimising the rotation — Sippl's iterative method |
| 27 | Optimising the rotation — Kabsch's method |

## Summary

**How do you know a descriptor is any good?** (pp. 1–2) Two answers. The *enrichment factor*
measures how much of a known active class a similarity ranking pulls into the top `p %` of
the data; *ROC curves* plot sensitivity against 1 − specificity as a classification
threshold sweeps, and summarise the result as an AUC. See
[[concepts/enrichment-factor]] and [[concepts/roc-curves-and-auc]].

**3D descriptors** (pp. 3–6) start from the observation that what matters for binding is the
spatial arrangement of functional groups, not the scaffold carrying them — the
*pharmacophore*. Because conformations are unknown, practical 3D descriptors bin
interatomic distances between typed atoms (atom-pair and atom-triplet descriptors) or
summarise the molecular shape by distance distributions to four reference points (USR).
The lecture's blunt verdict: **3D descriptors often perform worse than topological ones**.
See [[concepts/pharmacophore]], [[concepts/atom-pair-and-triplet-descriptors]],
[[concepts/ultrafast-shape-recognition]].

**Further descriptors** (p. 7) encode neighbourhood statistics
([[concepts/autocorrelation-vectors]]) or replace structure by measured behaviour
([[concepts/affinity-fingerprints]]).

**Clustering** (pp. 8–12) groups molecules by a similarity measure without labels. The
lecture covers hierarchical agglomerative clustering with four linkage definitions plus
Ward's method and the Lance–Williams recursion that unifies them, the neighbour-list-based
Jarvis–Patrick method, and k-means. See [[concepts/clustering-of-molecules]],
[[concepts/hierarchical-clustering]], [[concepts/jarvis-patrick-clustering]],
[[concepts/k-means-clustering]].

**Chapter 4: superposition** (pp. 13–27) asks for the relative orientation of several
ligands binding the same, unknown protein. Molecules are modelled as sums of Gaussians so
that overlap becomes an integral; SEAL optimises translation and rotation of rigid
molecules against a normalised overlap index. Making the molecules flexible requires
conformations, hence a digression into spatial structure ([[concepts/molecular-conformation]],
[[concepts/vsepr-model]], [[concepts/conformation-generation]]) before the flexible
algorithms GASP and FlexS ([[concepts/flexible-superposition]]). The chapter closes with
the exactly solvable sub-problem: superposing two *point sets* by minimising the RMSD
([[concepts/rmsd-and-point-set-superposition]]).

## Formulas & algorithms

```text
Enrichment
  E(m,p)   = % molecules of m's class in the first p% of data
           / % molecules of m's class in the data
  E(A,p)   = (1/|A|) Σ_{m∈A} E(m,p)
  %MAEF    = % of the maximal achievable enrichment factor

Classification
  TPR = TP/P = TP/(TP+FN)        TNR = TN/N = TN/(TN+FP)
  FPR = FP/N = FP/(FP+TN)        Acc = (TP+TN)/(P+N)
  AUC ∈ [0,1];  random process = 0.5

Atom-pair similarity
  sim(A,B) = Σ_{k∈bins} min(f_A[k], f_B[k]) / ( ½ Σ_{k∈bins} (f_A[k] + f_B[k]) )

USR
  m_k(f_p)  = ∫ x^k f_p(x) dx        (first three moments of each of four distributions)
  S(M_A, M_B) → [0,1]

Autocorrelation
  A(d) = Σ_{ij} d_ij p_i p_j     d_ij = 1 if the bond distance between i and j is d
  autocorrelation vector = (A(1), A(2), …, A(n))

Clustering
  single linkage    f'(A,B) = min_{a∈A, b∈B} f(a,b)
  complete linkage  f'(A,B) = max_{a∈A, b∈B} f(a,b)
  group average     f'(A,B) = (1/(|A||B|)) Σ_{a∈A, b∈B} f(a,b)
  centroid          f'(A,B) = f(c(A), c(B)),  c(A) = (1/|A|) Σ_{a∈A} a
  Ward              ESS(C)  = Σ_{a∈M} (a − c(C_a))²
                    f'(A,B) = ESS((C \ {A,B}) ∪ {A∪B})
  Lance–Williams    f'(C, A∪B) = α_A f'(C,A) + α_B f'(C,B) + β f'(A,B)
                                 + γ |f'(C,A) − f'(C,B)|
                    α_A = α_B = ½, β = 0, γ = −½  →  nearest neighbour
                    α_A = α_B = ½, β = 0, γ = +½  →  furthest neighbour
  k-means           c_i = (1/|S_i|) Σ_{x_j ∈ S_i} x_j

Gaussian molecule model
  f(x)       = a·e^{−b(x−x₀)²}
  ρ(x)       = Σ_{atoms i} a_i e^{−b|x−x_i|²}
  Z_AB       = ∫ ρ_A(x) ρ_B(x) dx
  Z_AB(t,R)  = ∫ ρ_A(x) ρ_B(Rx − t) dx
  Carbó      C_AB(t,R) = Z_AB(t,R) / sqrt(Z_AA · Z_BB)
  Hodgkin    H_AB(t,R) = 2 Z_AB(t,R) / (Z_AA + Z_BB)
  after integration
             Z_AB(t,R) = sqrt(π/2b) Σ_{ij} a_i a_j e^{−(b/2)|x_i − y_j|²}
  multi-property   w_ij = Σ_{properties p} k_p a_ip a_jp

Flexible superposition
  GASP   S = k₁ E_conf + k₂ E_vol + k₃ E_match
  FlexS  S = k₁ E_match + k₂ E_vol + k₃ E_gauss

Point-set superposition
  RMSD_{X,Y}(R,t) = sqrt( (1/n) Σ_{i=1..n} (x_i − R y_i − t)² )
  optimal translation  t = c(X) − c(Y')      (shift both centroids to the origin)
  Sippl   U = XᵀY,  γ_min = arctan[ (u₂₁ − u₁₂) / (u₁₁ − u₂₂) ];  iterate over x, y, z
  Kabsch  UᵀU = E;  Lagrange minimisation gives U(S+L) = R,
          RᵀR = (S+L)ᵀ(S+L);  eigenvectors a₁,a₂,a₃ and eigenvalues μ₁≥μ₂≥μ₃ of RᵀR
          U = R[S+L]⁻¹ = R A Λ⁻¹ Aᵀ,  Λ = diag(√μ₁, √μ₂, √μ₃),  A = (a₁,a₂,a₃)
```

## Exam-relevant points

- The enrichment factor is a *ratio of percentages*, so a value of 1 means "no better than
  random"; the AUC of a random classifier is 0.5.
- **3D descriptors often perform worse than topological ones** — because conformations are
  unknown (noise) and because the training data are biased towards topologically similar
  molecules.
- Centroid clustering requires objects that can be *geometrically interpreted*; the other
  three linkages only need a distance matrix.
- Lance–Williams unifies the linkages; changing γ from −½ to +½ turns nearest neighbour into
  furthest neighbour.
- The Jarvis–Patrick criterion is applied **transitively**.
- The superposition problem is NP-hard in general; SEAL simplifies it by assuming
  conformations are given and constant.
- Quaternions are used for the rotation because they have **no singularities** (unlike Euler
  angles).
- In point-set superposition, rotation and translation **decouple**: shift both centroids to
  the origin first, then solve for the rotation alone.

## Open questions

- Page 1: `%MAEF` is glossed only as "f-tree averaging" — the exact normalisation is not
  written out.
- Page 7 lists the SEA approach with a single line; the statistical model behind it is not
  described.
- Page 26 (Sippl) gives the derivative for the z-axis only and states that the optimisation
  cycle is independent of `U`; the convergence argument is not spelled out.

## Pages touched

`sources/ciw-04-…` (this page) · `concepts/enrichment-factor` ·
`concepts/roc-curves-and-auc` · `concepts/pharmacophore` ·
`concepts/atom-pair-and-triplet-descriptors` · `concepts/ultrafast-shape-recognition` ·
`concepts/autocorrelation-vectors` · `concepts/affinity-fingerprints` ·
`concepts/clustering-of-molecules` · `concepts/hierarchical-clustering` ·
`concepts/jarvis-patrick-clustering` · `concepts/k-means-clustering` ·
`concepts/molecular-superposition` · `concepts/gaussian-molecular-representation` ·
`concepts/seal-algorithm` · `concepts/molecular-conformation` · `concepts/vsepr-model` ·
`concepts/conformation-generation` · `concepts/flexible-superposition` ·
`concepts/rmsd-and-point-set-superposition` · `exercises/ciw-e5-feature-trees` ·
`index` · `log` · `synthesis` · `open-questions`
