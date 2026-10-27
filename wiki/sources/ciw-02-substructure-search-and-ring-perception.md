---
title: CiW Lecture 2 — Substructure Search and Ring Perception
type: source
raw: raw/ciw_2.pdf
tags: [lecture, graph-algorithms, substructure-search, rings]
date_ingested: 2026-09-30
pages: 29
---

# CiW Lecture 2 — Substructure Search and Ring Perception

Handwritten German summary of lecture 2, sections **2.1 Substructure search** (pp. 1–6) and
**2.2 Definition and computation of ring bases** (pp. 9–25), plus exercise sheets
**E2** (pp. 7–8) and **E3** (pp. 26–29). Translated to English.

## Summary

### 2.1 Substructure search

- **Problem**: given a molecular graph G and a fragment F, does F occur as a substructure of
  G? Find a mapping m: F → G. This is **subgraph isomorphism** and is **NP-complete**.
  See [[concepts/subgraph-isomorphism]].
- **Ullmann algorithm** — matrix-based. *Advantages*: clean separation between node/edge
  compatibility checking and the graph algorithm; no final subgraph-isomorphism check needed;
  extensible to disconnected subgraphs and molecules. *Disadvantages*: the matrix form gives
  individual steps costing O(|V₁|·|V₂|); the iterative refinement of the whole matrix at each
  matching extension is runtime-intensive. See [[concepts/ullmann-algorithm]].
- **VF2 algorithm** — state-space search with local extension and look-ahead pruning.
  Decide locally and ad hoc which nodes to map; use a look-ahead strategy to detect
  unextendable mappings early. See [[concepts/vf2-algorithm]].
- **Benchmark**: VF2 ≈ 10 ms almost ever; Ullmann 10–1000 ms. Explicit hydrogens and rings
  hurt both, Ullmann far more. VF2 is roughly size-independent; Ullmann grows with size.
  See [[concepts/vf2-algorithm]] § Performance.

### 2.2 Ring perception

- **Acyclic bond**: a bond whose removal disconnects the molecular graph. Naive test per bond
  is O(|V|+|E|) ⇒ O(|E|(|V|+|E|)) overall; computing **biconnected components** in one DFS
  pass gives O(|V|+|E|). See [[concepts/biconnected-components-and-acyclic-bonds]].
- **All rings** (Ω): Hanser's *collapsing P-graph* algorithm enumerates every cycle.
  Exponential in the worst case. See [[concepts/hanser-all-rings-algorithm]].
- **Cycle space**: cycles form a vector space over GF(2) under ⊕ (symmetric difference /
  XOR on edge vectors). Every basis has **μ(G) = |E| − |V| + c(G)** cycles — the
  **cyclomatic number**. See [[concepts/cycle-space-and-cycle-basis]].
- **SSSR** = a **minimal cycle basis** (smallest set of smallest rings). Consists only of
  elementary cycles, is chemically intuitive, but is **not unique**.
  See [[concepts/sssr-and-minimal-cycle-basis]].
- **Horton's algorithm** computes a minimal cycle basis: enumerate a candidate set via
  Horton's theorem, sort by length, greedily add independent cycles (Gauss) until μ are
  chosen. Total O(μ·|V|·|E|²). See [[concepts/horton-algorithm]].
- **Relevant cycles** (Plotkin) = the union of all minimal cycle bases; this set **is unique**
  but can be exponentially large. Vismara's theorem gives a local criterion and Vismara's
  algorithm computes polynomially many **prototypes** (RCPs) grouped into **families** (RCFs).
  See [[concepts/relevant-cycles-and-vismara]].
- **Unique Ring Families (URF)** fix the remaining chemical problems (para-substituted rings
  overcounting). URF-related is an equivalence relation; a URF is an equivalence class, and
  URFs are really **edge sets**, not cycles. Computable in O(|E|⁵ + |V|²), < 200 ms.
  See [[concepts/unique-ring-families]].
- **Linkers and chains**: a bond is part of a **linker** iff removing it splits the molecule
  into multiple connected components each containing at least one ring.
  See [[concepts/linkers-and-chains]].

## Key concepts introduced

| Page(s) | Concept | Wiki page |
|---|---|---|
| 1 | Subgraph isomorphism, NP-completeness | [[concepts/subgraph-isomorphism]] |
| 1 | Ullmann algorithm, pros and cons | [[concepts/ullmann-algorithm]] |
| 2–6 | VF2: states, P(S), feasibility, performance | [[concepts/vf2-algorithm]] |
| 7–8 | Exercise E2 — VF2 trace | [[exercises/ciw-e2-vf2-trace]] |
| 9 | Acyclic bonds, biconnected components | [[concepts/biconnected-components-and-acyclic-bonds]] |
| 10–11 | Hanser collapsing P-graph, ALL-RINGS | [[concepts/hanser-all-rings-algorithm]] |
| 12–13, 15 | Cycles, ⊕, cycle space, cyclomatic number | [[concepts/cycle-space-and-cycle-basis]] |
| 14 | Minimal cycle basis, SSSR | [[concepts/sssr-and-minimal-cycle-basis]] |
| 16–17 | Horton's theorem and algorithm | [[concepts/horton-algorithm]] |
| 18–23 | Relevant cycles, Vismara, RCF/RCP | [[concepts/relevant-cycles-and-vismara]] |
| 24–25 | Essential rings, URF-pair-related, URF | [[concepts/unique-ring-families]] |
| 26–29 | Exercise E3 — cycle bases, linkers & chains | [[exercises/ciw-e3-cycle-bases-and-linkers]], [[concepts/linkers-and-chains]] |

## Formulas & algorithms

```text
μ(G) = |E| − |V| + c(G)                 # cyclomatic number = size of any cycle basis
C ⊕ C' = (C ∪ C') \ (C ∩ C')            # cycle addition = XOR on edge sets
|C| = |E_C|,  |B| = Σ_{C ∈ B} |C|        # cycle length and basis length
Horton total runtime:  O(μ · |V| · |E|²)
Vismara runtime:       O(|V|·|E|²) + O(μ·|E|³)
URF computation:       O(|E|⁵ + |V|²)
RC enumeration:        O(|V| · |C_R|)    # optimal
```

## Exam-relevant points

- Subgraph isomorphism is **NP-complete**; both Ullmann and VF2 are exponential worst-case.
- The four VF2 feasibility rules: **R_match, R_adj (1-look-ahead), R_next (2-look-ahead),
  R_sem**, combined by conjunction.
- μ(G) = |E| − |V| + c(G), and that this is the minimum number of edges whose removal turns
  G into a forest (spanning tree).
- A minimal cycle basis contains only **elementary** cycles and is **not unique**;
  the set of **relevant** cycles **is** unique but may be exponential.
- Cube example: μ = 5, relevant cycles p = 6, SSSR = 5, URFs = 6.
- The addition operation is closed on cycles but **not** on elementary cycles.

## Open questions

- Page 1 announces "2.1 Substructure search" but starts directly with the Ullmann summary;
  the algorithm's own description may be in a slide set not covered by this summary.
- Exercise E3 task numbering: the summary shows tasks 3-1 and 3-2 — confirm whether an
  E3 task 3-3 exists.

## Pages touched by this ingest

Created: 11 concept pages, 2 exercise pages (see table above).
Updated: [[index]], [[log]], [[synthesis]], [[open-questions]].
