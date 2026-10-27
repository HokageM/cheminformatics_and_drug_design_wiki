---
title: GCI Exercise 3 - Stereochemistry, Rings, Subgraph Search and MCS
type: exercise
tags: [gci, stereochemistry, rings, subgraph-isomorphism, mcs]
created: 2026-10-19
updated: 2026-10-19
sources: ["[[sources/gci-03-stereochemistry-rings-substructure-and-mcs]]"]
status: developing
---

# GCI Exercise 3 - Stereochemistry, Rings, Subgraph Search and MCS

This exercise page records the hand-worked traces embedded in GCI part 3: CIP ordering, ring/bond classification, Ullmann refinement and Bron-Kerbosch clique enumeration.

## Tasks and approach

| Topic | Task in the notes | Approach captured here |
|---|---|---|
| CIP | rank substituents around stereocentres and assign R/S or E/Z | build substituent trees; compare shells using [[concepts/cip-sequence-rules]] |
| rings | find smallest rings and cyclic/acyclic bonds | BFS for smallest local ring; low-link DFS for bridges |
| Ullmann | trace candidate matrices for a query in a target graph | initialise by label/degree, then refine neighbourhood compatibility |
| MCS | transform MCS into clique search and run Bron-Kerbosch | build [[concepts/modular-product-graph]], enumerate cliques with [[concepts/bron-kerbosch-algorithm]] |

## Pseudocode summary

```text
PROCEDURE SolveCIPExercise(molecule M, stereocentre c)
  INPUT : drawn molecule with a marked stereocentre
  OUTPUT: ordered substituents and stereo label

  roots <- atoms directly attached to c
  for each root: draw substituent tree outward from c
  duplicate atoms for multiple bonds and ring closures
  compare roots shell by shell until all priorities are assigned
  orient lowest-priority substituent away from the viewer
  read 1 -> 2 -> 3 as clockwise or counter-clockwise to assign R/S
```

```text
PROCEDURE TraceUllmannExercise(query F, target G)
  INPUT : query and target graphs from the sheet
  OUTPUT: accepted embeddings and number of recursive steps

  M <- initial matrix from atom labels and degrees
  for each query row in search order:
      choose a still-unused target column with M[row,column] = 1
      zero the remaining row entries
      refine: delete candidates whose query neighbours lack target-neighbour support
      if a row becomes empty: backtrack
      else continue recursively
```

```text
PROCEDURE TraceBronKerboschExercise(productGraph P)
  INPUT : compatibility graph from the sheet
  OUTPUT: maximal cliques listed once

  I <- empty current clique
  X <- all vertices
  N <- empty processed set
  BronKerbosch(P, I, X, N)
  record each output clique and its size
```

```mermaid
flowchart LR
    CIP["CIP trees"] --> Ring["ring and bridge labels"]
    Ring --> U["Ullmann matrices"]
    U --> P["product graph"]
    P --> BK["Bron-Kerbosch trace"]
```
*The exercise moves from local stereochemical ordering to global graph search.*

## Solution sketch

- CIP examples show that direct atom priority is often insufficient; the decisive difference can occur several shells away after multiple-bond duplication or ring opening.
- The ring examples contrast a local BFS smallest-ring calculation with a global DFS low-link pass that labels all acyclic bonds.
- In the Ullmann trace, refinement reduces the recursion count substantially: the notes contrast a 36-branch unrefined product of row candidate counts with a smaller refined trace of 13 steps.
- The Bron-Kerbosch trace lists four maximal cliques in the drawn compatibility graph, with the largest clique containing five vertices.

## What it teaches

- Stereochemical labels, ring membership and substructure hits are not visual annotations; they are outputs of explicit graph procedures.
- Matrix refinement and clique search are dual-looking pruning strategies: Ullmann deletes impossible assignments, while Bron-Kerbosch grows only mutually compatible assignments.
- The same clique machinery later reappears in MCS and structure-based methods.

## See also

- [[concepts/cip-sequence-rules]]
- [[concepts/smallest-ring-search]]
- [[concepts/ullmann-algorithm]]
- [[concepts/maximum-common-substructure]]
- [[concepts/bron-kerbosch-algorithm]]

## Sources

- [[sources/gci-03-stereochemistry-rings-substructure-and-mcs]] (pp. 3, 5-8, 16, 23, 25, 33-34)
