---
title: "CiW 03 — Frequent Pattern Mining, Structure Diagrams, Molecular Surfaces, Reduced Graphs"
type: source
tags: [source, lecture, ciw-03]
created: 2026-09-30
updated: 2026-09-30
raw: raw/ciw_3.pdf
pages: 27
status: ingested
---

# CiW 03 — Frequent Pattern Mining, Structure Diagrams, Molecular Surfaces, Reduced Graphs

Scanned handwritten German summary, 27 pages. Covers the remainder of chapter 2
(sections 2.3, 2.4, 2.5) and the beginning of chapter 3 (reduced graph descriptors),
interleaved with exercise sheets **Ex 4** and **Ex 5**.

## Page map

| Pages | Content |
|---|---|
| 1–5 | §2.3 Search for frequent patterns (frequent pattern mining, MoSS) |
| 6–7 | Exercise 4, tasks 4-1 (search-tree trace) and 4-2 (KNIME MoSS) |
| 8–13 | §2.4 Generation of structure diagrams (SDG, ring layout, collision handling, interaction diagrams) |
| 14–18 | §2.5 Computation of molecular surfaces (VdW, Connolly, marching cubes, Kohonen maps) |
| 19 | Exercise 4, task 4-3 (ball-pivoting algorithm) |
| 20–26 | §3.1 Reduced graphs and feature trees |
| 27 | Exercise 5, task 5-1 (feature trees) |

## Summary

The lecture completes the "molecule as a graph" thread of lecture 2 and then leaves it in
two directions.

**Frequent pattern mining** (pp. 1–5) asks which substructures occur in at least `p %` of a
molecule set `A` — and, in the *contrast* variant, in at most `n %` of a second set `B`.
The search tree enumerates substructures by adding one bond per level; because runtime is
linear in the number of visited nodes, everything depends on pruning. Four pruning rules
are given, plus a canonical-extension scheme that avoids duplicate substructures outright.
See [[concepts/frequent-pattern-mining]] and [[concepts/moss-algorithm]].

**Structure diagram generation** (pp. 8–13) is the inverse problem: given a molecular graph,
find a 2D layout obeying chemical drawing conventions. SDG is NP-hard. The basic algorithm
places atoms iteratively from a drawing queue, prioritised by the Shelley score; ring
systems are laid out separately by an analytical decomposition method with a ring-template
database fallback; collisions are found with a scan-line algorithm and repaired by local
layout modifications. The same machinery, extended by a convex-hull placement of amino
acids, produces 2D protein–ligand interaction diagrams. See
[[concepts/structure-diagram-generation]], [[concepts/ring-system-layout]],
[[concepts/collision-detection-scan-line]], [[concepts/protein-ligand-interaction-diagrams]].

**Molecular surfaces** (pp. 14–18) moves from topology to geometry. The van der Waals
interaction, modelled by the Lennard-Jones potential, defines an atomic radius; from it
three nested surface definitions follow (VdW, solvent-accessible, molecular/Connolly).
Connolly's algorithm computes the molecular surface by a gift-wrapping traversal of the
torus-path network; marching cubes approximates surfaces from grid data; Kohonen maps
project a 3D surface into 2D for molecule comparison. See [[concepts/molecular-surfaces]],
[[concepts/lennard-jones-potential]], [[concepts/connolly-surface-algorithm]],
[[concepts/marching-cubes]], [[concepts/kohonen-maps]],
[[concepts/ball-pivoting-algorithm]].

**Reduced graphs** (pp. 20–26) start chapter 3. A molecular graph is precise but hard to
compare; collapsing rings, linkers and features into single labelled nodes yields a much
smaller graph that can be compared efficiently, at the price of abstraction. Feature trees
push this further: they drop 3D information entirely, represent the molecule as a
node-labelled *tree*, and compare two molecules by a topology-preserving matching computed
with split-search and match-search. See [[concepts/reduced-graphs]],
[[concepts/feature-trees]], [[concepts/feature-tree-comparison]].

## Key concepts

| Concept | Page(s) |
|---|---|
| Frequent pattern mining, support, closed fragment, contrast pattern mining | 1 |
| Search tree construction, embeddings, equivalence classes | 1–2 |
| Positive-support-based, size-based, smallest-fulfilling, structural pruning | 2–3 |
| Duplicate avoidance via atom ordering and bond ordering | 3 |
| Perfect-extension pruning, equivalent-sibling pruning, initial embeddings | 4 |
| Contrast patterns, ring matching, variable chain length | 5 |
| SDG problem statement, IUPAC drawing rules, basic iterative algorithm | 8 |
| Shelley priority score, drawing units (CDU/RDU), hard cases, prefabricated units | 9 |
| Ring-system layout, analytical decomposition, ring database, force-field fallback | 10 |
| Collision detection, scan-line principle, layout modifications | 11 |
| Optimal ligand layout, convex-hull amino-acid placement, collision handling | 12 |
| Hydrophobic contacts as cubic splines | 13 |
| Van der Waals interaction, Lennard-Jones potential, united-atom radii | 14 |
| VdW / solvent-accessible / molecular surface; convex, saddle, concave patches | 15 |
| Connolly algorithm, gift-wrapping over torus paths | 16 |
| Marching cubes, 15 base patterns | 17 |
| Kohonen maps (Gasteiger, Zupan) | 18 |
| Reduced graphs, node types Ar/R/L/F, Gillet hierarchy, Daylight fingerprints | 20–21 |
| Feature trees (Rarey): definition, generation, node labels, compare function | 22–23 |
| Topology-preserving matching, split-search, match-search, dynamic programming | 24–26 |

## Formulas & algorithms

```text
sup_A(S)          = percentage of molecules in A that contain substructure S
S closed          ⟺ ∄ S' ⊋ S with sup_A(S') = sup_A(S)
contrast pattern  : sup_A(S) ≥ p  ∧  sup_B(S) ≤ n

Shelley score     s_{a,0} = 1 + 2δ          (δ = 1 if a cyclic, 0 if acyclic)
                  s_{a,n} = 3·s_{a,n-1} + Σ_j s_{j,n-1}   (j adjacent to a); stop at n = 5

Lennard-Jones     V_ij(r) = A_ij / r^12 − B_ij / r^6

regular polygon   interior angle Φ = 180° − 360°/R   for ring size R ≤ 8

Feature tree
  compare         f(A,B) = Σ_i min(a_i, b_i) / Σ_i (a_i + b_i)/2
  match score     sim(m) = s·f_steric(a,b) + (1−s)·f_chemistry(a,b)
  tree similarity S_M(A,B) = Σ_{m∈M} size(m)·sim(m) / (size(A) + size(B))
  split score     score(S) = α·(bal(a₁,a₂) + bal(b₁,b₂))/2
                           + (1−α)·(sim(a₁,b₁) + sim(a₂,b₂))
  match score     score(m) = α·sim(a₁,a₂) + (1−α)·sim(ν₁,ν₂)
```

## Exam-relevant points

- Support falls monotonically down the search tree — this is what makes positive-support
  pruning sound. **Negative support does not fall monotonically**, so it can never be used
  for pruning, only for filtering.
- Closedness cannot be used for pruning under smallest-fulfilling-pattern search.
- Structural pruning is an **approximation**: duplicates can still occur.
- SDG is NP-hard; so is optimal ligand layout.
- Three surface definitions and how they nest: VdW ⊂ molecular ⊂ solvent-accessible
  (in terms of enclosed volume).
- The molecular surface is continuous and differentiable but can self-intersect ⇒ cusp
  trimming.
- Reduced graphs and feature trees trade precision for comparability; feature-tree
  comparison does **not** presuppose an exact subgraph match.

## Open questions

- Page 1 lists the data structure for embeddings but not the concrete duplicate-free
  enumeration order used by MoSS in the exercise; the exercise trace on p. 6 implies the
  bond order single < aromatic < double < triple.
- Exercise 5 on p. 27 shows only task 5-1; further tasks presumably belong to lecture 4.
- The Kohonen-map page is terse — the objective function of the learning phase is given
  only as "over the input vector".

## Pages touched

`sources/ciw-03-…` (this page) · `concepts/frequent-pattern-mining` ·
`concepts/moss-algorithm` · `concepts/structure-diagram-generation` ·
`concepts/ring-system-layout` · `concepts/collision-detection-scan-line` ·
`concepts/protein-ligand-interaction-diagrams` · `concepts/molecular-surfaces` ·
`concepts/lennard-jones-potential` · `concepts/connolly-surface-algorithm` ·
`concepts/marching-cubes` · `concepts/kohonen-maps` ·
`concepts/ball-pivoting-algorithm` · `concepts/reduced-graphs` ·
`concepts/feature-trees` · `concepts/feature-tree-comparison` ·
`exercises/ciw-e4-moss-and-surfaces` · `exercises/ciw-e5-feature-trees` ·
`index` · `log` · `synthesis` · `open-questions`
