---
title: "3D-QSAR"
type: concept
tags: [qsar, 3d, field, superposition]
created: 2026-09-30
updated: 2026-09-30
sources: ["[[sources/ciw-05-pharmacophores-qsar-and-docking]]"]
status: solid
---

# 3D-QSAR

QSAR that takes the **3D structure** of the molecules into account when deriving the model.

## Why it matters

2D QSAR correlates activity with numbers attached to a formula. 3D-QSAR correlates it with
numbers attached to *positions in space*, which means the model can be visualised as
regions around the ligands where more (or less) of a given property helps. That turns a
regression into a design hypothesis.

## The problem

```text
PROBLEM:
  → conformations and relative orientations are UNKNOWN
  → need a description of common 3D properties
```

Both halves of the problem come straight from lecture 4: the bioactive conformer is unknown
([[concepts/molecular-conformation]]) and the relative orientation has to be produced by
[[concepts/molecular-superposition]]. 3D-QSAR therefore *inherits* every uncertainty of
those steps before it computes anything.

```mermaid
flowchart LR
    M["Set of actives"] --> C["Conformation generation"]
    C --> S["Molecular superposition"]
    S --> G["Embed in 3D grid"]
    G --> F["Compute fields at grid points"]
    F --> R["Regress field values<br/>against activity"]
    R --> V["Visualise significant regions"]
```
*Every arrow before the regression is itself an unsolved problem — which is why 3D-QSAR results are so sensitive to the alignment.*

## The two methods

| Method | Compares | Page |
|---|---|---|
| **CoMFA** | molecular **fields** (steric, electrostatic, hydrophobic) | [[concepts/comfa]] |
| **CoMSIA** | local molecular **similarities** | [[concepts/comsia]] |

The general model form is

```text
log 1/C  =   Σ        Σ            a_{f,x,y,z} · f(x,y,z)   +  a
          field f  grid point x,y,z
```

so a "descriptor" is now one field type at one grid point — of which there are tens of
thousands. This immediately creates the defining difficulty of 3D-QSAR:

> **# free variables ≫ # biological data**

resolved by [[concepts/principal-component-analysis]] and
[[concepts/partial-least-squares]].

## Application of a 3D-QSAR model

```text
PREDICTION OF BINDING AFFINITIES:
    1. superimpose the unknown molecule onto the molecules of the model
    2. compute the fields for the unknown molecule
    3. insert the field values into the model

GRAPHICAL EVALUATION (visualisation of the model):
    - after the regression, each grid point carries a significance value a_{f,x,y,z}
    - for each field, regions with high a-values can be visualised
```

The visualisation is the payoff: contoured regions saying "add bulk here", "add negative
charge there" are directly actionable in [[concepts/lead-optimization-heuristics]].

## Caveats

- The model is only defined for molecules that can be superimposed onto the training set —
  a new scaffold may simply have no valid alignment.
- Results depend strongly on the chosen alignment; a different superposition gives a
  different model.
- Prerequisite (from CoMFA): the molecules must bind **competitively to the same target**.

## See also

- [[concepts/comfa]]
- [[concepts/comsia]]
- [[concepts/qsar]]
- [[concepts/molecular-superposition]]
- [[concepts/partial-least-squares]]

## Sources

- [[sources/ciw-05-pharmacophores-qsar-and-docking]] (pp. 18, 22)
