---
title: "GCI 01 — Foundations of Cheminformatics"
type: source
raw: raw/foundation_gci_part1.pdf
date_ingested: 2026-10-19
---

# GCI 01 — Foundations of Cheminformatics

Series: [[sources/gci-01-foundations-of-cheminformatics]] -> [[sources/gci-02-inchi-canonical-smiles-and-smarts]] -> [[sources/gci-03-stereochemistry-rings-substructure-and-mcs]] -> [[sources/gci-04-molecular-glues-descriptors-fingerprints-and-similarity]].

## Summary

- Cheminformatics (Chemieinformatik) applies informatics methods to chemical problems: compound structures, properties and transformations become searchable data and predictive models.
- The central loop is experiment → data → model → prediction → new experiment, i.e. inductive learning from measured molecules to untested molecules.
- Bioinformatics is placed at target discovery; cheminformatics supports lead generation and lead optimisation.
- The history notes graph theory in chemistry in the 1960s and a 1962 QSAR study relating molecule descriptors and coefficients to activity.
- Chemical databases store molecules with biological effects, side effects, physicochemical properties, toxicity, synthesis and patent information.
- Named resources include PDB, ChEMBL, ZINC, PubChem, BRENDA, DrugBank, SureChEMBL, CSD, ChemSpider, eMolecules, SciFinder, MDDR, WDI, DNP, CAS and Ligand Expo.
- Markush structures represent many related patent compounds by a scaffold with variable substituent positions.
- Pipeline Pilot, KNIME and AZOrange automate cheminformatics preprocessing, descriptor calculation, model development, prediction and model maintenance.
- Molecules are treated as labelled graphs: atoms are vertices, bonds are edges, and 2D drawings can be searched and serialised.
- PDB, mol2, SDF and SMILES store different subsets of molecular information; omitted information must be inferred later.
- SD format records contain header, counts line, atom block, bond block, property block, optional data block and `$$$$` separators.
- SMILES encodes atoms, bonds, branches, ring numbers, aromaticity and stereochemistry in a compact line notation.
- DFS can generate a SMILES string by emitting atoms, bond symbols, branches and ring IDs; visited non-parent neighbours mark ring closures.
- The exercise pages apply database lookup, file-format interpretation, KNIME workflow reading and hand SMILES generation/validation.

## Key concepts introduced

- [[concepts/cheminformatics]]
- [[concepts/chemical-databases-and-search-engines]]
- [[entities/chemical-database-catalog]]
- [[concepts/chemical-workflow-systems]]
- [[concepts/molecular-graphs]]
- [[concepts/molecular-file-formats]]
- [[concepts/smiles]]
- [[concepts/smiles-generation]]
- [[concepts/markush-structures]]
- [[tools/knime]]
- [[tools/pipeline-pilot]]
- [[tools/azorange]]
- [[exercises/gci-e1-databases-workflows-and-smiles]]

## Formulas & algorithms

```text
PROCEDURE InductiveCheminformaticsLoop(problem P)
  INPUT : chemical problem and experiments that measure relevant properties
  OUTPUT: predictions for untested molecules

  experiments <- measure known molecules
  data <- standardise and store structures, properties and transformations
  model <- learn structure-property relationship from data
  predictions <- apply model to candidate molecules
  choose new experiments from predictions
  repeat until the decision is good enough
```

```text
MODEL EarlyQSAR(X, beta)
  INPUT : molecule-by-property matrix X, fitted coefficient vector beta
  OUTPUT: activity predictions y_hat

  y_hat <- X * beta
  compare y_hat with measured activity
  use the model to prioritise or explain compounds
```

```text
PROCEDURE ParseSDRecord(lines)
  INPUT : one SD-format molecule record ending before $$$$
  OUTPUT: molecular graph plus optional data fields

  header <- first three lines
  counts <- fourth line with atom and bond counts
  atoms <- next counts.nAtoms atom lines
  bonds <- next counts.nBonds bond lines
  properties <- read property lines
  data <- read tagged data blocks if present
  return graph(atoms, bonds), properties, data
```

```text
ALGORITHM GenerateSMILES(graph G, start atom a)
  INPUT : labelled molecular graph
  OUTPUT: one valid SMILES string

  ringIds <- mark DFS back edges with ring numbers
  visited <- empty set
  function emit(atom x, parent):
      append atomToken(x)
      visited.add(x)
      for each ring edge from x to already visited non-parent atom:
          append ring number
      for each unvisited neighbour y:
          if y is a branch: append "("
          append bondToken(x,y)
          emit(y, x)
          if y is a branch: append ")"
  emit(a, none)
  return string
  # complexity: O(|V| + |E|)
```

## Exam-relevant points

- Definition: cheminformatics is informatics for chemical problems.
- Guiding question: infer structure-property relationships.
- Pipeline boundary: target discovery = bioinformatics; lead generation and optimisation = cheminformatics.
- Database contents differ: biomacromolecular structures (PDB), bioactivity (ChEMBL/PubChem), purchasable compounds (ZINC), enzymes (BRENDA), drugs (DrugBank), patents (SureChEMBL/CAS) and crystal structures (CSD).
- PDB is line-/keyword-based and coordinate-centred; mol2 is TRIPOS record-based; SDF is record-based and extendable; SMILES is compact graph syntax.
- In SD files, atom lines encode coordinates, element, mass difference, charge and stereochemistry; bond lines encode atom indices, bond type, stereochemistry and topology.
- SMILES basics: implicit hydrogens, parentheses for branches, digits for rings, lowercase aromatic atoms, `@` for chirality and `/`/`\` for double-bond geometry.

## Open questions

- Commercial resources such as MDDR, WDI, DNP, SciFinder and CAS are listed only briefly; their current coverage should be checked from primary documentation before operational use.
- The handwritten exercise contains many alternative SMILES strings; the ingest captures the rules and selected checked outcomes rather than every alternative.

## Pages touched by this ingest

Created: [[concepts/cheminformatics]], [[concepts/chemical-databases-and-search-engines]], [[concepts/chemical-workflow-systems]], [[concepts/molecular-graphs]], [[concepts/molecular-file-formats]], [[concepts/smiles]], [[concepts/smiles-generation]], [[concepts/markush-structures]], [[entities/chemical-database-catalog]], [[tools/knime]], [[tools/pipeline-pilot]], [[tools/azorange]], [[exercises/gci-e1-databases-workflows-and-smiles]].

Updated: [[concepts/drug-discovery-pipeline]], [[concepts/qsar]], [[concepts/molecular-structure-and-stereochemistry]], [[concepts/ring-perception]], [[overview]], [[synthesis]], [[open-questions]], [[index]], [[log]].
