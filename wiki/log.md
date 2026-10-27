---
title: Log
type: meta
updated: 2026-10-19
---

# Log

Append-only. Format: `## [YYYY-MM-DD] ingest|query|lint|refactor | <title>`

## [2026-09-30] refactor | Wiki initialised
Created: CLAUDE.md schema, wiki/ skeleton (sources, concepts, tools, entities, exercises, comparisons, assets), index.md, log.md, overview.md, synthesis.md, open-questions.md
Updated: —
Conflicts: none

## [2026-09-30] ingest | ciw_1.pdf — Lecture 1: Drug Action, Protein–Ligand Interactions and Lead Discovery
Source is a scanned/photographed handwritten German summary (22 pages, image-only PDF); text
extracted by rendering pages and reading them visually, then translated to English.
Created: sources/ciw-01-drug-action-and-molecular-interactions,
  concepts/drug-discovery-pipeline, concepts/pharmacokinetics-and-pharmacodynamics,
  concepts/admet, concepts/enzymes-and-receptors, concepts/protein-ligand-binding,
  concepts/desolvation-and-water, concepts/molecular-structure-and-stereochemistry,
  concepts/binding-thermodynamics, concepts/intermolecular-interactions,
  concepts/hydrogen-bond, concepts/ionic-interactions-and-metal-complexation,
  concepts/hydrophobic-effect, concepts/enthalpy-entropy-compensation,
  concepts/lead-optimization-heuristics, concepts/lead-finding-strategies,
  concepts/high-throughput-screening, concepts/virtual-screening, concepts/de-novo-design,
  concepts/protein-flexibility, exercises/ciw-e1-thermodynamics-and-hydrogen-bonds
Updated: index.md, synthesis.md, open-questions.md, overview.md, CLAUDE.md (source format)
Conflicts: none. 5 open questions recorded (hydrophobic coefficient units, enzyme name,
  ADMET mapping, missing exercise task 4, Kᵢ transcription check).

## [2026-09-30] ingest | ciw_2.pdf — Lecture 2: Substructure Search and Ring Perception
29-page scanned handwritten German summary (sections 2.1 and 2.2 plus exercises E2 and E3).
Created: sources/ciw-02-substructure-search-and-ring-perception,
  concepts/subgraph-isomorphism, concepts/ullmann-algorithm, concepts/vf2-algorithm,
  concepts/ring-perception, concepts/biconnected-components-and-acyclic-bonds,
  concepts/hanser-all-rings-algorithm, concepts/cycle-space-and-cycle-basis,
  concepts/sssr-and-minimal-cycle-basis, concepts/horton-algorithm,
  concepts/relevant-cycles-and-vismara, concepts/unique-ring-families,
  concepts/linkers-and-chains, exercises/ciw-e2-vf2-trace,
  exercises/ciw-e3-cycle-bases-and-linkers
Updated: index.md, synthesis.md
Conflicts: none. 2 new open questions (missing Ullmann description, E3 task numbering).

## [2026-09-30] ingest | ciw_3.pdf — Lecture 3: Pattern Mining, Structure Diagrams, Surfaces, Reduced Graphs
27-page scanned handwritten German summary (sections 2.3, 2.4, 2.5 and 3.1, plus exercises
E4 and E5).
Created: sources/ciw-03-pattern-mining-diagrams-surfaces-and-reduced-graphs,
  concepts/frequent-pattern-mining, concepts/moss-algorithm,
  concepts/structure-diagram-generation, concepts/ring-system-layout,
  concepts/collision-detection-scan-line, concepts/protein-ligand-interaction-diagrams,
  concepts/lennard-jones-potential, concepts/molecular-surfaces,
  concepts/connolly-surface-algorithm, concepts/marching-cubes,
  concepts/ball-pivoting-algorithm, concepts/kohonen-maps, concepts/reduced-graphs,
  concepts/feature-trees, concepts/feature-tree-comparison,
  exercises/ciw-e4-moss-and-surfaces, exercises/ciw-e5-feature-trees
Updated: index.md, synthesis.md, open-questions.md
Conflicts: none. 3 new open questions (MoSS enumeration order, missing Ex-5 tasks,
  Kohonen objective function). First cross-chapter links back to lecture 1 concepts
  (hydrophobic effect, desolvation, protein–ligand binding) via molecular surfaces.

## [2026-09-30] ingest | ciw_4.pdf — Lecture 4: Descriptor Evaluation, Clustering, Superposition
27-page scanned handwritten German summary (sections 3.2–3.5, all of chapter 4, and
exercise E5 task 5-2).
Created: sources/ciw-04-descriptor-evaluation-clustering-and-superposition,
  concepts/enrichment-factor, concepts/roc-curves-and-auc, concepts/pharmacophore,
  concepts/atom-pair-and-triplet-descriptors, concepts/ultrafast-shape-recognition,
  concepts/autocorrelation-vectors, concepts/affinity-fingerprints,
  concepts/clustering-of-molecules, concepts/hierarchical-clustering,
  concepts/jarvis-patrick-clustering, concepts/k-means-clustering,
  concepts/molecular-superposition, concepts/gaussian-molecular-representation,
  concepts/seal-algorithm, concepts/molecular-conformation, concepts/vsepr-model,
  concepts/conformation-generation, concepts/flexible-superposition,
  concepts/rmsd-and-point-set-superposition
Updated: exercises/ciw-e5-feature-trees (task 5-2 appended; now a 2-source page),
  index.md, synthesis.md, open-questions.md
Conflicts: none, but one notable tension recorded — lecture 4 states that 3D descriptors
  often perform worse than topological ones, which qualifies the lecture-3 premise that
  richer representations are better. 3 new open questions (%MAEF normalisation, SEA model,
  Sippl convergence).

## [2026-09-30] ingest | ciw_5.pdf — Lecture 5: Pharmacophores, QSAR, Docking
29-page scanned handwritten German summary (end of chapter 4, all of chapter 5, start of
chapter 6, plus exercise E6).
Created: sources/ciw-05-pharmacophores-qsar-and-docking,
  concepts/pharmacophore-derivation, concepts/disco-algorithm,
  concepts/pharmacophore-matching, concepts/catalyst-algorithm,
  concepts/caveat-algorithm, concepts/directed-tweak,
  concepts/ligandscout-algorithm, concepts/pharmer-algorithm,
  concepts/matched-molecular-pairs, concepts/matched-molecular-pair-analysis,
  concepts/qsar, concepts/physicochemical-parameters,
  concepts/lipophilicity-and-logp, concepts/hansch-analysis,
  concepts/free-wilson-analysis, concepts/3d-qsar, concepts/comfa, concepts/comsia,
  concepts/principal-component-analysis, concepts/partial-least-squares,
  concepts/qsar-model-validation, concepts/docking, concepts/scoring-functions,
  concepts/dock-algorithm, concepts/kuhl-algorithm, concepts/clix-algorithm,
  concepts/geometric-hashing-docking,
  exercises/ciw-e6-qsar-and-matched-molecular-pairs
Updated: index.md, synthesis.md, open-questions.md
Conflicts: none. This is the first ingest that closes loops rather than opening them —
  Böhm's scoring function re-expresses every lecture-1 interaction type as a regression
  term, and the distance-compatibility-graph/clique pattern now appears in three separate
  chapters (DISCO, DOCK, Kuhl). 4 new open questions (CAVEAT torsion bins, Pharmer Bloom
  filter, CoMFA relevance-vs-contribution note, docking clique-search complexity claim).

## [2026-09-30] ingest | ciw_6.pdf — Lecture 6: Flexible Docking, Binding Sites, Fragment Spaces, Protein–Protein Docking
Source: raw/ciw_6.pdf (28 pages, image-only scan of handwritten German notes).
Read all 28 pages with the ReadScannedSource procedure; no exercise sheet in this scan.
Created: sources/ciw-06-flexible-docking-binding-sites-and-fragment-spaces,
  concepts/pose-clustering, concepts/glide-hierarchical-filtering,
  concepts/flexible-docking, concepts/genetic-algorithm-docking,
  concepts/randomised-docking, concepts/place-and-join,
  concepts/incremental-construction-docking, concepts/binding-site-detection,
  concepts/ligsite-and-pocket, concepts/surfnet, concepts/cast-alpha-shapes,
  concepts/pass-algorithm, concepts/drugsite, concepts/evolutionary-site-prediction,
  concepts/binding-site-prediction-evaluation, concepts/druggability,
  concepts/combinatorial-libraries, concepts/focused-libraries,
  concepts/fragment-based-drug-design, concepts/chemical-space,
  concepts/fragment-spaces, concepts/fragment-space-search,
  concepts/protein-protein-docking, concepts/katchalski-katzir-algorithm,
  concepts/surface-reduction-for-docking, concepts/monte-carlo-protein-docking
Updated: concepts/de-novo-design (lecture-6 taxonomy section, stub -> solid, now 2 sources),
  index.md, synthesis.md, open-questions.md
Conflicts: none, but one correction of emphasis. The SCREEN result that pocket volume does
  not correlate with ligand volume weakens the shape-complementarity intuition behind
  concepts/dock-algorithm and concepts/molecular-surfaces; noted in concepts/druggability
  and as synthesis claim 29 rather than as a contradiction, since the lecture presents the
  two without comment. 7 new open questions (accuracy-figure semantics, DrugSite C and
  threshold, MAPpod contact term, Katchalski-Katzir sign convention, illegible FlexNovo
  line, the CAST-vs-DrugSite accuracy gap).
Note: this completes the ingest of raw/ciw_1.pdf through raw/ciw_6.pdf. A lint pass is now
  the natural next operation - the Tools, Entities and Comparisons index sections are still
  empty and many named tools (FlexX, GLIDE, GOLD, AutoDock, LUDI, MCSS, TOPAS, PatchDock,
  RosettaDock) now warrant pages in wiki/tools/.

## [2026-10-19] ingest | GCI 01 — Foundations of Cheminformatics
Source: raw/foundation_gci_part1.pdf (35-page scanned handwritten German summary, image-only). Read all 35 provided page images visually and translated to English.
Created: sources/gci-01-foundations-of-cheminformatics,
  concepts/cheminformatics, concepts/chemical-databases-and-search-engines,
  concepts/chemical-workflow-systems, concepts/molecular-graphs,
  concepts/molecular-file-formats, concepts/smiles, concepts/smiles-generation,
  concepts/markush-structures, entities/chemical-database-catalog,
  tools/knime, tools/pipeline-pilot, tools/azorange,
  exercises/gci-e1-databases-workflows-and-smiles
Updated: concepts/drug-discovery-pipeline, concepts/qsar,
  concepts/molecular-structure-and-stereochemistry, concepts/ring-perception,
  overview.md, synthesis.md, open-questions.md, index.md, log.md
Conflicts: none. 2 new open questions recorded (commercial database scope; exact SMILES exercise alternatives).
## [2026-10-19] ingest | GCI 02 - InChI, Canonical SMILES and SMARTS
Source is `raw/foundations_gci_part2.pdf`, a 29-page scanned handwritten German summary; page images were read visually and translated to English.
Created: sources/gci-02-inchi-canonical-smiles-and-smarts, concepts/inchi-and-inchikey, concepts/molecular-canonicalization, concepts/morgan-canonicalization, concepts/canon-smiles-algorithm, concepts/smarts, exercises/gci-e2-identifiers-canonicalization-and-smarts
Updated: concepts/smiles, concepts/smiles-generation, concepts/molecular-graphs, concepts/molecular-file-formats, concepts/molecular-structure-and-stereochemistry, concepts/ring-perception, overview.md, synthesis.md, open-questions.md, index.md, log.md
Conflicts: none. 3 open questions recorded (InChI opaque fields, GENES intermediate trace, canonical SMILES ring emission).

## [2026-10-19] ingest | GCI 03 - Stereochemistry, Rings, Substructure Search and MCS
Source: raw/foundations_gci_part3.pdf (34-page scanned handwritten German summary, image-only). Read all 34 provided page images visually and translated to English.
Created: sources/gci-03-stereochemistry-rings-substructure-and-mcs,
  concepts/cip-sequence-rules, concepts/connected-components,
  concepts/smallest-ring-search, concepts/rotatable-bonds,
  concepts/maximum-common-substructure, concepts/modular-product-graph,
  concepts/bron-kerbosch-algorithm,
  exercises/gci-e3-stereochemistry-rings-subgraph-and-mcs
Updated: concepts/molecular-structure-and-stereochemistry, concepts/ring-perception,
  concepts/biconnected-components-and-acyclic-bonds, concepts/subgraph-isomorphism,
  concepts/ullmann-algorithm, overview.md, synthesis.md, open-questions.md, index.md,
  log.md
Conflicts: none. 3 open questions recorded (part-3 exercise trace completeness, CIP
  optimisation invariant, ΔY exchange examples). The earlier Ullmann-details open question
  is resolved by the GCI part-3 refinement procedure.

## [2026-10-19] ingest | GCI 04 - Molecular Glues, Descriptors, Fingerprints and Similarity
Source: raw/foundations_gci_part4.pdf (16-page scanned handwritten German summary, image-only). Read all 16 provided page images visually and translated to English.
Created: sources/gci-04-molecular-glues-descriptors-fingerprints-and-similarity,
  concepts/molecular-glues, concepts/molecular-similarity,
  concepts/molecular-descriptors, concepts/topological-indices,
  concepts/molecular-fingerprints, concepts/ecfp-and-fcfp-fingerprints,
  concepts/similarity-and-distance-measures
Updated: concepts/protein-ligand-binding, concepts/intermolecular-interactions,
  concepts/binding-thermodynamics, concepts/hydrophobic-effect,
  concepts/virtual-screening, concepts/morgan-canonicalization,
  sources/gci-01-foundations-of-cheminformatics,
  sources/gci-02-inchi-canonical-smiles-and-smarts,
  sources/gci-03-stereochemistry-rings-substructure-and-mcs,
  overview.md, synthesis.md, open-questions.md, index.md, log.md
Conflicts: none. 3 open questions recorded (Randic worked example, ECFP duplicate-retention rule,
  Cosine-vs-Tanimoto efficiency). This completes the four-part GCI foundation series.

## [2026-10-19] lint | Post-GCI-series wiki lint
Scope: all 173 wiki pages after ingesting the four-part GCI series.
Fixed: stripped UTF-8 BOM from 9 pages written during the GCI 01 ingest
  (concepts/cheminformatics, concepts/chemical-databases-and-search-engines,
  concepts/chemical-workflow-systems, concepts/markush-structures,
  entities/chemical-database-catalog, exercises/gci-e1-databases-workflows-and-smiles,
  tools/knime, tools/pipeline-pilot, tools/azorange) — a BOM before the opening `---`
  breaks YAML frontmatter parsing in Obsidian/Dataview.
Fixed: dead wikilink `[[../CLAUDE]]` in overview.md replaced by a plain reference.
Checked clean: 0 dead links, 0 orphan pages, index.md in sync with the filesystem,
  all code fences balanced, all Mermaid blocks have a valid diagram header.
Noted, not changed: descriptive concept pages without pseudocode (admet,
  drug-discovery-pipeline, lead-finding-strategies, molecular-conformation,
  molecular-surfaces, pharmacokinetics-and-pharmacodynamics, pharmacophore,
  clustering-of-molecules, protein-ligand-interaction-diagrams) — no algorithm to encode.
Stub candidates for promotion once more sources arrive: concepts/high-throughput-screening,
  tools/pipeline-pilot, tools/azorange.
