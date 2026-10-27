---
title: Synthesis
type: meta
tags: [meta, thesis]
created: 2026-09-30
updated: 2026-10-19
status: developing
---

# Synthesis

The evolving big-picture argument: how the methods in this module fit together, where they
agree, where they trade off, and what the module as a whole is teaching.

## Current thesis

*(after lecture 1)*

Computational drug design is the attempt to **predict a free energy difference from a
structure**. Everything else follows from how badly that problem is posed:

1. **The target is a moving object.** Proteins have flexibility at six levels
   ([[concepts/protein-flexibility]]), so a single crystal structure is already a lossy model.
2. **Water is a participant, not a background.** Every protein–ligand contact must out-compete
   a water contact, so affinity is a *balance sheet*, not a sum
   ([[concepts/desolvation-and-water]]).
3. **Enthalpy and entropy compensate.** Any modification that gains enthalpy usually loses
   entropy, so interaction counting predicts nothing
   ([[concepts/enthalpy-entropy-compensation]]). The tyrosyl-tRNA-synthetase example shows
   two chemically similar edits differing by three orders of magnitude in Kᵢ.
4. **Therefore design is heuristic, and every heuristic has a caveat**
   ([[concepts/lead-optimization-heuristics]]).
5. **And affinity is not even the hard part** — most candidates die on ADMET
   ([[concepts/admet]]), which is a different, weakly structure-determined prediction problem.

This is why the field has five parallel lead-finding strategies rather than one
([[concepts/lead-finding-strategies]]): none of them is reliable enough to be used alone,
and all of them terminate in experimental validation.

*(after lecture 2)*

A second, independent theme appears: **before you can compute anything about a molecule, you
must first decide what a molecule *is* algorithmically.** Lecture 2 shows that even the
apparently trivial question "how many rings does this molecule have?" has no single answer.

6. **The basic operations are NP-complete.** Substructure search is subgraph isomorphism
   ([[concepts/subgraph-isomorphism]]); practical speed comes entirely from pruning
   ([[concepts/vf2-algorithm]]), not from better asymptotics.
7. **Chemical intuition and graph theory disagree.** The cyclomatic number says a cube has 5
   rings; a chemist says 6 ([[concepts/cycle-space-and-cycle-basis]]).
8. **Each ring concept trades one requirement for another** — all rings (exponential), SSSR
   (ambiguous), relevant cycles (unique but exponential), URFs (all five)
   ([[concepts/ring-perception]]). The field converged on URFs only after three failed
   attempts, which is the same pattern as the failed additivity assumption in lecture 1.

The unifying claim so far: **cheminformatics is a discipline of principled approximations.**
Both the physics (free energy) and the discrete mathematics (ring perception, isomorphism)
are intractable in the exact form, so the real content of the field is knowing *which*
approximation fails *where*.

*(after lecture 3)*

Lecture 3 supplies the mechanism by which the approximations are made, and it is the same
one three times over: **replace the exact object by a coarser one that can be enumerated,
then repair the damage locally.**

9. **Pattern mining** cannot enumerate all substructures, so it enumerates a *search tree*
   and prunes it ([[concepts/moss-algorithm]]). The soundness of the whole method rests on
   one monotonicity fact — support falls down the tree — and the lecture is careful to note
   that the *negative* support does not have it, so it cannot prune.
10. **Structure diagram generation** is NP-hard, so it does not optimise a layout; it places
    atoms greedily by a heuristic score, then *detects and repairs collisions*
    ([[concepts/structure-diagram-generation]], [[concepts/collision-detection-scan-line]]).
11. **Molecular surfaces** replace a quantum-mechanical electron density by hard spheres of
    van der Waals radius, and then *repair* the resulting unphysical crevices by rolling a
    probe over them ([[concepts/molecular-surfaces]]). The repair even needs its own repair:
    cusp trimming.
12. **Descriptors** replace the molecular graph by a reduced graph or a feature tree, giving
    up exact subgraph matching in exchange for a graded, computable similarity
    ([[concepts/reduced-graphs]], [[concepts/feature-tree-comparison]]).

Two observations tie lectures 1–3 together.

First, **the lecture-2 graph machinery is infrastructure, not an end in itself.** Biconnected
components reappear in ring-system layout and in feature-tree construction; the SSSR
reappears as the node definition of a reduced graph. Ring perception was never about rings —
it was about having a canonical decomposition to build everything else on.

Second, **the surface is where the algorithms meet the thermodynamics.** Lecture 1 said
binding is a free-energy difference dominated by desolvation and the hydrophobic effect,
both of which are *area* terms ([[concepts/hydrophobic-effect]],
[[concepts/desolvation-and-water]]). Lecture 3 finally defines that area precisely enough to
compute it. The chain
*Lennard-Jones potential → VdW radius → molecular surface → buried area → ΔG contribution*
is the first complete path in this wiki from a physical model to a number a scoring function
can use.

*(after lecture 4)*

Lecture 4 is the first one that turns the tools back on themselves: it asks not "how do I
compute a descriptor?" but **"how do I know whether a descriptor is any good?"** — and the
answer is uncomfortable.

13. **Validation precedes sophistication.** Enrichment factors and ROC/AUC
    ([[concepts/enrichment-factor]], [[concepts/roc-curves-and-auc]]) exist because a
    virtual screen is only ever a *ranking*; nothing in the method itself tells you whether
    the ranking is better than chance. Every method in lectures 2–3 is only as good as its
    score on this one benchmark.
14. **More physics does not imply more performance.** The explicit finding that 3D
    atom-triplet descriptors often *underperform* 2D topological ones
    ([[concepts/atom-pair-and-triplet-descriptors]]) inverts the assumption running through
    lectures 1–3. The reason is conformational: a 3D descriptor is a descriptor of *one
    conformer*, and the bioactive conformer is unknown ([[concepts/molecular-conformation]]).
    The 2D graph is at least unambiguous.
15. **Alignment-free beats alignment where alignment is the bottleneck.** USR
    ([[concepts/ultrafast-shape-recognition]]) and autocorrelation vectors
    ([[concepts/autocorrelation-vectors]]) get 3D-ish information without solving the
    superposition problem at all — the same move as feature trees in lecture 3, one
    dimension up.
16. **Clustering is the "which approximation fails where" question again.** Partitional
    methods need `k` in advance, hierarchical methods do not scale, Jarvis–Patrick needs two
    arbitrary constants ([[concepts/clustering-of-molecules]]). There is no default.
17. **Superposition is docking without a protein.** SEAL, GASP and FlexS
    ([[concepts/seal-algorithm]], [[concepts/flexible-superposition]]) use exactly the
    machinery lecture 1 predicted would be needed — Gaussian-smoothed shape, multi-start
    optimisation, incremental construction over rotatable bonds — but against a ligand
    ensemble instead of a binding site. The pharmacophore ([[concepts/pharmacophore]]) is
    the inferred negative image of the site.
18. **Only the last step is exact.** Point-set superposition
    ([[concepts/rmsd-and-point-set-superposition]]) is the single problem in the whole course
    with a closed-form optimal solution (Kabsch). Everything upstream of it — which points
    to match, which conformer, which descriptor — is heuristic. That asymmetry is the most
    honest summary of the field so far.

The through-line from lecture 1 now closes a loop: lecture 1 said binding is a free-energy
difference we cannot compute; lectures 2–3 built computable proxies; lecture 4 supplies both
the metric that tells you how badly the proxies do and the first evidence that adding
realism to a proxy can make it worse.

*(after lecture 5)*

Lecture 5 is where the wiki stops accumulating new ideas and starts revealing that the
existing ones were the same idea all along.

19. **One graph construction solves three unrelated-looking problems.** DISCO derives a
    pharmacophore, DOCK places a ligand, Kuhl formalises docking — and all three build a
    *distance-compatibility graph* whose cliques are the answer
    ([[concepts/disco-algorithm]], [[concepts/dock-algorithm]],
    [[concepts/kuhl-algorithm]]). The justification is always the same one sentence: rigid
    motions preserve distances, so mutual distance-compatibility is exactly the condition
    for a set of correspondences to be simultaneously realisable.
20. **Every method faces the same fork: index or optimise.** Pre-enumerate conformers and
    index them ([[concepts/caveat-algorithm]], [[concepts/pharmer-algorithm]],
    [[concepts/geometric-hashing-docking]]) or generate geometry on demand by numerical
    optimisation ([[concepts/directed-tweak]]). Neither wins; they trade storage against
    query time.
21. **Scoring functions are QSAR.** The lecture says this outright
    ([[concepts/scoring-functions]]): an empirical scoring function is a regression of
    geometric descriptors against measured ΔG. Böhm's five terms map one-to-one onto the
    interaction types of lecture 1, which means the structure-based and ligand-based tracks
    were never really separate — they use the same statistics on different features.
22. **The additivity assumption refuses to die.** logP is additive over groups
    ([[concepts/lipophilicity-and-logp]]), Free–Wilson is additive over substituents
    ([[concepts/free-wilson-analysis]]), CoMFA is additive over grid points
    ([[concepts/comfa]]), and Böhm is additive over interaction types. Lecture 1 proved it
    false for binding free energies. It survives because where it fails — cooperativity at
    a binding site — is precisely where none of these models look.
23. **Unsupervised reduction throws away the signal.** PCA keeps the directions of largest
    variance, which need not be the directions that explain activity; PLS fixes this by
    looking at the target ([[concepts/principal-component-analysis]],
    [[concepts/partial-least-squares]]). This is the same lesson as claim 14 from lecture 4:
    more information in the representation is not the same as more *relevant* information.
24. **Validation is adversarial, not decorative.** The lecture gives two explicit ways q²
    lies — similar molecules on both sides of the split, and selecting the model on the very
    statistic you then report ([[concepts/qsar-model-validation]]). The second indicts PLS
    directly, since PLS chooses its dimension by cross-validated q².
25. **Predicting differences is easier than predicting values.** Matched molecular pairs
    ([[concepts/matched-molecular-pairs]]) abandon the absolute-value regression entirely.
    Systematic errors cancel, the output is a human-readable rule, and the price is that the
    method only speaks about transformations it has seen — the same closed-vocabulary
    limitation as Free–Wilson, arrived at from the opposite direction.

The arc of the course is now visible. Lecture 1 posed an intractable physical question;
lectures 2–3 built discrete proxies; lecture 4 supplied the metrics and the first
disappointment; lecture 5 shows the proxies converging — on one graph algorithm, one
regression, one additivity assumption — and hands the problem to docking, where the protein
structure finally returns and the whole apparatus gets a real target to aim at.

*(after lecture 6)*

26. **Docking is a sampling problem disguised as a scoring problem, and lecture 6 is the
    admission that sampling cannot be done exhaustively.** Every method on pages 1–7 is a
    way of *not* enumerating the conformation space:
    [[concepts/randomised-docking|randomised methods]] sample it,
    [[concepts/genetic-algorithm-docking|genetic algorithms]] evolve within it,
    [[concepts/place-and-join]] factorises it, and
    [[concepts/incremental-construction-docking|incremental construction]] never builds the
    parts that already fail. The fact that four unrelated strategies were needed is itself
    the finding: there is no good one.

27. **Whenever the search space cannot be pruned, prune the *survivors* instead.**
    [[concepts/pose-clustering]] clusters transformations, incremental construction clusters
    partial solutions, [[concepts/monte-carlo-protein-docking|RosettaDock]] clusters final
    poses, and [[concepts/glide-hierarchical-filtering|GLIDE]] filters between every stage.
    Clustering, introduced in lecture 4 as a way of organising compound collections
    ([[concepts/clustering-of-molecules]]), has quietly become the universal population
    control of structure-based methods.

28. **The course has been assuming its own conclusion.** Lectures 1–5 all presuppose a known
    binding site; [[concepts/binding-site-detection]] removes that assumption and the field
    fragments immediately into geometry, energy and evolution — three families that do not
    agree, with accuracies from 8 % to 74 %. The lesson is in the failure modes:
    [[concepts/ligsite-and-pocket|grids]] depend on orientation,
    [[concepts/surfnet|spheres]] overestimate wide pockets,
    [[concepts/cast-alpha-shapes|Voronoi]] misses funnels,
    [[concepts/drugsite|energy]] depends on the force field. Each method encodes one
    intuition about what a pocket *is*, and active sites are too variable for any one of
    them.

29. **Druggability is where cheminformatics finally admits it cannot fix everything.** The
    SCREEN result that **pocket volume does not correlate with ligand volume** quietly
    destroys the shape-complementarity intuition that motivated
    [[concepts/dock-algorithm|DOCK's]] negative image and
    [[concepts/molecular-surfaces|surface matching]]: drugs do not fill their pockets. What
    they do is bury a large hydrophobic surface — which returns the argument to the
    [[concepts/hydrophobic-effect]] and [[concepts/desolvation-and-water]] of lecture 1, now
    as a *selection criterion for targets* rather than an explanation of affinity.

30. **The central intellectual move of the lecture is replacing an explicit set by an
    implicit one.** [[concepts/chemical-space]] has > 10⁶⁰ members and cannot be enumerated;
    a [[concepts/fragment-spaces|fragment space]] stores a comparably large set as a few
    thousand fragments plus connection rules, and solves synthetic accessibility *by
    construction* rather than by filtering afterwards. This is the same compression that
    [[concepts/reduced-graphs]] applied to single molecules, lifted to whole collections —
    and it is no coincidence that [[concepts/fragment-space-search|FTrees-FS]] searches
    fragment spaces with exactly the reduced-graph machinery of lecture 3. The abstraction
    is compositional, so it survives being applied to an implicit set.

31. **Every lecture-6 method is a rearrangement of lecture 2–5 machinery, not new
    mathematics.** Hinge bending extends [[concepts/geometric-hashing-docking|geometric
    hashing]]; PatchDock uses geometric hashing plus pose clustering; pose clustering is
    complete-linkage [[concepts/hierarchical-clustering]] on an
    [[concepts/rmsd-and-point-set-superposition|RMSD]] metric; Hajduk's druggability score
    is a [[concepts/qsar]] model with hit rate as the dependent variable; SCREEN is a random
    forest over surface descriptors. The field's toolbox turns out to be small, and the
    skill is in recognising which problem has which shape.

32. **[[concepts/katchalski-katzir-algorithm|Katchalski-Katzir]] is the one genuinely new
    idea, and it is imported from signal processing.** Encoding "surface = 1, core = large
    negative" makes contact and interpenetration a single product, and the convolution
    theorem then evaluates every translation simultaneously, cutting O(n⁶) to
    O(N_R·N³ log N). It is the clearest example in the course of the general principle that
    a *change of representation*, not a better search, is what buys an order of magnitude —
    the same principle as cycle space over GF(2) in lecture 2.

33. **The CAPRI results close the course honestly.** ~50 % success, good on
    enzyme–inhibitor complexes, very poor on transient and antigen–antibody complexes — i.e.
    the methods work exactly where their assumptions (rigid backbone, tight shape
    complementarity, preformed interface) happen to hold, and fail where binding involves
    conformational change. [[concepts/protein-flexibility]], flagged as unsolved in lecture
    1, is still unsolved 28 pages later, and it is the single limitation that all six
    lectures share.

*(after GCI foundation part 1)*

34. **The course now has its missing layer zero: representation and infrastructure.** GCI part 1 explains how later algorithms get input: chemical databases, file formats, workflow systems and line notations. Before subgraph isomorphism, ring perception or QSAR can run, molecules must be curated, standardised and represented as labelled graphs ([[concepts/molecular-graphs]], [[concepts/molecular-file-formats]], [[concepts/smiles]]).
35. **Cheminformatics is inductive learning with chemical syntax attached.** The foundation loop — experiment -> data -> model -> prediction is exactly the pattern later repeated by QSAR, scoring functions and virtual screening ([[concepts/cheminformatics]], [[concepts/qsar]]).
36. **SMILES makes the graph-theory theme visible at the syntax level.** DFS, back edges and branch stacks are no longer only theoretical graph algorithms; they print the molecule as a string ([[concepts/smiles-generation]]).

*(after GCI foundation part 2)*

37. **Representation becomes identity only after canonicalisation.** GCI part 1 showed that a molecule can be written as SMILES; part 2 shows why this is not enough. The same graph has many traversals, so identifiers require canonical atom ordering ([[concepts/molecular-canonicalization]], [[concepts/morgan-canonicalization]]) or a layered standard identifier ([[concepts/inchi-and-inchikey]]).
38. **The same syntax family splits into three roles.** [[concepts/smiles]] describes one molecule, [[concepts/canon-smiles-algorithm|unique SMILES]] describes one molecule deterministically, and [[concepts/smarts]] describes a set of substructures. Confusing these roles is a category error: identity, serialisation and query are different operations on the same graph.
39. **Canonicalisation is another approximation boundary.** Morgan, CANON and GENES reduce a graph symmetry problem to ranks, products, tie-breaking and traversal rules. Like ring perception, the output is only unique relative to the rule system, which is why toolkit-specific canonical SMILES should not be treated as a universal chemical truth.

*(after GCI foundation part 3)*

40. **Stereochemistry is not an exception to the graph story; it is another traversal problem.** CIP priorities look chemical, but GCI part 3 implements them as substituent trees with duplicate atoms for multiple bonds and rings ([[concepts/cip-sequence-rules]]). The same move as canonical SMILES appears again: define a deterministic graph procedure, then attach chemical semantics to its output.
41. **Ring perception now has a local/global split.** [[concepts/smallest-ring-search]] answers a local question with BFS, while [[concepts/biconnected-components-and-acyclic-bonds]] answers the global ring-versus-chain question with low-link DFS. This clarifies why SMARTS-style local ring predicates, rotatable-bond definitions and full ring bases are related but not interchangeable.
42. **The clique reduction is the recurring graph-algorithm skeleton.** GCI part 3 shows MCS as [[concepts/modular-product-graph]] plus [[concepts/bron-kerbosch-algorithm]], which retroactively connects substructure search, pharmacophore matching and docking clique methods. The field repeatedly solves chemical matching by building a compatibility graph and asking for a clique.

*(after GCI foundation part 4)*

43. **The complete GCI series now forms a representation ladder.** Part 1 defines molecules as database records and graphs; part 2 makes those graphs canonical and queryable; part 3 runs exact graph algorithms over them; part 4 deliberately abandons exactness for [[concepts/molecular-descriptors]], [[concepts/molecular-fingerprints]] and [[concepts/similarity-and-distance-measures]]. The ladder is not a replacement sequence: exact identity, substructure matching and approximate similarity answer different questions.
44. **Similarity is the practical answer to ignorance about the protein.** If the target structure and relevant binding groups are known, docking or pharmacophore matching can be attempted. If they are not, [[concepts/molecular-similarity]] says only that similar physico-chemical descriptions tend statistically to preserve binding. This closes the foundation arc by connecting representation directly back to [[concepts/protein-ligand-binding]].
45. **Hashing is the canonicalisation trade-off turned inside out.** Parts 2-3 sought deterministic graph descriptions; part 4 uses Daylight and [[concepts/ecfp-and-fcfp-fingerprints]] to intentionally collapse many features into fixed-length vectors. Collisions and non-invertibility are accepted because the goal is not chemical identity but fast ranking and filtering. The same Morgan-style neighbourhood growth appears first as canonical ordering and then as circular feature generation.

## Tensions and trade-offs

| Axis | Pull | Counter-pull |
|---|---|---|
| Lipophilic surface | more potency | less solubility |
| Hydrogen bonds | more enthalpy | desolvation cost, compensation |
| Ligand rigidity | less entropy loss on binding | harder synthesis, narrower SAR |
| Model detail (flexibility, solvent) | more accuracy | combinatorial cost |

## See also

- [[overview]]
- [[open-questions]]
