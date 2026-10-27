---
title: "Exercise 6 — QSAR and Matched Molecular Pairs"
type: exercise
tags: [exercise, ciw-e6, qsar, mmp, validation]
created: 2026-09-30
updated: 2026-09-30
sources: ["[[sources/ciw-05-pharmacophores-qsar-and-docking]]"]
status: solid
---

# Exercise 6 — QSAR and Matched Molecular Pairs

Sheet "CiW – Ex 6". In the scan the tasks appear out of order: 6-2 on pp. 11–12, 6-1 on
pp. 13–14. They are presented here in numeric order.

## Task 6-1 — QSAR

### 1a) Set up the regression system

A Free–Wilson style system `X · b = a`, where the rows of X are molecules, the columns are
indicator variables for each substituent at each substitution site, b is the vector of
substituent contributions, and a holds the measured activities.

```text
        s11 ... s15 | s21 ... s25              b            a
      ( 0 0 0 0 0   |  0  0 0 0 0 )         ( a_1 )      ( 7.46 )
      ( 0 0 0 0 0   | -1  0 0 0 0 )   ×     (  :  )  =   ( 8.16 )
      ( 0 0 0 0 0   |  0  0 1 0 0 )         ( a_9 )      (  :   )
```

Each row has exactly one 1 per substitution site — the indicator δ_ij of
[[concepts/free-wilson-analysis]].

### 1b) Correlation coefficient

> A numerical value that indicates how closely two variables are related to each other,
> in [−1, 1].

| Value | Meaning |
|---|---|
| 0 | no linear relation |
| 0.5 | moderate linear relation: one increases, the other also |
| 1 | perfect linear relation |
| −1 | one increases, the other decreases |

### 1c) Interpretation

A correlation coefficient of **0.94 is high** → high fit to the **training data**.
(Note the hedge: fit to the training data, not predictive power —
[[concepts/qsar-model-validation]].)

### 1d) Meaning of the coefficients of the independent variables

They represent the **quantitative contribution of each component to the activity**.

### 2) Leave-one-out cross validation

```text
Take one data point into the test set, the rest is the training set. Repeat.
Used to assess the PERFORMANCE and GENERALISATION ABILITY of a predictive model.
```

### 3) What does the LOO q² tell us about a model?

```text
q² > 0   = good
q² = 0   = not better than random
```

### 4) LOO q² vs external q²

| | Definition |
|---|---|
| **LOO q²** | calculated during leave-one-out cross-validation |
| **external q²** | uses an independent dataset that was not used during training |

| LOO q² | ext q² | verdict |
|---|---|---|
| high | high | model is good and reliable for new data |
| high | low | **overfitting** the training data |
| low | low | bad |

→ [[concepts/qsar-model-validation]]

## Task 6-2 — Matched Molecular Pairs

### 1) QSAR vs MMPA

**QSAR:** on the basis of many data, determine and describe the relationship between
chemical structure and biological effect.

**MMPA:** work on a set of molecule pairs (A,B) that differ by the same transformation T;
analyse the change of a property ΔP over all molecule pairs (A,B); if statistically
relevant, derive a rule `T → ΔP`.

**Advantages of MMPA:**
- easily interpretable, learning from experience;
- prediction of a property difference is easier than prediction of the absolute value of a
  property.

→ [[concepts/matched-molecular-pairs]], [[concepts/matched-molecular-pair-analysis]]

### 2) Hussain and Rea

```text
1) Take all input molecules and enumerate all acyclic cuts
2) Index those cuts, saving (key, value) pairs, where the KEY is one side
   of the cut and the VALUE are all possible other sides of the cut
3) Derive a transformation
```

### 3) Derive a transformation

From two molecules sharing a key, the pair of values is the transformation, e.g.
`−[△] >> −[○]` supported by MolA and MolB.

### 4) Core and context

| Term | Definition |
|---|---|
| **core** | the common structural component shared by MMPs |
| **context** | the surroundings around / variations around the core |

→ **Equal for both!** (both members of the pair share the same core and the same context)

## See also

- [[concepts/qsar]]
- [[concepts/free-wilson-analysis]]
- [[concepts/qsar-model-validation]]
- [[concepts/matched-molecular-pairs]]
- [[concepts/matched-molecular-pair-analysis]]

## Sources

- [[sources/ciw-05-pharmacophores-qsar-and-docking]] (pp. 11–14)
