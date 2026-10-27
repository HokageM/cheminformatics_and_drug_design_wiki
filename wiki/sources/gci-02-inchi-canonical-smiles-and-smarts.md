---
title: "GCI 02 - InChI, Canonical SMILES and SMARTS"
type: source
raw: raw/foundations_gci_part2.pdf
date_ingested: 2026-10-19
---

# GCI 02 - InChI, Canonical SMILES and SMARTS

Series: [[sources/gci-01-foundations-of-cheminformatics]] -> [[sources/gci-02-inchi-canonical-smiles-and-smarts]] -> [[sources/gci-03-stereochemistry-rings-substructure-and-mcs]] -> [[sources/gci-04-molecular-glues-descriptors-fingerprints-and-similarity]].

## Summary

- Part 2 continues GCI part 1 from ordinary SMILES into identifier and query languages: [[concepts/inchi-and-inchikey]], canonical SMILES and [[concepts/smarts]].
- InChI (International Chemical Identifier) is built as a versioned, normalised, multi-layer identifier whose main layer records formula, heavy-atom connectivity and hydrogens.
- Additional InChI layers encode charge, stereochemistry, isotopic substitution, fixed hydrogens and fixed isotopic information; opaque infixes can represent special cases in later versions.
- The InChIKey is a fixed-length, hashed, non-unique derivative of an InChI string that search engines can index, but it should not be treated as a lossless molecule representation.
- Canonicalisation solves the problem that many linear strings can represent the same graph by assigning a unique atom order independent of input numbering.
- A breadth-first traversal (BFS; breadth-first search, *Breitensuche*) is used as an order-preserving graph traversal where vertices are visited once and neighbours are queued.
- The Morgan algorithm assigns and iteratively refines connectivity values (CVs) for atoms from their neighbour CVs until refinement no longer separates atoms.
- If Morgan CVs alone do not distinguish atoms, tie-breaking enumerates candidate orderings over the remaining equivalent atoms and minimises the resulting order.
- The CANON algorithm uses extended-sum initial invariants, rank refinement and tie-breaking to compute a canonical atom order.
- Unique SMILES generation can use either CANON-style atom ordering or a GENES approach that combines two DFS passes, a bond-order system and bond priority rules.
- SMARTS is a SMILES-derived pattern language for chemical substructures: atom and bond expressions can include properties, recursion and logical operators.
- SMARTS examples include halogen wildcards, chain/ring constraints, aromaticity, ring membership, charge, chirality, logical conjunction/disjunction and recursive environment tests.
- Exercises trace canonical atom rankings and hand-generate InChI-like connection layers and canonical SMILES fragments for small and drug-like structures.

## Key concepts introduced

- [[concepts/inchi-and-inchikey]]
- [[concepts/molecular-canonicalization]]
- [[concepts/morgan-canonicalization]]
- [[concepts/canon-smiles-algorithm]]
- [[concepts/smarts]]
- [[exercises/gci-e2-identifiers-canonicalization-and-smarts]]

## Formulas & algorithms

```text
PROCEDURE BuildInCHI(molecule M)
  INPUT : normalised molecular graph with optional charge, stereo, isotope and fixed-H data
  OUTPUT: layered InChI string

  emit "InChI=" + version + "/" + normalisationType
  layer1.formula <- HillFormula(M)                         # C, H, then other elements alphabetically
  layer1.connectivity <- canonical heavy-atom connection table
  layer1.hydrogen <- mobile-hydrogen groups and fixed hydrogens when required
  layer2.charge <- net charge and protonation information
  layer3.stereo <- E/Z double-bond stereo and R/S-like tetrahedral stereo
  layer4.isotopic <- isotope-labelled atoms
  layer5.fixedH <- fixed locations of mobile H atoms
  layer6.fixedIsotopic <- fixed isotope positions
  return concatenate non-empty layers with InChI separators
```

```text
ALGORITHM BreadthFirstSearch(G, start)
  INPUT : graph G = (V,E), start vertex
  OUTPUT: traversal order

  for each v in V: queued[v] <- false
  Q <- empty queue
  enqueue start; queued[start] <- true
  while Q is not empty:
      v <- dequeue Q
      append v to order
      for each neighbour w of v in the chosen neighbour order:
          if not queued[w]:
              enqueue w; queued[w] <- true
  return order
  # complexity: O(|V| + |E|)
```

```text
ALGORITHM MorganCanonicalRanks(G)
  INPUT : labelled molecular graph
  OUTPUT: refined atom ranks, with possible ties

  orderElements <- O > N > C unless the implementation defines another element order
  for each atom v:
      CV[v] <- initial value from element, heavy-atom degree and non-H bond orders
  repeat at most |V| times:
      previous <- CV
      for each atom v:
          CV[v] <- combine(previous[v], sorted previous values of neighbours)
      compress CV values to ranks while preserving order
      if numberOfClasses(CV) did not increase: break
  return CV
  # unresolved ties require tie-breaking by enumerating candidate atom orders
```

```text
ALGORITHM CANONOrder(G)
  INPUT : molecular graph
  OUTPUT: canonical atom order

  initialRank <- extended sum over atom invariants
  ranks <- repeatedly refine initialRank by sorted neighbour-rank products
  while ranks contain tied atoms:
      select the first tied class under the current ranking
      for each candidate atom a in that class:
          split a into its own rank and refine again
          generate a candidate traversal/order
      keep the lexicographically minimal candidate order
  return order
```

```text
PROCEDURE MatchSMARTS(pattern P, molecule M)
  INPUT : SMARTS atom/bond expression graph P and molecular graph M
  OUTPUT: substructure matches

  parse atom primitives, bond primitives, recursion and logical operators
  candidateAtoms[p] <- atoms in M satisfying each atom expression p
  search assignments from pattern atoms to distinct molecule atoms
      require atom-expression truth for each assigned atom
      require bond-expression truth for each mapped pattern bond
      recursively evaluate nested SMARTS expressions when present
  return all complete assignments
```

## Exam-relevant points

- InChI strings are layered; InChIKeys are hashed, fixed-length and not lossless.
- The main InChI layer contains molecular formula, heavy-atom connectivity and H-atom information.
- Hill formula order: C first, H second, remaining elements alphabetically; without carbon, all elements are alphabetical.
- Canonicalisation is the production of an unambiguous atom order independent of the original numbering.
- BFS visits each node once and stores nodes in a queue; its result depends on the neighbour order.
- Morgan CVs are refined from adjacent atoms until either all atoms are separated or no further separation occurs.
- Canonical SMILES requires choosing the start atom, neighbour order and ring-closure numbering from the canonical order.
- SMARTS extends SMILES with atom and bond primitives plus logical operators; the first SMARTS atom describes the first atom of a match.
- Important SMARTS atom primitives in the notes: `*`, `a`, `A`, `D<n>`, `X<n>`, `v<n>`, `H<n>`, `h<n>`, `x<n>`, `R<n>`, `r<n>`, charge, isotope and chirality primitives.
- Important SMARTS bond primitives in the notes: single/aromatic, single or aromatic, directional up/down, double, triple, aromatic, any bond and ring bond.

## Open questions

- The handwritten notes state that InChI can contain opaque information in future versions, but the exact examples are not specified.
- The GENES table in the exercise trace is partly compressed; this ingest captures the rule sequence, but not every intermediate product number.
- Ring rendering in canonical SMILES pseudocode is flagged as tricky in the source: ring numbers must be opened and closed in the correct direction when backtracking.

## Pages touched by this ingest

Created: [[concepts/inchi-and-inchikey]], [[concepts/molecular-canonicalization]], [[concepts/morgan-canonicalization]], [[concepts/canon-smiles-algorithm]], [[concepts/smarts]], [[exercises/gci-e2-identifiers-canonicalization-and-smarts]].

Updated: [[concepts/smiles]], [[concepts/smiles-generation]], [[concepts/molecular-graphs]], [[concepts/molecular-file-formats]], [[concepts/molecular-structure-and-stereochemistry]], [[concepts/ring-perception]], [[overview]], [[synthesis]], [[open-questions]], [[index]], [[log]].
