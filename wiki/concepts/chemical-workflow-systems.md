---
title: Chemical Workflow Systems
type: concept
tags: [workflow, automation, qsar]
created: 2026-10-19
updated: 2026-10-19
sources: ["[[sources/gci-01-foundations-of-cheminformatics]]"]
status: developing
---

# Chemical Workflow Systems

Chemical workflow systems chain reusable processing nodes so cheminformatics data can be imported, cleaned, transformed, modelled and reported reproducibly.

## Why it matters

GCI treats automation as necessary because cheminformatics works with large data volumes and repeated preprocessing steps.

## How it works

```text
PROCEDURE QSARWorkflow(database DB)
  INPUT : molecules with measured activities
  OUTPUT: maintained predictive model

  records <- read DB
  records <- normalise structures and remove duplicates
  records <- filter by assay, structure validity and property range
  descriptors <- calculate molecular descriptors
  model <- develop QSAR model
  predictions <- predict untested molecules
  maintain model as new data arrive
```

```mermaid
flowchart LR
    DB["Database"] --> N["Normalise"]
    N --> D["Remove duplicates"]
    D --> F["Filter"]
    F --> C["Descriptor calculation"]
    C --> M["Model development"]
    M --> P["Prediction"]
    P --> U["Model maintenance"]
    U --> M
```
*The GCI QSAR workflow is a cyclic data-cleaning, modelling and maintenance process.*

## Practical notes

- Pipeline Pilot: graphical workflow system for scientific data services.
- KNIME: open-source graphical workflow system similar to Pipeline Pilot.
- AZOrange: Orange/Python-rooted tool for data analysis, visualisation and QSAR analysis.

## Limitations / caveats

- Workflow systems make processing reproducible, but bad standardisation rules or filters still propagate.

## See also

- [[tools/pipeline-pilot]]
- [[tools/knime]]
- [[tools/azorange]]
- [[concepts/qsar]]

## Sources

- [[sources/gci-01-foundations-of-cheminformatics]] (p. 6)
