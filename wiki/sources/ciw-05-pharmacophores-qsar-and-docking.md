---
title: "CiW Lecture 5 — Pharmacophores, QSAR and Docking"
type: source
tags: [source, lecture, pharmacophore, qsar, docking, ciw-05]
created: 2026-09-30
updated: 2026-09-30
raw: raw/ciw_5.pdf
pages: 29
status: solid
---

# CiW Lecture 5 — Pharmacophores, QSAR and Docking

Scanned handwritten German summary, 29 pages. Covers the remainder of chapter 4
(working with pharmacophores), all of chapter 5 (QSAR), the beginning of chapter 6
(docking), and exercise sheet 6.

## Page map

| Pages | Content |
|---|---|
| 1–2 | Working with pharmacophores: screening workflow, active-analog approach, orientation maps |
| 3 | DISCO: distance-compatibility graph + clique search |
| 4 | Pharmacophore matching = 3D database searching; CATALYST |
| 5 | CAVEAT: vector-pair database and bins |
| 6 | UNITY: directed tweak |
| 7 | LigandScout (bipartite matching), Pharmer (KDB-tree triangle index) |
| 8 | QSAR chapter opener: matched molecular pairs, MMPA, MMS |
| 9–10 | MMPA workflow and the four MMP identification algorithms |
| 11–12 | **Exercise 6-2** — MMPs, Hussain & Rea, core vs context |
| 13–14 | **Exercise 6-1** — QSAR regression matrix, correlation coefficient, LOO q² |
| 15 | QSAR definition; physico-chemical parameters (σ, π/logP, MR, MW, Verloop) |
| 16 | logP determination; Hansch analysis |
| 17 | Free–Wilson analysis |
| 18 | Combined approach; 3D-QSAR problem statement |
| 19 | CoMFA: prerequisites, method, GRID fields, correlation model |
| 20 | PCA |
| 21 | PLS |
| 22 | CoMSIA; application and visualisation of 3D-QSAR models |
| 23 | Evaluating QSAR models: train/test split, leave-n-out, RSS/MSE/RMSE |
| 24 | Pearson r, R², q²/Q², the two evaluation pitfalls |
| 25 | Docking: problem statement, taxonomy, scoring-function problem, ΔG = −RT ln Kᵢ |
| 26 | Scoring functions: force field, PMF, empirical (Böhm) |
| 27 | DOCK: sphere representation of the site, clique-based matching |
| 28 | Kuhl algorithm (docking graph, Bron–Kerbosch); CLIX |
| 29 | Geometric hashing (Fischer): hash table of atom triplets, voting scheme |

## Summary

Lecture 5 completes the ligand-based track and opens the structure-based one.

The first block finishes what lecture 4 started. Lecture 4 defined what a
[[concepts/pharmacophore]] *is*; lecture 5 shows how to **derive** one from a set of
actives when the protein structure is unavailable ([[concepts/pharmacophore-derivation]],
[[concepts/disco-algorithm]]) and how to **search a database** with it
([[concepts/pharmacophore-matching]] and the five named systems). The recurring technical
device is the distance-compatibility graph: potential point assignments become nodes,
compatible pairs become edges, and cliques are candidate pharmacophores — exactly the
construction that returns in [[concepts/kuhl-algorithm]] for docking.

The second block is [[concepts/qsar]]: correlate numerical descriptions of molecules with
measured activity. The lecture walks the historical ladder — Hansch (physico-chemical
parameters), Free–Wilson (substituent indicators), the combined model that contains both as
special cases, and finally 3D-QSAR (CoMFA/CoMSIA) where the descriptor is a field sampled
on a grid. Because the grid produces far more free variables than data points, the lecture
attaches two dimension-reduction methods, [[concepts/principal-component-analysis]] and
[[concepts/partial-least-squares]], and then a careful treatment of
[[concepts/qsar-model-validation]] — including two explicit warnings about how q² can lie.
[[concepts/matched-molecular-pairs]] is presented as the modern, non-regression alternative:
predict property *differences* instead of absolute values.

The third block starts [[concepts/docking]]. Given a protein structure, find the ligand
pose and the affinity. The lecture splits the problem into the search (DOCK, Kuhl, CLIX,
geometric hashing) and the [[concepts/scoring-functions]] that rank poses, recovering the
thermodynamics of lecture 1: ΔG = ΔH − TΔS, ΔG = −RT ln Kᵢ, and Böhm's empirical function
with terms for rotatable bonds, H-bonds, ionic interactions and lipophilic surface.

## Key concepts

| Concept | Page(s) | Page in wiki |
|---|---|---|
| Screening workflow, active-analog approach, orientation maps | 1–2 | [[concepts/pharmacophore-derivation]] |
| DISCO | 3 | [[concepts/disco-algorithm]] |
| 3D database searching | 4 | [[concepts/pharmacophore-matching]] |
| CATALYST | 4 | [[concepts/catalyst-algorithm]] |
| CAVEAT | 5 | [[concepts/caveat-algorithm]] |
| UNITY / directed tweak | 6 | [[concepts/directed-tweak]] |
| LigandScout | 7 | [[concepts/ligandscout-algorithm]] |
| Pharmer | 7 | [[concepts/pharmer-algorithm]] |
| MMP, MMS | 8 | [[concepts/matched-molecular-pairs]] |
| MMPA and its four algorithms | 9–10 | [[concepts/matched-molecular-pair-analysis]] |
| QSAR definition and goals | 15 | [[concepts/qsar]] |
| Hammett σ, π, MR, MW, Verloop | 15 | [[concepts/physicochemical-parameters]] |
| logP, octanol/water, π additivity | 16 | [[concepts/lipophilicity-and-logp]] |
| Hansch analysis | 16 | [[concepts/hansch-analysis]] |
| Free–Wilson analysis, combined approach | 17–18 | [[concepts/free-wilson-analysis]] |
| 3D-QSAR | 18 | [[concepts/3d-qsar]] |
| CoMFA | 19 | [[concepts/comfa]] |
| PCA | 20 | [[concepts/principal-component-analysis]] |
| PLS | 21 | [[concepts/partial-least-squares]] |
| CoMSIA | 22 | [[concepts/comsia]] |
| RSS/MSE/RMSE, r, R², q², Q² | 23–24 | [[concepts/qsar-model-validation]] |
| Docking problem and taxonomy | 25 | [[concepts/docking]] |
| Force field, PMF, empirical/Böhm | 25–26 | [[concepts/scoring-functions]] |
| DOCK | 27 | [[concepts/dock-algorithm]] |
| Kuhl, CLIX | 28 | [[concepts/kuhl-algorithm]], [[concepts/clix-algorithm]] |
| Fischer geometric hashing | 29 | [[concepts/geometric-hashing-docking]] |

## Formulas and algorithms

- π(X) = logP(R–X) − logP(R–H)  — additive lipophilicity contribution (p. 16)
- Hansch: log 1/C = k₁(logP)² + k₂ logP + k₃σ + … + k (p. 16)
- Free–Wilson: log 1/c = Σᵢ Σⱼ a_ij δ_ij + μ, δ_ij = 1 if sᵢⱼ sits at Xᵢ (p. 17)
- Combined: log 1/c = Σᵢ Σⱼ s_ij Σₖ a_ijk Φ_ijk + μ (p. 18)
- CoMFA: log 1/C = Σ_f Σ_{x,y,z} a_{f,x,y,z} · f(x,y,z) + a (p. 19)
- RSS = Σ(yᵢ − pᵢ)², MSE = RSS/n, RMSE = √MSE (p. 23)
- r = Σ(pᵢ−p̄)(yᵢ−ȳ) / [√Σ(pᵢ−p̄)² · √Σ(yᵢ−ȳ)²],  r ∈ [−1,1] (p. 24)
- R² = 1 − Σ(pᵢ−yᵢ)² / Σ(yᵢ−ȳ)²,  R² ∈ (−∞, 1] (p. 24)
- ΔG = −RT ln Kᵢ, ΔG = ΔH − TΔS, Kᵢ = [P][L]/[PL] (p. 25)
- PMF: E(R,L) = Σ_{r∈R, l∈L} g_{a(r)a(l)}(d(r,l)) (p. 26)
- Böhm: ΔG = ΔG₀ + ΔG_rot·N_rot + ΔG_hb Σ f(ΔR)f(Δα) + ΔG_io Σ f(ΔR)f(Δα) + ΔG_lipo·|A_lipo| (p. 26)
- Distance compatibility: |d(l₁,l₂) − d(k₁,k₂)| < ε (pp. 3, 27)
- Docking clique set: C = {(s,m) ∈ S×M | s = R·m + t}, maximise |C| (p. 28)

## Exam-relevant points

- The **distance-compatibility graph + clique search** pattern appears three times
  (DISCO, DOCK, Kuhl). Be able to construct it and say why cliques are the right object.
- Free–Wilson and Hansch are **special cases of one combined model** (k=1, Φ=1 gives
  Free–Wilson; i=j=1 gives Hansch).
- CoMFA fields diverge near atoms → capping; **CoMSIA fixes this** with Gaussian similarity
  indices that have a finite maximum.
- PCA maximises variance *without looking at the activity*; PLS maximises **correlation with
  the activity**. That one difference is the whole reason PLS is preferred in 3D-QSAR.
- r²/R² measure fit to the **training** set; q²/Q² measure fit under **cross-validation**.
  A low RSS says nothing about prediction for unknown molecules.
- Böhm's function term-by-term, and which physical effect from lecture 1 each term encodes.
- Scoring-function taxonomy: force field (enthalpy only) / PMF (knowledge-based, inverse
  Boltzmann) / empirical (regression against measured ΔG).

## Open questions

- p. 5: CAVEAT's bin size for the torsion angle t "depends on a₂" — the functional form is
  not given.
- p. 7: Pharmer's per-triangle metadata lists a Bloom filter but not what it filters.
- p. 19: the marginal note distinguishes "relevance/explanation" from "contribution" for
  a_{f,x,y,z}; the argument is compressed and worth reconstructing.
- p. 28: "clique search is NP-hard but in general this does not hold for the docking
  problem" — the reason (bounded degree / geometric structure) is asserted, not argued.

## Pages touched by this ingest

Created: this page, 25 concept pages, 1 exercise page.
Updated: `index.md`, `log.md`, `synthesis.md`, `open-questions.md`.
