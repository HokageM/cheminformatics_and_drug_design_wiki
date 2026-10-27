---
title: Index
type: meta
updated: 2026-10-19
---

# Index

Catalog of every page in the wiki. Read this first when answering a query.

## Meta
- [[overview]] — what this wiki covers and how it is organised.
- [[synthesis]] — evolving big-picture thesis of the field.
- [[open-questions]] — unresolved questions, gaps, contradictions.
- [[log]] — chronological record of ingests, queries and lint passes.

## Sources
- [[sources/ciw-01-drug-action-and-molecular-interactions]] — lecture 1 + exercise E1: drug development, pharmacology, protein–ligand interactions, thermodynamics, lead finding. (raw/ciw_1.pdf, 22 pp.)
- [[sources/ciw-02-substructure-search-and-ring-perception]] — lecture 2 + exercises E2/E3: subgraph isomorphism, Ullmann, VF2, ring perception, cycle bases, SSSR, relevant cycles, URFs. (raw/ciw_2.pdf, 29 pp.)
- [[sources/ciw-03-pattern-mining-diagrams-surfaces-and-reduced-graphs]] — lecture 3 + exercises E4/E5: frequent pattern mining, structure diagram generation, molecular surfaces, reduced graphs and feature trees. (raw/ciw_3.pdf, 27 pp.)
- [[sources/ciw-04-descriptor-evaluation-clustering-and-superposition]] — lecture 4 + exercise E5: enrichment/ROC evaluation, 3D descriptors, clustering, molecular superposition and conformation generation. (raw/ciw_4.pdf, 27 pp.)
- [[sources/ciw-05-pharmacophores-qsar-and-docking]] — lecture 5 + exercise E6: pharmacophore derivation and matching, QSAR (Hansch, Free–Wilson, CoMFA/CoMSIA), model validation, matched molecular pairs, docking. (raw/ciw_5.pdf, 29 pp.)
- [[sources/ciw-06-flexible-docking-binding-sites-and-fragment-spaces]] — lecture 6: pose clustering, flexible docking (GA, randomised, place & join, incremental construction), binding-site detection, druggability, combinatorial and fragment-based design, fragment spaces, protein–protein docking. (raw/ciw_6.pdf, 28 pp.)

- [[sources/gci-01-foundations-of-cheminformatics]] — GCI foundation part 1: definition/history of cheminformatics, databases, workflows, molecular graphs, file formats, SMILES and SMILES generation. (raw/foundation_gci_part1.pdf, 35 pp.)
- [[sources/gci-02-inchi-canonical-smiles-and-smarts]] - GCI foundation part 2: InChI and InChIKey, molecular canonicalisation, Morgan/CANON/GENES unique SMILES and SMARTS query syntax. (raw/foundations_gci_part2.pdf, 29 pp.)
- [[sources/gci-03-stereochemistry-rings-substructure-and-mcs]] - GCI foundation part 3: CIP stereochemistry, smallest rings, connected components, cyclic/acyclic and rotatable bonds, Ullmann search, MCS and Bron-Kerbosch. (raw/foundations_gci_part3.pdf, 34 pp.)
- [[sources/gci-04-molecular-glues-descriptors-fingerprints-and-similarity]] - GCI foundation part 4: molecular glues, similarity searching, descriptors, topological indices, fingerprints, ECFP/FCFP and similarity coefficients. (raw/foundations_gci_part4.pdf, 16 pp.)

## Concepts
### Cheminformatics foundations and molecular representation
- [[concepts/cheminformatics]] — informatics methods for chemical problems; experiment-data-model-prediction loop. (1 source)
- [[concepts/chemical-databases-and-search-engines]] — structure, bioactivity, availability, enzyme, drug, patent and crystal databases. (1 source)
- [[concepts/chemical-workflow-systems]] — node-based automation for data cleaning, descriptors, QSAR models and predictions. (1 source)
- [[concepts/molecular-graphs]] - atoms as labelled vertices and bonds as labelled edges; basis for traversal and canonical order. (2 sources)
- [[concepts/molecular-file-formats]] - PDB, mol2, SDF, SMILES, InChI/InChIKey and SMARTS-style strings. (2 sources)
- [[concepts/smiles]] - compact line notation; contrasted with canonical SMILES and SMARTS. (2 sources)
- [[concepts/smiles-generation]] - DFS-based generation plus canonical ordering for unique SMILES. (2 sources)
- [[concepts/markush-structures]] — patent-style generic structures with variable substituents. (1 source)
- [[concepts/inchi-and-inchikey]] - layered chemical identifiers and fixed-length hashed lookup keys. (1 source)
- [[concepts/molecular-canonicalization]] - deterministic atom ordering for identifiers and canonical line notations. (1 source)
- [[concepts/morgan-canonicalization]] - iterative connectivity-value refinement for canonical atom ranking and ECFP feature growth. (2 sources)
- [[concepts/canon-smiles-algorithm]] - CANON and GENES routes to unique SMILES. (1 source)
- [[concepts/smarts]] - SMILES-derived substructure query language with atom, bond and logical primitives. (2 sources)
- [[concepts/cip-sequence-rules]] - graph-based CIP substituent ordering for R/S and E/Z stereochemistry. (1 source)
- [[concepts/connected-components]] - DFS partition of a molecular graph into covalently connected fragments. (1 source)

### Molecular descriptors, fingerprints and similarity
- [[concepts/molecular-glues]] - small molecules that stabilise protein-bound states by presenting functional groups in space. (1 source)
- [[concepts/molecular-similarity]] - statistical comparison of molecules by chosen properties for ligand-based search. (1 source)
- [[concepts/molecular-descriptors]] - quantitative molecular characterisations for comparison, QSAR and screening. (1 source)
- [[concepts/topological-indices]] - scalar graph descriptors such as Wiener and Randic indices. (1 source)
- [[concepts/molecular-fingerprints]] - bit or count vector encodings of structural features. (1 source)
- [[concepts/ecfp-and-fcfp-fingerprints]] - circular Morgan-style fingerprints with structural or pharmacophoric atom identifiers. (1 source)
- [[concepts/similarity-and-distance-measures]] - Manhattan, Euclidean, Soergel, Tanimoto, Dice, Cosine and Tversky comparisons. (1 source)

- [[concepts/drug-discovery-pipeline]] — preclinical/clinical stages, hit vs lead, where computers enter. (2 sources)
- [[concepts/pharmacokinetics-and-pharmacodynamics]] — what the drug does to the body vs what the body does to the drug. (1 source)
- [[concepts/admet]] — absorption, distribution, metabolism, elimination, toxicity and the six boundary conditions. (1 source)
- [[concepts/enzymes-and-receptors]] — the two main target classes; competitive vs allosteric inhibition. (1 source)
- [[concepts/protein-ligand-binding]] — complementarity, statistical ligand similarity and the eight stages of complex formation. (2 sources)
- [[concepts/desolvation-and-water]] — hydration shell, desolvation, bridging waters, H-bond balance sheet. (1 source)
- [[concepts/molecular-structure-and-stereochemistry]] - bonds, hybridisation, conformation, isomerism, stereo layers and CIP labels. (4 sources)
- [[concepts/binding-thermodynamics]] — Kᵢ, ΔG = RT ln Kᵢ, ΔG = ΔH − TΔS, IC₅₀. (2 sources)
- [[concepts/intermolecular-interactions]] — interaction classes in a protein–ligand complex and similarity descriptors. (2 sources)
- [[concepts/hydrogen-bond]] — donors, acceptors, geometry criteria, scoring. (1 source)
- [[concepts/ionic-interactions-and-metal-complexation]] — salt bridges, protonation states, metal binders. (1 source)
- [[concepts/hydrophobic-effect]] — entropy-driven packing of lipophilic surfaces. (2 sources)
- [[concepts/enthalpy-entropy-compensation]] — why binding affinity is not additive. (1 source)
- [[concepts/lead-optimization-heuristics]] — five rules of thumb, each with its caveat. (1 source)
- [[concepts/lead-finding-strategies]] — traditional, screening, virtual screening, similarity, de novo. (1 source)
- [[concepts/high-throughput-screening]] — experimental screening of large libraries. (1 source)
- [[concepts/virtual-screening]] — structure-based vs ligand-based computational screening. (2 sources)
- [[concepts/de-novo-design]] — constructing molecules inside the binding site from fragments; atom-/fragment-/template-based (LUDI, MCSS). (2 sources)
- [[concepts/protein-flexibility]] — six levels of flexibility; the central modelling challenge. (1 source)

### Graph algorithms & substructure search
- [[concepts/subgraph-isomorphism]] - the NP-complete problem behind substructure search; basis for MCS. (2 sources)
- [[concepts/ullmann-algorithm]] - matrix-refinement solver with explicit GCI initial matrix and neighbourhood pruning. (2 sources)
- [[concepts/vf2-algorithm]] — state-space search with look-ahead; the practical default. (1 source)

### Maximum common substructure and clique search
- [[concepts/maximum-common-substructure]] - largest shared graph pattern between two molecules; MCIS/MCES variants. (1 source)
- [[concepts/modular-product-graph]] - compatibility graph whose cliques encode common subgraphs. (1 source)
- [[concepts/bron-kerbosch-algorithm]] - maximal-clique enumeration with candidate and processed sets; MCS engine. (1 source)

### Ring perception
- [[concepts/ring-perception]] - ring concepts, DFS ring closures, SMARTS predicates and smallest-ring search. (4 sources)
- [[concepts/smallest-ring-search]] - BFS-based local shortest-cycle detection around an atom or bond. (1 source)
- [[concepts/biconnected-components-and-acyclic-bonds]] - ring/chain split in one DFS pass with low-link bridge detection. (2 sources)
- [[concepts/rotatable-bonds]] - non-ring single bonds between non-terminal atoms; torsional degrees of freedom. (1 source)
- [[concepts/hanser-all-rings-algorithm]] — collapsing P-graph; enumerates all cycles Ω. (1 source)
- [[concepts/cycle-space-and-cycle-basis]] — cycles as a GF(2) vector space; cyclomatic number μ. (1 source)
- [[concepts/sssr-and-minimal-cycle-basis]] — the chemically intuitive but ambiguous answer. (1 source)
- [[concepts/horton-algorithm]] — greedy shortest-first computation of a minimal cycle basis. (1 source)
- [[concepts/relevant-cycles-and-vismara]] — the unique but possibly exponential cycle set. (1 source)
- [[concepts/unique-ring-families]] — URFs; the concept that satisfies all five requirements. (1 source)
- [[concepts/linkers-and-chains]] — classifying acyclic bonds for scaffold analysis. (1 source)

### Frequent pattern mining
- [[concepts/frequent-pattern-mining]] — support, closed fragments, contrast patterns. (1 source)
- [[concepts/moss-algorithm]] — search tree, four pruning rules, canonical extension. (1 source)

### Structure diagram generation
- [[concepts/structure-diagram-generation]] — NP-hard 2D layout; IUPAC rules, Shelley score, drawing units. (1 source)
- [[concepts/ring-system-layout]] — decomposition, ring database templates, force-field fallback. (1 source)
- [[concepts/collision-detection-scan-line]] — line-segment intersection by sweep; layout repair operations. (1 source)
- [[concepts/protein-ligand-interaction-diagrams]] — 2D binding-site pictures; convex-hull residue placement. (1 source)

### Molecular surfaces
- [[concepts/lennard-jones-potential]] — the VdW model that defines the atomic radius. (1 source)
- [[concepts/molecular-surfaces]] — VdW / solvent-accessible / molecular surface; patch types. (1 source)
- [[concepts/connolly-surface-algorithm]] — gift-wrapping over the torus-path network. (1 source)
- [[concepts/marching-cubes]] — isosurface from grid data; 15 base patterns. (1 source)
- [[concepts/ball-pivoting-algorithm]] — triangle mesh from a point cloud; edge labels. (1 source)
- [[concepts/kohonen-maps]] — 2D torus projection of a 3D surface for molecule comparison. (1 source)

### Reduced graph descriptors
- [[concepts/reduced-graphs]] — collapsing rings/linkers/features; Gillet's label hierarchy. (1 source)
- [[concepts/feature-trees]] — node-labelled tree descriptor; generation and labels. (1 source)
- [[concepts/feature-tree-comparison]] — topology-preserving matching; split-search and match-search. (1 source)

### Descriptor evaluation
- [[concepts/enrichment-factor]] — how much of a known active class a ranking pulls into the top p%. (1 source)
- [[concepts/roc-curves-and-auc]] — confusion matrix, TPR/FPR, threshold sweep, AUC. (1 source)

### 3D descriptors
- [[concepts/pharmacophore]] — the spatial arrangement of groups required for binding; PPPs. (1 source)
- [[concepts/atom-pair-and-triplet-descriptors]] — binned typed-distance histograms; why 3D often loses to 2D. (1 source)
- [[concepts/ultrafast-shape-recognition]] — alignment-free shape via four reference points. (1 source)
- [[concepts/autocorrelation-vectors]] — property recurrence at each bond distance. (1 source)
- [[concepts/affinity-fingerprints]] — describe a molecule by its affinities to a protein panel. (1 source)

### Clustering
- [[concepts/clustering-of-molecules]] — unsupervised grouping; partitional vs hierarchical. (1 source)
- [[concepts/hierarchical-clustering]] — dendrograms, four linkages, Ward, Lance–Williams. (1 source)
- [[concepts/jarvis-patrick-clustering]] — shared-nearest-neighbour clustering, applied transitively. (1 source)
- [[concepts/k-means-clustering]] — assign/re-average loop; local optimum only. (1 source)

### Molecular superposition
- [[concepts/molecular-superposition]] — the overlay problem for ligands of an unknown target. (1 source)
- [[concepts/gaussian-molecular-representation]] — Gaussians per atom; Carbó and Hodgkin indices. (1 source)
- [[concepts/seal-algorithm]] — rigid superposition by multi-start local optimisation with quaternions. (1 source)
- [[concepts/molecular-conformation]] — constitution vs configuration vs conformation; geometric parameters. (1 source)
- [[concepts/vsepr-model]] — electron-pair repulsion; ideal geometries and their deviations. (1 source)
- [[concepts/conformation-generation]] — CORINA, fragment databases, torsion-angle libraries. (1 source)
- [[concepts/flexible-superposition]] — GASP (genetic algorithm) and FlexS (incremental construction). (1 source)
- [[concepts/rmsd-and-point-set-superposition]] — RMSD, centroid translation, Sippl and Kabsch rotations. (1 source)

### Working with pharmacophores
- [[concepts/pharmacophore-derivation]] — screening workflow, active-analog approach, orientation maps. (1 source)
- [[concepts/disco-algorithm]] — distance-compatibility graph + clique search over conformers. (1 source)
- [[concepts/pharmacophore-matching]] — 3D database searching; the assignment/conformation double problem. (1 source)
- [[concepts/catalyst-algorithm]] — hierarchical conformer scan + atom-for-atom backtracking. (1 source)
- [[concepts/caveat-algorithm]] — binned index over vector pairs (d, t, a₁, a₂); linkers and pharmacophores. (1 source)
- [[concepts/directed-tweak]] — UNITY: torsion angles optimised numerically instead of enumerated. (1 source)
- [[concepts/ligandscout-algorithm]] — maximum bipartite matching + Kabsch, iterated. (1 source)
- [[concepts/pharmer-algorithm]] — KDB-tree index over pharmacophore-point triangles. (1 source)

### QSAR
- [[concepts/qsar]] — quantitative structure–activity relationships; the family of models and the early matrix view. (2 sources)
- [[concepts/physicochemical-parameters]] — Hammett σ, π/logP, MR, MW, Verloop. (1 source)
- [[concepts/lipophilicity-and-logp]] — octanol/water partitioning and the additivity of π. (1 source)
- [[concepts/hansch-analysis]] — global parameters with a quadratic logP term. (1 source)
- [[concepts/free-wilson-analysis]] — substituent indicators; the combined model containing both. (1 source)
- [[concepts/matched-molecular-pairs]] — MMP, MMS, core and context. (1 source)
- [[concepts/matched-molecular-pair-analysis]] — rule mining T → ΔP; four identification algorithms. (1 source)
- [[concepts/qsar-model-validation]] — RSS/MSE/RMSE, r, R², q², Q² and the two pitfalls. (1 source)

### 3D-QSAR and dimensionality reduction
- [[concepts/3d-qsar]] — fields on a grid; inherits the alignment problem. (1 source)
- [[concepts/comfa]] — GRID fields, capping, the variables ≫ observations problem. (1 source)
- [[concepts/comsia]] — Gaussian similarity indices; finite maxima, no capping. (1 source)
- [[concepts/principal-component-analysis]] — maximise variance; ignores the activity. (1 source)
- [[concepts/partial-least-squares]] — maximise correlation with the activity; cross-validated stopping. (1 source)

### Docking
- [[concepts/docking]] — problem statement and the three-axis taxonomy. (1 source)
- [[concepts/scoring-functions]] — force field vs PMF vs empirical; Böhm's function. (1 source)
- [[concepts/dock-algorithm]] — inscribed spheres as a negative image; 4-matchings. (1 source)
- [[concepts/kuhl-algorithm]] — docking graph, Bron–Kerbosch, the "not" set trick. (1 source)
- [[concepts/clix-algorithm]] — interaction map targets; place on 2 points, rotate, score. (1 source)
- [[concepts/geometric-hashing-docking]] — Fischer: triangle hash table + voting scheme. (1 source)

### Flexible docking
- [[concepts/flexible-docking]] — enumerative vs randomised vs combinatorial; when the conformation is decided. (1 source)
- [[concepts/pose-clustering]] — interaction surfaces, triplet hashing, complete-linkage clustering of transformations. (1 source)
- [[concepts/glide-hierarchical-filtering]] — successive filters, greedy score then final scoring. (1 source)
- [[concepts/genetic-algorithm-docking]] — GOLD, DOCK+GA, evolutionary programming with the PLP function. (1 source)
- [[concepts/randomised-docking]] — tabu search (PRO_LEADS), simulated annealing (AutoDock), MCM, MD. (1 source)
- [[concepts/place-and-join]] — DesJarlais overlap atoms; hinge bending as extended geometric hashing. (1 source)
- [[concepts/incremental-construction-docking]] — FlexX build-up loop; backtracking vs greedy. (1 source)

### Binding site detection
- [[concepts/binding-site-detection]] — binding pocket vs active site; the four method families and their failure modes. (1 source)
- [[concepts/ligsite-and-pocket]] — PSP events, burial degree 0–7, threshold ≥ 4. (1 source)
- [[concepts/surfnet]] — gap spheres shrunk until collision-free; overestimates wide pockets. (1 source)
- [[concepts/cast-alpha-shapes]] — Voronoi + alpha shapes + discrete flow; misses funnel-shaped pockets. (1 source)
- [[concepts/pass-algorithm]] — virtual spheres over the whole surface, layers reveal the portal. (1 source)
- [[concepts/drugsite]] — carbon-probe vdW grid, average space filter, contour level, > 100 Å³ clusters. (1 source)
- [[concepts/evolutionary-site-prediction]] — Aloy: MSA, invariant polar residues, mapping and clustering. (1 source)
- [[concepts/binding-site-prediction-evaluation]] — the five criteria and the two benchmark questions. (1 source)

### Druggability
- [[concepts/druggability]] — Cheng's MAPpod, Hajduk's NMR hit rate, Nayal & Honig's SCREEN; pockets are large, deep, rigid, curved. (1 source)

### Library design and de novo design
- [[concepts/combinatorial-libraries]] — CombiLibs, HTS drawbacks, SELECT's diversity/profile fitness. (1 source)
- [[concepts/focused-libraries]] — target-specific libraries; exploiting combinatorial structure for speed. (1 source)
- [[concepts/fragment-based-drug-design]] — weak but efficient binders; SAR by NMR and X-ray. (1 source)
- [[concepts/chemical-space]] — descriptor-bounded space; Lipinski Ro5, Bohacek 10⁶⁰, GDB-17. (1 source)
- [[concepts/fragment-spaces]] — implicit combinatorial spaces; shredding vs constructive, RECAP, BRICS, link types. (1 source)
- [[concepts/fragment-space-search]] — TOPAS, FTrees-FS (double dynamic programming), FlexNovo. (1 source)

### Protein–protein docking
- [[concepts/protein-protein-docking]] — symmetric problem, unknown interface, hot spots, CAPRI results. (1 source)
- [[concepts/katchalski-katzir-algorithm]] — grid encoding, correlation, convolution theorem, O(N_R·N³ log N). (1 source)
- [[concepts/surface-reduction-for-docking]] — sphere world, cylinder projection, PatchDock/FlexDock/FireDock. (1 source)
- [[concepts/monte-carlo-protein-docking]] — RosettaDock and ICM-DISCO; days per complex. (1 source)

## Tools
- [[tools/knime]] — open-source graphical workflow system used for cheminformatics workflows. (2 sources)
- [[tools/pipeline-pilot]] — graphical scientific workflow system for data access, analysis and reporting. (1 source)
- [[tools/azorange]] — Orange/Python-style open-source QSAR analysis environment named in GCI. (1 source)

## Entities
- [[entities/chemical-database-catalog]] — named resources from GCI: PDB, ChEMBL, ZINC, PubChem, BRENDA, DrugBank, SureChEMBL, CSD and search engines. (1 source)

## Exercises
- [[exercises/ciw-e1-thermodynamics-and-hydrogen-bonds]] — computing ΔG/Kᵢ from ΔH/ΔS; hydrogen-bond scoring function. (1 source)
- [[exercises/ciw-e2-vf2-trace]] — hand-execution of VF2 on a 7-atom molecule with a 3-atom query. (1 source)
- [[exercises/ciw-e3-cycle-bases-and-linkers]] — cycle bases, essential vs relevant cycles, linker detection. (1 source)
- [[exercises/ciw-e4-moss-and-surfaces]] — MoSS search-tree trace, KNIME MoSS parameters, ball-pivoting. (1 source)
- [[exercises/ciw-e5-feature-trees]] — match-search traversal order; partitional vs hierarchical clustering. (2 sources)
- [[exercises/ciw-e6-qsar-and-matched-molecular-pairs]] — Free–Wilson regression system, correlation coefficient, LOO vs external q², Hussain & Rea, core/context. (1 source)

- [[exercises/gci-e1-databases-workflows-and-smiles]] — database lookup, KNIME workflow interpretation, file formats and hand SMILES generation. (1 source)
- [[exercises/gci-e2-identifiers-canonicalization-and-smarts]] - InChI layers, Morgan/CANON/GENES canonical ordering and SMARTS pattern interpretation. (1 source)
- [[exercises/gci-e3-stereochemistry-rings-subgraph-and-mcs]] - CIP ordering, ring/bond classification, Ullmann refinement and Bron-Kerbosch traces. (1 source)

## Comparisons
_(none yet)_
