---
title: Open Questions
type: meta
tags: [meta]
created: 2026-09-30
updated: 2026-10-19
status: developing
---

# Open Questions

Unresolved questions, knowledge gaps, and flagged contradictions. Add entries during ingest
and lint; move them to *Resolved* (with a note in [[log]]) once answered.

## Open

- **GCI commercial database scope.** The foundation notes list MDDR, WDI, DNP, SciFinder and CAS only by name or short label. Expand their current scope and access model from primary documentation if they become operationally important. -> [[concepts/chemical-databases-and-search-engines]]
- **SMILES exercise alternatives.** The notes contain many hand-written candidate SMILES strings; this ingest captures the rules and selected checked outcomes, but not every alternative. Revisit the scan if exact exercise grading is needed. -> [[exercises/gci-e1-databases-workflows-and-smiles]]
- **GCI InChI opaque fields.** Part 2 notes that opaque information may appear in future InChI versions, but does not specify the fields or when they are generated. Check current InChI documentation before modelling those layers. -> [[concepts/inchi-and-inchikey]]
- **GENES intermediate trace.** The handwritten GENES unique-SMILES tables contain compressed product/rank columns; the wiki records the rule sequence but not every intermediate number. Revisit if exact exercise grading is needed. -> [[concepts/canon-smiles-algorithm]]
- **Canonical SMILES ring emission.** The notes explicitly warn that rings are easy to render incorrectly during recursive printing; clarify the exact open/close numbering convention against toolkit documentation. -> [[concepts/canon-smiles-algorithm]]
- **GCI part 3 exercise traces.** The stereochemistry, Ullmann and Bron-Kerbosch exercise pages contain dense handwritten intermediate tables; this ingest captures the algorithms and key outcomes but not every matrix/tree state. Revisit the images if exact grading is needed. -> [[exercises/gci-e3-stereochemistry-rings-subgraph-and-mcs]]
- **CIP optimisation invariant.** The notes mention optimising CIP comparison by precomputing atom automorphism information, for example Morgan-like ranks, but do not define the exact invariant vector. -> [[concepts/cip-sequence-rules]]
- **ΔY exchange in chemical line graphs.** The MCS section cites Whitney's line-graph exception and notes that it is rare in chemistry, but gives no concrete chemical example. -> [[concepts/maximum-common-substructure]]
- **GCI Randic-index worked example.** Part 4 gives the Randic formula clearly, but the handwritten note about an exceptional branched-alkane example is compressed. Revisit the scan or slides if exact exercise-style values are needed. -> [[concepts/topological-indices]]
- **ECFP duplicate-removal tie rule.** Part 4 states that duplicate circular substructures should be stored once, but does not specify the exact retention rule when identifiers/iteration depths differ. Check RDKit or original ECFP documentation before asserting toolkit-equivalent output. -> [[concepts/ecfp-and-fcfp-fingerprints]]
- **Cosine vs Tanimoto efficiency.** The notes say Cosine is more efficient than Tanimoto for some topological feature-vector comparisons, but do not state whether this is mathematical, indexing-related or implementation-specific. -> [[concepts/similarity-and-distance-measures]]

- **Hydrophobic-effect coefficient.** Lecture 1 gives ≈ −50 to −200 J·mol⁻¹·Å⁻² of buried
  surface. The common textbook value is ≈ 25–30 cal·mol⁻¹·Å⁻² (≈ 105–125 J·mol⁻¹·Å⁻²).
  Verify the unit and the intended range. → [[concepts/hydrophobic-effect]]
- **Enzyme name.** The notes write "Tyrosyl-RNA-Synthase"; the standard name is
  **tyrosyl-tRNA synthetase**. Confirm against the lecture slides. → [[concepts/hydrogen-bond]]
- **ADMET ↔ boundary-condition mapping.** The handwritten mapping of the six boundary
  conditions onto A-D-M-E-T is ambiguous for condition 3 (specificity → metabolism?).
  → [[concepts/admet]]
- **Exercise E1, task 4** is not present in the summary (tasks 1–3 and 5 are). Check whether
  it was skipped or belongs to another sheet. → [[exercises/ciw-e1-thermodynamics-and-hydrogen-bonds]]
- **Kᵢ recomputation.** Several Kᵢ values in the E1 table should be re-derived from the listed
  ΔG to check for transcription errors (e.g. ligand 3 at pH 7.4: ΔG = −41.8 kJ/mol).
- **Exercise E3 task numbering.** The sheet jumps in a way that suggests a task 3-3 exists
  which is not in the summary. → [[exercises/ciw-e3-cycle-bases-and-linkers]]
- **MoSS enumeration order.** Lecture 3 p. 1 gives the data structures but not the concrete
  duplicate-free enumeration order; the exercise trace on p. 6 implies
  `single ≺ aromatic ≺ double ≺ triple`. Confirm against the MoSS paper.
  → [[concepts/moss-algorithm]]
- **Exercise 5 tasks 5-2 ff.** Only task 5-1 appears in the lecture-3 scan; check whether
  the rest is in `raw/ciw_4.pdf`. → [[exercises/ciw-e5-feature-trees]]
- **Kohonen objective function.** The notes specify the neuron-selection criterion only as
  "objective function over the input vector (coordinates)". Fill in the standard
  best-matching-unit rule. → [[concepts/kohonen-maps]]
- **%MAEF normalisation.** Lecture 4 p. 1 glosses `%MAEF` only as "f-tree averaging"; the
  exact definition of the maximal achievable enrichment factor is not written out.
  → [[concepts/enrichment-factor]]
- **SEA approach.** Listed in one line as "target identification via molecular similarity of
  ligands"; the statistical model behind it is not described.
  → [[concepts/affinity-fingerprints]]
- **Sippl convergence.** The derivative is given for the z-axis only, and the claim that the
  optimisation cycle is independent of `U` is stated without argument.
  → [[concepts/rmsd-and-point-set-superposition]]
- **CAVEAT torsion bin size.** The bin size of the torsion angle t is said to depend on the
  opening angle a₂, but the functional form is not given.
  → [[concepts/caveat-algorithm]]
- **Pharmer's Bloom filter.** Listed as per-triangle metadata; what membership it tests
  (atom types? feature sets?) is not stated. → [[concepts/pharmer-algorithm]]
- **CoMFA "relevance, not contribution".** The marginal note argues that a small
  a_{f,x,y,z} at a high-variance grid point can still drive large affinity differences; the
  argument is compressed and worth reconstructing. → [[concepts/comfa]]
- **Docking clique-search complexity.** "Clique search is NP-hard, BK is exponential, but in
  general this does not hold for the docking problem" — the structural reason (geometric
  constraints bound clique size) is asserted, not argued. → [[concepts/kuhl-algorithm]]
- **Meaning of the binding-site accuracy figures.** The notes annotate methods with e.g.
  "74 % (3)", "63 % (1)", "8 % (1)". The parenthesised number appears to be the rank cut-off
  (true site among the top-1 or top-3 predictions), but the benchmark set and the criterion
  used are not stated, so the numbers are not comparable as written.
  → [[concepts/binding-site-prediction-evaluation]]
- **DrugSite's undefined parameters.** The factor `C` in `P_i = Σ_j (A_j·C/r¹² − B_j·C/r⁶)`
  is never defined, and neither is the `threshold` in `CL = mean − threshold × sd`. Both
  control the result completely. → [[concepts/drugsite]]
- **MAPpod's contact term.** `ΔG_MAPpod = ΔG_target desolv + ΔG_ligand desolv + ΔG_contact`
  — whether the contact term is a buried-surface-area term or a contact count is not stated.
  → [[concepts/druggability]]
- **Katchalski-Katzir sign conventions.** Why protein A gets `p ≪ 0` and protein B gets
  `0 < p < 1` (rather than both negative, or symmetric values) is asserted without
  derivation; the asymmetry presumably keeps the correlation from being dominated by
  core-core terms. → [[concepts/katchalski-katzir-algorithm]]
- **FlexNovo.** The handwritten line describing FlexNovo is partly illegible; only that it
  searches fragment spaces is recoverable. Worth looking up the original description.
  → [[concepts/fragment-space-search]]
- **Accuracy gap between geometric and energy-based site detection.** CAST reaches 74 % and
  DrugSite 8 % — an eightfold difference that the notes do not explain. Is this a
  parameterisation failure, a benchmark artefact, or a real limitation of probe-energy
  methods? → [[concepts/binding-site-detection]]

## Flagged contradictions

_(none yet)_

## Resolved

- **Ullmann algorithm details.** CIW lecture 2 only gave the Ullmann pros/cons, but GCI part 3 supplies the initial matrix, row/column assignment conditions and neighbourhood refinement procedure. -> [[concepts/ullmann-algorithm]], [[sources/gci-03-stereochemistry-rings-substructure-and-mcs]]
