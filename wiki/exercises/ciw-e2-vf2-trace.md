---
title: Exercise E2 — VF2 Trace
type: exercise
tags: [exercise, vf2, substructure-search]
created: 2026-09-30
updated: 2026-09-30
sources: ["[[sources/ciw-02-substructure-search-and-ring-perception]]"]
status: developing
---

# Exercise E2 — VF2 Trace

Hand-execution of the [[concepts/vf2-algorithm]] on a small molecule pair (task 2-3).

## Setup

- **Graph G₁**: a 7-atom molecule — chain `1–O(2)–C(3, bearing NH₂ at 5)–O(4)–C(6)–C(7)`
  (numbering as drawn in the notes).
- **Subgraph G₂**: `HO(1)–C(2)–C(3)` — a 3-atom query.

Data structures tracked at every recursion depth `k`:
`core1`, `core2` (the mapping), `out1`, `out2` (membership + depth), `M`, `T₁`, `T₂`, `P(S)`.

## Trace

### k = 0

```text
core2 = [0,0,0]              out2 = [0,0,0]
core1 = [0,0,0,0,0,0,0]      out1 = [0,0,0,0,0,0,0]
M = ∅        T2 = V2      T1 = V1
P(S) = {(1,1),(2,1),(3,1),(4,1),(5,1),(6,1),(7,1)}
```

| Candidate | Result |
|---|---|
| (1,1) | not feasible: `R_sem` false due to label |
| (2,1) | `R_adj = 1 ∧ R_match = 1 ∧ R_next = 1 ∧ R_sem = 1` ⇒ **feasible** |
| (3,1) | not feasible: `R_sem` false due to label |
| (4,1) | `R_adj = 1 ∧ R_match = 1 ∧ R_next = 1 ∧ R_sem = 1` ⇒ **feasible** |
| (5,1) | not feasible: `R_sem = 0` |
| (6,1) | not feasible: `R_sem = 0` |
| (7,1) | not feasible: `R_sem = 0` |

### k = 1 (branch M = {(2,1)})

```text
core2 = [2,0,0]              out2 = [1,1,0]
core1 = [0,1,0,0,0,0,0]      out1 = [1,1,1,0,0,0,0]
M = {(2,1)}   T2 = {2}   T1 = {1,3}
P(S) = {(1,2),(3,2)}     N2 = {3}   N1 = {4,5,6,7}
```

| Candidate | Result |
|---|---|
| (1,2) | `R_sem = 1 ∧ R_adj = 1 ∧ R_next = 0 ∧ R_match = 1` ⇒ pruned by 2-look-ahead |
| (3,2) | `R_sem = 1 ∧ R_adj = 1 ∧ R_next = 1 ∧ R_match = 1` ⇒ **feasible** |

### k = 2

```text
core2 = [2,3,0]              out2 = [1,1,2]
core1 = [0,1,2,0,0,0,0]      out1 = [1,1,1,2,2,0,0]
M = {(1,2),(3,2)}   T2 = {3}   T1 = {1,4,5}
P(S) = {(1,3),(4,3),(5,3)}
```

| Candidate | Result |
|---|---|
| (1,3) | `R_sem = 1 ∧ R_adj = 1 ∧ R_next = 1 ∧ R_match = 0` ⇒ pruned |
| (4,3) | `R_sem = 0` |
| (5,3) | `R_sem = 0` |

⇒ dead end, backtrack.

### Second branch, k = 1 with M = {(4,1)}

```text
core2 = [4,0,0]              out2 = [1,1,0]
core1 = [0,0,0,1,0,0,0]      out1 = [0,0,1,1,0,1,0]
M = {(4,1)}    T2 = {2}   T1 = {3,6}
(3,2) → feasible ;  (6,2) → feasible
```

### k = 2 (branch M = {(4,1),(3,1)})

```text
core2 = [4,3,0]              out2 = [1,1,2]
core1 = [0,0,2,1,0,0,0]      out1 = [0,2,1,1,2,1,0]
M = {(4,1),(3,1)}   T2 = {3}   T1 = {2,5,6}
P(S) = {(2,3),(5,3),(6,3)}
```

| Candidate | Result |
|---|---|
| (2,3) | not same label |
| (5,3) | not same label |
| (6,3) | `R_match = 0` |

### k = 2 (branch M = {(4,1),(6,2)}) — the successful one

```text
core2 = [4,6,0]   out2 = [1,1,2]
M = {(4,1),(6,2)}   T2 = {3}   T1 = {3,7}
candidates {(3,3),(7,3)}:
    (3,3) → R_match fails
    (7,3) → MATCH
k = 3:  core2 = [4,6,7]   M = {(4,1),(6,2),(7,3)}      ⇒ complete matching
```

## What this exercise teaches

- `R_sem` (label compatibility) rejects most candidates immediately and cheaply — it should
  be evaluated first in practice.
- `R_next` (2-look-ahead) is what prunes the `(1,2)` branch that `R_adj` alone would allow;
  this is the concrete value of the look-ahead strategy.
- The importance of `Restore-State`: the arrays `core1/core2/out1/out2` are mutated in place
  and must be rolled back on backtracking (O(n) memory, see
  [[concepts/vf2-algorithm]] § Data structures).

## See also

- [[concepts/vf2-algorithm]]
- [[concepts/subgraph-isomorphism]]

## Sources

- [[sources/ciw-02-substructure-search-and-ring-perception]] (pp. 7–8)
