---
title: "GCI 03 - Stereochemistry, Rings, Substructure Search and MCS"
type: source
raw: raw/foundations_gci_part3.pdf
date_ingested: 2026-10-19
---

# GCI 03 - Stereochemistry, Rings, Substructure Search and MCS

Series: [[sources/gci-01-foundations-of-cheminformatics]] -> [[sources/gci-02-inchi-canonical-smiles-and-smarts]] -> [[sources/gci-03-stereochemistry-rings-substructure-and-mcs]] -> [[sources/gci-04-molecular-glues-descriptors-fingerprints-and-similarity]].

## Summary

- Part 3 continues GCI by moving from line notations and canonical identifiers into the graph algorithms needed for stereochemical labelling, ring/chain decomposition, substructure search and maximum common substructure search.
- The CIP sequence rules (Cahn-Ingold-Prelog rules; **CIP-Regeln**) rank substituents by atomic number, isotope mass, recursive comparison of adjacent atoms, multiple-bond duplication and ring-opening duplicate atoms.
- R/S stereochemistry is assigned after the four substituents of a tetrahedral centre are ordered; E/Z double-bond stereochemistry uses the higher-priority substituent on each side of a double bond.
- Substituent comparison can be implemented by building a substituent tree, sorting adjacency lists with a bond-comparison routine, caching repeated comparisons and precomputing atom invariants such as Morgan ranks.
- A smallest ring containing an atom or bond can be found with BFS: cross-edges/back-edges give candidate cycle lengths from stored depths.
- Connectivity in undirected molecular graphs is an equivalence relation; its equivalence classes are connected components, found by DFS in linear time.
- A bond is acyclic if removing it disconnects its endpoints; a naive per-bond DFS is correct but costs O(|E|·(|V|+|E|)), while Tarjan-style low-link DFS labels all acyclic and cyclic bonds in O(|V|+|E|).
- Articulation nodes and biconnected components separate chain bonds from ring systems: a BCC with one bond is a chain bond; multi-edge BCCs are cyclic regions.
- A rotatable bond is treated as a non-ring single bond whose endpoints are not terminal; ring bonds and terminal single bonds are excluded.
- Ullmann subgraph isomorphism represents assignments as a matrix whose rows are query nodes and columns are target nodes; backtracking fixes one row at a time while refinement deletes candidates whose neighbourhoods cannot be matched.
- The initial Ullmann matrix uses atom-label, hybridisation and degree constraints; the necessary refinement criterion requires every query neighbour to have at least one still-possible target neighbour.
- Maximum common substructure (MCS) asks for the largest common subgraph of two molecular graphs; variants differ by induced vs non-induced, connected vs disconnected, ring/chain restrictions and atom vs bond objective.
- MCES can be reduced to MCIS via line graphs, with Whitney's theorem explaining when line-graph isomorphism corresponds to edge isomorphism of the original graphs; rare ΔY exchanges are the exception.
- Modular/product compatibility graphs convert common-subgraph problems into clique problems: compatible atom matches become product-graph vertices and mutually compatible matches become c-/d-edges.
- Bron-Kerbosch enumerates maximal cliques using current clique `I`, extension candidates `X` and the forbidden/processed set `N`; branch-and-bound and c-connected variants make it usable for MCS.

## Key concepts introduced

- [[concepts/cip-sequence-rules]]
- [[concepts/connected-components]]
- [[concepts/smallest-ring-search]]
- [[concepts/rotatable-bonds]]
- [[concepts/maximum-common-substructure]]
- [[concepts/modular-product-graph]]
- [[concepts/bron-kerbosch-algorithm]]
- [[exercises/gci-e3-stereochemistry-rings-subgraph-and-mcs]]

## Formulas & algorithms

```text
ALGORITHM CIPRankSubstituents(molecule G, centre c)
  INPUT : molecular graph G and stereogenic centre or double-bond end c
  OUTPUT: substituents sorted from highest to lowest CIP priority

  for each directly attached substituent root r of c:
      T[r] <- BuildSubstituentTree(G, c, r)
      duplicate atoms reached through double or triple bonds according to bond order
      open rings by duplicate nodes; stop a ring path when an atom would be seen twice
  sort roots by CompareCIPSubstituentTrees(T[a], T[b])
  return sorted roots
```

```text
ALGORITHM CompareCIPSubstituentTrees(Ta, Tb)
  INPUT : two substituent trees rooted next to the same stereocentre
  OUTPUT: -1, 0, +1 priority comparison

  for level k from 0 outward:
      La <- atoms at level k of Ta, sorted by decreasing CIP atom priority
      Lb <- atoms at level k of Tb, sorted by decreasing CIP atom priority
      compare La and Lb lexicographically by atomic number, isotope mass and duplicate status
      if one list is higher: return that ordering
  return 0
```

```text
ALGORITHM SmallestRingBFS(G, start)
  INPUT : molecular graph G and start atom or edge endpoint
  OUTPUT: length of a smallest detected ring, or none

  for each v in V(G): queued[v] <- false; depth[v] <- undefined; parent[v] <- none
  enqueue start; queued[start] <- true; depth[start] <- 0
  smallest <- infinity
  while queue not empty:
      w <- dequeue
      for each ring-eligible neighbour u of w:
          if not queued[u]:
              parent[u] <- w; depth[u] <- depth[w] + 1; queued[u] <- true; enqueue u
          else if parent[w] != u:
              length <- depth[w] + depth[u] + 1
              smallest <- min(smallest, length)
  return smallest if finite else none
```

```text
ALGORITHM ConnectedComponents(G)
  INPUT : undirected molecular graph G = (V,E)
  OUTPUT: component number cc[v] for every atom v and component count

  for each v in V: cc[v] <- 0
  n_cc <- 0
  for each v in V:
      if cc[v] == 0:
          n_cc <- n_cc + 1
          DFSVisit(v, n_cc)
  return cc, n_cc

PROCEDURE DFSVisit(v, component)
  cc[v] <- component
  for each u in Adj[v]:
      if cc[u] == 0: DFSVisit(u, component)
  # complexity: O(|V| + |E|)
```

```text
ALGORITHM NaiveAcyclicBondTest(G, edge e = (a,b))
  INPUT : molecular graph G and bond e
  OUTPUT: cyclic if a and b remain connected without e, otherwise acyclic

  mark all atoms unvisited
  temporarily remove e
  DFSVisit(a)
  restore e
  if visited[b]: return cyclic
  else:          return acyclic
  # one bond: O(|V| + |E|); all bonds: O(|E|·(|V| + |E|))
```

```text
ALGORITHM TarjanCyclicAndAcyclicBonds(G)
  INPUT : connected undirected molecular graph G
  OUTPUT: cyclic[e] for every bond e, articulation atoms and low-link numbers

  for each atom u: discovery[u] <- 0; low[u] <- 0
  for each bond e: cyclic[e] <- true
  time <- 0
  for each atom u:
      if discovery[u] == 0: DFSVisit(u, parent = none)

PROCEDURE DFSVisit(u, parent)
  time <- time + 1; discovery[u] <- time; low[u] <- discovery[u]
  childCount <- 0
  for each neighbour v of u:
      if discovery[v] == 0:
          childCount <- childCount + 1
          DFSVisit(v, u)
          low[u] <- min(low[u], low[v])
          if low[v] > discovery[u]: cyclic[(u,v)] <- false       # tree edge is a bridge
          if parent != none and low[v] >= discovery[u]: mark u articulation
      else if v != parent:
          low[u] <- min(low[u], discovery[v])                    # back edge
  if parent == none and childCount >= 2: mark u articulation
  # complexity: O(|V| + |E|)
```

```text
ALGORITHM UllmannSubgraphSearch(target G, query F)
  INPUT : target molecular graph G, query fragment F
  OUTPUT: all injective mappings of F into G

  M <- InitialUllmannMatrix(F, G)
  usedColumn[j] <- false for each target node j
  EnumerateSubgraph(depth = 0, M, usedColumn)

PROCEDURE EnumerateSubgraph(depth h, matrix P, usedColumn U)
  if h == |V(F)|:
      output P as a subgraph mapping
      return
  for each target column j with P[h,j] == 1 and U[j] == false:
      Psave <- P
      zero all entries in row h; P[h,j] <- 1; U[j] <- true
      if UllmannRefine(G, F, P, h): EnumerateSubgraph(h + 1, P, U)
      P <- Psave; U[j] <- false
```

```text
PROCEDURE UllmannRefine(target G, query F, matrix P, fixedDepth h)
  INPUT : current compatibility matrix P
  OUTPUT: true if every query row still has a possible target; false otherwise

  repeat:
      changed <- false
      for each allowed entry P[i,j] == 1 at or below the unfixed rows:
          valid <- true
          for each query neighbour x of i:
              found <- false
              for each target neighbour y of j:
                  if P[x,y] == 1: found <- true; break
              if not found: valid <- false; break
          if not valid:
              P[i,j] <- 0; changed <- true
              if row i has no 1 entries: return false
  until not changed
  return true
```

```text
ALGORITHM ModularProductMCS(G1, G2)
  INPUT : two labelled molecular graphs
  OUTPUT: maximum common connected subgraph as a set of atom matches

  P <- build product graph whose vertices are compatible atom pairs (u in G1, v in G2)
  add c-edge between pairs when both original graphs contain the corresponding bond
  add d-edge between pairs when neither original graph contains the corresponding bond
  run c-connected BronKerbosch on P
  return largest c-connected clique, decoded as atom matches
```

```text
ALGORITHM BronKerbosch(I, X, N)
  INPUT : current clique I, candidate extensions X, forbidden/processed vertices N
  OUTPUT: all maximal cliques

  if X is empty:
      if N is empty: output I
      return
  if exists n in N such that X subset Adj(n): return
  for each x in copy(X):
      BronKerbosch(I ∪ {x}, X ∩ Adj(x), N ∩ Adj(x))
      X <- X \ {x}
      N <- N ∪ {x}
```

## Exam-relevant points

- CIP priority first follows atomic number; isotopes of the same element follow mass number.
- If first-shell atoms are identical, compare the sorted next shell, and continue outward until a difference is found.
- Multiple bonds are handled by duplicating atoms; rings are opened by duplicate atoms and a ring path terminates when it would encounter an atom for the second time.
- R/S is assigned from ordered tetrahedral substituents; E/Z is assigned from the higher-priority substituent on each side of a double bond.
- Connectedness is reflexive, symmetric and transitive, so connected components are equivalence classes.
- Naively testing every bond for acyclicity by deleting it is correct but too slow; a low-link DFS labels all bridges in linear time.
- A root of a DFS tree is an articulation node iff it has at least two DFS-tree children; a non-root node is an articulation node iff a child has `low[child] >= discovery[node]`.
- An acyclic bond is exactly a DFS-tree edge `(v,w)` with `low[w] > discovery[v]`.
- Ullmann's assignment matrix has one row per query atom and one column per target atom; every query row must have exactly one selected target column, while each target column can be used at most once.
- The initial Ullmann matrix allows a query atom to map to a target atom only when labels are compatible and the target degree is at least the query degree.
- Ullmann refinement deletes `m_ij` when some neighbour of query atom `i` has no compatible neighbour of target atom `j`.
- MCS is NP-hard; product-graph MCS reduces a chemical graph problem to maximum clique.
- In the product graph, c-edges represent bonds in both molecules and d-edges represent non-bonds in both molecules; a clique is a mutually compatible set of matches.
- For connected MCS, the clique must be c-connected: the subgraph induced by c-edges must be connected.
- Bron-Kerbosch stores the current clique `I`, expandable candidates `X` and processed forbidden vertices `N` to enumerate each maximal clique once.

## Open questions

- The exercise traces on pages 3, 5, 16, 23, 25 and 33 contain many hand-computed intermediate matrices/trees; this page records the algorithmic conclusions, not every table entry.
- The notes mention optimising CIP comparison with Morgan-precomputed atom automorphism classes but do not specify the exact invariant vector used.
- The line-graph/Whitney section notes ΔY exchanges are rare in chemistry, but the source does not give a chemical counterexample.

## Pages touched by this ingest

Created: [[concepts/cip-sequence-rules]], [[concepts/connected-components]], [[concepts/smallest-ring-search]], [[concepts/rotatable-bonds]], [[concepts/maximum-common-substructure]], [[concepts/modular-product-graph]], [[concepts/bron-kerbosch-algorithm]], [[exercises/gci-e3-stereochemistry-rings-subgraph-and-mcs]].

Updated: [[concepts/molecular-structure-and-stereochemistry]], [[concepts/ring-perception]], [[concepts/biconnected-components-and-acyclic-bonds]], [[concepts/subgraph-isomorphism]], [[concepts/ullmann-algorithm]], [[overview]], [[synthesis]], [[open-questions]], [[index]], [[log]].
