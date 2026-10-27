---
title: "CiW Lecture 6 — Flexible Docking, Binding Sites, Fragment Spaces and Protein–Protein Docking"
type: source
tags: [source, lecture, docking, binding-site, druggability, fragment-space, ciw-06]
created: 2026-09-30
updated: 2026-09-30
raw: raw/ciw_6.pdf
pages: 28
status: solid
---

# CiW Lecture 6 — Flexible Docking, Binding Sites, Fragment Spaces and Protein–Protein Docking

Scanned handwritten German summary, 28 pages. Completes chapter 6 (docking), then covers
binding-site detection and druggability, combinatorial and fragment-based design, de novo
design with fragment spaces, and finally protein–protein docking. No exercise sheet in this
scan.

## Page map

| Pages | Content |
|---|---|
| 1–2 | Pose clustering (FlexX/Rarey): interaction-surface representation, hash table, clustering of orientations |
| 3 | Hierarchical filtering: GLIDE |
| 4 | Flexible docking taxonomy; genetic algorithms (GOLD, DOCK+GA, evolutionary programming, PLP) |
| 5 | Randomised methods: PRO_LEADS (tabu search), AutoDock (simulated annealing), MCM, MD |
| 6 | Place & join: DesJarlais, hinge bending |
| 7 | Incremental construction: algorithm and search strategies |
| 8 | Automated determination of active sites: definitions, problem, method families |
| 9 | Grid-based POCKET/LIGSITE; sphere-based SURFNET |
| 10 | Voronoi/alpha shapes (CAST); geometric construction (PASS) |
| 11 | Energy-based DrugSite |
| 12 | Evolutionary-based (Aloy); problems of all prediction families |
| 13 | Evaluating binding-site prediction: five criteria |
| 14 | Druggability and function prediction |
| 15 | Druggability approaches: Cheng (energy-based, MAPpod), Hajduk (NMR fragment screening) |
| 16 | Nayal & Honig (SCREEN, random forest); properties of drug-binding pockets |
| 17 | HTS, combinatorial libraries, SELECT |
| 18 | Focused combinatorial libraries; fragment-based drug design; SAR by NMR |
| 19 | De novo design: taxonomy, LUDI, MCSS |
| 20 | Chemical space; Lipinski rule of 5; Bohacek 10⁶⁰; GDB-17 |
| 21 | Combinatorial chemical spaces; fragment spaces; RECAP |
| 22 | Shredding, link atoms and link types; BRICS; working with fragment spaces |
| 23 | Search technologies: TOPAS, FTrees-FS, FlexNovo |
| 24 | Protein–protein docking: significance, task, differences, pipeline |
| 25 | Classes of PP docking algorithms; Katchalski-Katzir grid representation |
| 26 | Katchalski-Katzir: convolution, DFT, runtime |
| 27 | Alternative surface reductions; PatchDock, FlexDock, FireDock |
| 28 | MC simulation: RosettaDock, ICM-DISCO; CAPRI evaluation |

## Summary

Lecture 6 completes the arc of the course by relaxing, one at a time, every simplification
the earlier lectures made.

**Ligand rigidity goes first.** [[concepts/flexible-docking]] classifies the escape routes:
enumerate conformers, randomise (tabu search, simulated annealing, Monte Carlo, MD), or
construct combinatorially. The combinatorial branch splits into
[[concepts/place-and-join]] and [[concepts/incremental-construction-docking]], the latter
being FlexX's approach and the direct descendant of the incremental construction already
met in FlexS ([[concepts/flexible-superposition]]). The number of surviving poses explodes,
so [[concepts/pose-clustering]] and [[concepts/glide-hierarchical-filtering]] appear purely
as population-control devices.

**The assumption that we know where the ligand binds goes second.** Half the lecture is
[[concepts/binding-site-detection]]: find the pocket from the protein structure alone, by
geometry ([[concepts/ligsite-and-pocket]], [[concepts/surfnet]],
[[concepts/cast-alpha-shapes]], [[concepts/pass-algorithm]]), by energy
([[concepts/drugsite]]) or by evolution ([[concepts/evolutionary-site-prediction]]). Each
family has a characteristic failure mode, and the lecture insists on
[[concepts/binding-site-prediction-evaluation]] before believing any of them. Once a pocket
is found, its descriptors support [[concepts/druggability]] — the probability that a
disease-relevant protein can be modulated by a small molecule at all.

**The assumption that the ligand already exists goes third.** [[concepts/combinatorial-libraries]]
and [[concepts/fragment-based-drug-design]] are two answers to poor HTS hit rates, and
[[concepts/de-novo-design]] is the third. Making de novo design tractable requires
restricting the search space, which produces the elegant construction of this lecture:
[[concepts/chemical-space]] is far too large (10⁶⁰), so a
[[concepts/fragment-spaces|fragment space]] defines a combinatorially large set implicitly,
through fragments plus connection rules, and [[concepts/fragment-space-search]] searches it
without enumerating it.

**Finally the assumption that one partner is small goes.**
[[concepts/protein-protein-docking]] is a symmetric problem with an unknown contact site
and a huge interface. The signature method, [[concepts/katchalski-katzir-algorithm]],
reduces the translation search to a convolution and evaluates it by FFT — the only place in
the course where a frequency-domain trick supplies the speed-up.

## Key concepts

| Concept | Page(s) | Page in wiki |
|---|---|---|
| Pose clustering | 1–2 | [[concepts/pose-clustering]] |
| GLIDE hierarchical filtering | 3 | [[concepts/glide-hierarchical-filtering]] |
| Flexible docking taxonomy | 4 | [[concepts/flexible-docking]] |
| GOLD, DOCK+GA, evolutionary programming | 4 | [[concepts/genetic-algorithm-docking]] |
| Tabu search, simulated annealing, MCM, MD | 5 | [[concepts/randomised-docking]] |
| DesJarlais, hinge bending | 6 | [[concepts/place-and-join]] |
| Incremental construction | 7 | [[concepts/incremental-construction-docking]] |
| Binding site vs active site; method families | 8, 12 | [[concepts/binding-site-detection]] |
| POCKET, LIGSITE | 9 | [[concepts/ligsite-and-pocket]] |
| SURFNET | 9 | [[concepts/surfnet]] |
| CAST / alpha shapes | 10 | [[concepts/cast-alpha-shapes]] |
| PASS | 10 | [[concepts/pass-algorithm]] |
| DrugSite | 11 | [[concepts/drugsite]] |
| Aloy, conserved residues | 12 | [[concepts/evolutionary-site-prediction]] |
| Five evaluation criteria | 13 | [[concepts/binding-site-prediction-evaluation]] |
| Druggability, MAPpod, SCREEN | 14–16 | [[concepts/druggability]] |
| HTS, CombiLibs, SELECT | 17 | [[concepts/combinatorial-libraries]] |
| Focused libraries, SAR by NMR | 18 | [[concepts/fragment-based-drug-design]] |
| LUDI, MCSS, taxonomy | 19 | [[concepts/de-novo-design]] |
| Lipinski, Bohacek, GDB-17 | 20 | [[concepts/chemical-space]] |
| RECAP, BRICS, shredding | 21–22 | [[concepts/fragment-spaces]] |
| TOPAS, FTrees-FS, FlexNovo | 23 | [[concepts/fragment-space-search]] |
| PP docking problem and pipeline | 24–25 | [[concepts/protein-protein-docking]] |
| Katchalski-Katzir, FFT | 25–26 | [[concepts/katchalski-katzir-algorithm]] |
| Sphere world, cylinder projection, PatchDock | 27 | [[concepts/surface-reduction-for-docking]] |
| RosettaDock, ICM-DISCO, CAPRI | 28 | [[concepts/monte-carlo-protein-docking]] |

## Formulas and algorithms

- Pose-clustering distance:
  `d_rms((R₁,t₁),(R₂,t₂)) = sqrt( (1/n) Σᵢ ((R₁xᵢ + t₁) − (R₂xᵢ + t₂))² )` (p. 2)
- Pose-clustering runtime: d_rms in O(1) after O(n) preprocessing; with m orientation pairs
  below d_max: scoring all pairs O(n²), sorting O(m log m), complete linkage O(m) (p. 2)
- Simulated-annealing acceptance: `P(ΔE) = exp(−ΔE / k_B T)` (p. 5)
- DrugSite vdW sum: `P_i = Σ_j ( A_j C / r_ij¹² − B_j C / r_ij⁶ )` (p. 11)
- DrugSite contour level: `CL = mean − threshold · std. deviation`; clusters > 100 Å³ (p. 11)
- MAPpod: `ΔG_MAPpod = ΔG_target desolvation + ΔG_ligand desolvation + ΔG_contact` (p. 15)
- Lipinski rule of 5: MW > 500 D, logP > 5, #H-donors > 5, #H-acceptors > 10 (p. 20)
- Chemical space size: Bohacek > 10⁶⁰ molecules; GDB-17: 1.66 × 10¹¹ molecules (p. 20)
- Katchalski-Katzir grid: `a_{l,m,n} = 1` on surface, `= p` inside, `= 0` outside;
  protein A: p ≪ 0, protein B: 0 < p < 1 (p. 25)
- Correlation: `C_{α,β,γ} = Σ_l Σ_m Σ_n a_{l,m,n} · b_{l+α, m+β, n+γ}`, naive O(n⁶) (p. 25)
- Convolution: `c(h) = Σ_n f(n) g(n+h)`, `c = f * g`; `DFT(f*g) = DFT(f) · DFT(g)`;
  DFT in O(n log n) ⇒ total `O(N_R · N³ log N)` (p. 26)

## Exam-relevant points

- The three ways to handle ligand flexibility (enumerate / randomise / construct
  combinatorially) and one representative algorithm of each.
- Incremental construction: backtracking DFS versus greedy, and the cost/risk trade-off.
- The five binding-site-detection families and the specific weakness of each: grid methods
  are sensitive to grid width and protein orientation; sphere methods struggle with wide
  pockets; Voronoi only finds pockets whose opening is narrower than every cross-section;
  energy methods depend on the force field; evolutionary methods need many homologues.
- The five evaluation criteria for a predicted binding site.
- Why a fragment space beats an enumerated database: the space is defined implicitly by
  fragments + connection rules and is combinatorially larger than anything enumerable.
- Katchalski-Katzir: how the grid encoding makes surface overlap reward and core overlap
  penalise, and how the FFT reduces O(n⁶) to O(N³ log N) per rotation.

## Open questions

- p. 1: the hash-table "chaining costs" remark and the note about storing point IDs is
  compressed to the point of being unclear.
- p. 11: DrugSite's `C` factor in the vdW sum is not defined, and the "threshold" in the
  contour-level formula is left unspecified.
- p. 15: MAPpod's third term is written "ΔG_contact"; whether this is contact surface or a
  contact-count term is not stated.
- p. 25: the sign conventions p ≪ 0 for protein A and 0 < p < 1 for protein B are asserted
  without deriving why this makes surface–surface contact optimal.

## Pages touched by this ingest

Created: this page, 26 concept pages.
Updated: `concepts/de-novo-design` (lecture-6 section), `index.md`, `log.md`,
`synthesis.md`, `open-questions.md`, `overview.md`.
