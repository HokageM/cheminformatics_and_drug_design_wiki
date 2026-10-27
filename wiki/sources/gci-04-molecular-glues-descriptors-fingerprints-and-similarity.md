---
title: "GCI 04 - Molecular Glues, Descriptors, Fingerprints and Similarity"
type: source
raw: raw/foundations_gci_part4.pdf
date_ingested: 2026-10-19
---

# GCI 04 - Molecular Glues, Descriptors, Fingerprints and Similarity

Series: [[sources/gci-01-foundations-of-cheminformatics]] -> [[sources/gci-02-inchi-canonical-smiles-and-smarts]] -> [[sources/gci-03-stereochemistry-rings-substructure-and-mcs]] -> [[sources/gci-04-molecular-glues-descriptors-fingerprints-and-similarity]].

## Summary

- Part 4 closes the GCI foundation lecture by moving from exact molecular graphs to approximate comparison: binding, [[concepts/molecular-glues]], descriptors, fingerprints and similarity metrics.
- A molecular glue (molekularer Klebstoff) is framed as a small molecule that stabilises or induces binding of a molecule to a protein by arranging functional groups in space.
- Protein-ligand complexes are governed by reversible intermolecular interactions; the notes repeat K_i = [ligand][protein]/[ligand-protein], ΔG = RT ln K_i and IC50 as the 50 % activity concentration.
- The similarity principle states that molecules with similar physico-chemical properties tend statistically to behave similarly in protein binding, especially when the protein or exact binding mode is unknown.
- Similarity searching starts from one or more known binders, searches a database for related molecules, identifies relevant functional groups, predicts binding properties and selects screening compounds.
- Molecular descriptors are quantitative molecular characterisations chosen for efficient, computer-supported similarity decisions.
- Descriptor choices are separated by the kind of similarity, the molecular properties encoded, the representation type and the comparison algorithm.
- Topological indices compress a molecular graph into scalar numbers: the Wiener index sums all non-H shortest-path distances, while the Randic index sums inverse square-root degree products over bonds.
- Floyd-Warshall computes all-pairs shortest paths for the Wiener index in O(n^3) time and O(n^2) space by allowing intermediate vertices one set at a time.
- Molecular fingerprints replace one scalar by bit or count vectors: structural keys ask a fixed list of yes/no questions; hashed fingerprints and Bloom-filter-like encodings trade interpretability for fixed length.
- Daylight fingerprints canonicalise paths, hash them and set several bits; they are deterministic and useful as substructure filters but not uniquely invertible.
- ECFP/FCFP fingerprints use Morgan-style circular neighbourhood growth: initial atom identifiers, iterative neighbour updates and duplicate removal generate integer features for screening, SAR analysis and library design.
- Similarity and distance measures compare feature vectors or feature sets; similarity is commonly normalised to [0,1], while metric distances satisfy non-negativity, identity, symmetry and triangle inequality.
- Manhattan, Euclidean and Soergel distances are given for numeric and binary vectors; Soergel distance is the complement of the Tanimoto/Jaccard coefficient for binary fingerprints.
- Tanimoto, Dice, Cosine and Tversky coefficients are compared; Tanimoto is the default for topological feature vectors, Cosine is noted as efficient, and Tversky can express asymmetric substructure-like similarity.

## Key concepts introduced

- [[concepts/molecular-glues]]
- [[concepts/molecular-similarity]]
- [[concepts/molecular-descriptors]]
- [[concepts/topological-indices]]
- [[concepts/molecular-fingerprints]]
- [[concepts/ecfp-and-fcfp-fingerprints]]
- [[concepts/similarity-and-distance-measures]]

## Formulas & algorithms

```text
PROCEDURE SimilaritySearch(knownBinders K, database D)
  INPUT : one or more molecules known to bind a target; compound database D
  OUTPUT: ranked candidates and candidate functional motifs

  descriptorsK <- compute descriptors or fingerprints for K
  for each molecule m in D:
      descriptorsM <- compute the same representation for m
      score[m] <- similarity(descriptorsM, descriptorsK)
  ranked <- sort D by decreasing score
  motifs <- inspect features common to K and high-ranked molecules
  select a diverse high-ranked subset for screening
  return ranked, motifs
```

```text
ALGORITHM FloydWarshallShortestPaths(W)
  INPUT : weighted adjacency matrix W with W[i,i]=0, W[i,j]=1 for bonds, infinity otherwise
  OUTPUT: all-pairs shortest-path matrix D

  D <- W
  n <- number of atoms
  for k in 1..n:
      for i in 1..n:
          for j in 1..n:
              D[i,j] <- min(D[i,j], D[i,k] + D[k,j])
  return D
  # time: O(n^3), space: O(n^2)
```

```text
ALGORITHM WienerIndex(G)
  INPUT : molecular graph G over non-H atoms
  OUTPUT: scalar Wiener index W

  D <- FloydWarshallShortestPaths(adjacencyMatrix(G))
  W <- 0
  for each unordered atom pair {i,j}:
      W <- W + D[i,j]
  return W
```

```text
ALGORITHM RandicIndex(G)
  INPUT : molecular graph G over non-H atoms
  OUTPUT: scalar branching index R

  R <- 0
  for each bond (i,j) in G:
      R <- R + 1 / sqrt(degreeNonH(i) * degreeNonH(j))
  return R
```

```text
PROCEDURE StructuralKeyFingerprint(molecule M, featureList F)
  INPUT : molecule M and ordered feature/query list F = [G1, ..., Gn]
  OUTPUT: bit vector B of length n

  for j in 1..n:
      if Gj is present as a subgraph or property of M:
          B[j] <- 1
      else:
          B[j] <- 0
  return B
```

```text
ALGORITHM DaylightFingerprint(M, pathLengthRange, nBits)
  INPUT : molecular graph M, allowed path lengths, fingerprint size nBits
  OUTPUT: hashed path fingerprint bit vector B

  B <- all zeros
  paths <- enumerate paths in M within pathLengthRange
  for each path p in paths:
      canonical <- canonicalPathString(p)
      seed <- integerFrom(canonical)
      bits <- pseudoRandomBits(seed, count = 4..5, range = 1..nBits)
      for each b in bits: B[b] <- 1
  return B
```

```text
ALGORITHM ECFP(M, radius r)
  INPUT : molecular graph M, neighbourhood radius r
  OUTPUT: set of circular feature identifiers

  for each atom a:
      id[a,0] <- initialAtomIdentifier(a)
      atomSet[a,0] <- {a}; bondSet[a,0] <- {}
  features <- {(id[a,0], atomSet[a,0], bondSet[a,0]) for all atoms a}
  for k in 1..r:
      for each atom a:
          env <- [(bondOrder(a,b), id[b,k-1]) for each neighbour b]
          sortedEnv <- sort(env)
          vector <- [id[a,k-1]] + sortedEnv + optionalStereo(a, k)
          id[a,k] <- hash(vector)
          atomSet[a,k], bondSet[a,k] <- union neighbourhood atoms and bonds up to k
          add (id[a,k], atomSet[a,k], bondSet[a,k]) to features
      remove duplicate features with identical atomSet and bondSet
  return feature identifiers from features
```

## Exam-relevant points

- Similarity searching is only statistical when the protein structure or relevant binding functional groups are unknown.
- A descriptor workflow requires four decisions: what similarity means, which properties to encode, what representation to produce and which comparison algorithm to use.
- Wiener index: sum of shortest paths between all non-H atom pairs; compactness/branching information, but not unique.
- Floyd-Warshall recurrence: `d_ij^(k) = min(d_ij^(k-1), d_ik^(k-1) + d_kj^(k-1))`.
- Randic index: sum over bonds of `1/sqrt(deg(i)deg(j))`; compare molecules of equal atom count.
- Structural keys are interpretable fixed questions; hashed fingerprints are fixed length and faster but bit positions cannot be uniquely mapped back to structures.
- Bloom filters are probabilistic membership filters; in fingerprints they motivate multiple hash-set bits and possible false positives.
- ECFP is circular and Morgan-like; FCFP changes the initial atom labels toward pharmacophoric properties.
- Duplicate ECFP features arise because different central atoms can describe the same substructure; duplicate removal keeps each substructure feature once.
- For binary vectors with counts `a = |A|`, `b = |B|`, `c = |A ∩ B|`: Tanimoto/Jaccard is `c/(a+b-c)`, Dice is `2c/(a+b)`, Cosine is `c/sqrt(ab)` and Tversky is `c/(α(a-c)+β(b-c)+c)`.
- Tanimoto is the usual comparison for topological fingerprints; Tversky becomes asymmetric when α != β and is useful for containment-like comparisons.

## Open questions

- The handwritten note about an exceptional Randic-index calculation for branched alkanes is partly compressed; this ingest records the formula and the same-atom-count caveat, not the unclear worked example.
- The ECFP duplicate-removal tie rule is described only qualitatively in the notes. Toolkit documentation should be checked before relying on exact retention order.
- The notes state that Cosine is more efficient than Tanimoto for some fingerprint comparisons but do not specify the implementation model.

## Pages touched by this ingest

Created: [[concepts/molecular-glues]], [[concepts/molecular-similarity]], [[concepts/molecular-descriptors]], [[concepts/topological-indices]], [[concepts/molecular-fingerprints]], [[concepts/ecfp-and-fcfp-fingerprints]], [[concepts/similarity-and-distance-measures]].

Updated: [[concepts/protein-ligand-binding]], [[concepts/intermolecular-interactions]], [[concepts/binding-thermodynamics]], [[concepts/hydrophobic-effect]], [[concepts/virtual-screening]], [[concepts/morgan-canonicalization]], [[sources/gci-01-foundations-of-cheminformatics]], [[sources/gci-02-inchi-canonical-smiles-and-smarts]], [[sources/gci-03-stereochemistry-rings-substructure-and-mcs]], [[overview]], [[synthesis]], [[open-questions]], [[index]], [[log]].
