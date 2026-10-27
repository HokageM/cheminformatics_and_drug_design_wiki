---
title: Lead Finding Strategies
type: concept
tags: [lead-discovery, screening, design-cycle]
created: 2026-09-30
updated: 2026-09-30
sources: ["[[sources/ciw-01-drug-action-and-molecular-interactions]]"]
status: developing
---

# Lead Finding Strategies

The five routes to a lead structure, and the design cycle they all feed.

## The design cycle

```mermaid
flowchart LR
    T["Target identification"] --> S["Screening"]
    S --> L["Lead structure"]
    L --> B["Biological testing"]
    B --> Q["QSAR → computer-aided design"]
    Q --> D["Experimental design"]
    D --> Y["Synthesis"]
    Y --> B
    B --> C["Candidates for further development"]
```
*Lead finding is a loop: design → synthesis → biological testing → QSAR → design.*

## The five strategies

| Strategy | Requires | Computational role |
|---|---|---|
| **Traditional design** | known activities, biology labs | minimal |
| **Screening** | cell/protein assay, robotics | data analysis |
| **Virtual screening** | 3D structure of the target, computers | docking, scoring |
| **Similarity searching** | known activities, computers | QSAR |
| **De novo design** | 3D structure of the target, computers | fragment assembly |

All of them are followed by **experimental validation** and then **lead optimisation**.

### Traditional design

- Successive modification / optimisation of known active compounds.
- Sources of initial active compounds:
  - constituents of plants
  - animal poisons and active substances
  - active substances from microorganisms

### (High-throughput) screening

See [[concepts/high-throughput-screening]].

### Virtual screening

See [[concepts/virtual-screening]].

### De novo design

See [[concepts/de-novo-design]].

## Current strategy in practice

```mermaid
flowchart TD
    VS["Virtual screening"] --> SEL["Selection of molecules<br/>focused combinatorial libraries"]
    SIM["Similarity searching"] --> SEL
    DN["De novo design"] --> SEL
    SEL --> ASSAY["Known activities (labs) · cell/protein assay (robotics)"]
    ASSAY --> EV["Experimental validation"]
    EV --> LO["Lead optimisation<br/>optimise ADME-Tox · reduce off-targets"]
    LO -->|"new input"| VS
```
*The three computational strategies feed a focused library, which is validated experimentally and then optimised.*

## See also

- [[concepts/virtual-screening]]
- [[concepts/de-novo-design]]
- [[concepts/high-throughput-screening]]
- [[concepts/drug-discovery-pipeline]]
- [[concepts/lead-optimization-heuristics]]

## Sources

- [[sources/ciw-01-drug-action-and-molecular-interactions]] (pp. 18–19)
