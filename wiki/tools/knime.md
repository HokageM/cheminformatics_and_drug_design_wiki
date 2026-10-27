---
title: KNIME
type: tool
tags: [workflow, cheminformatics, open-source]
created: 2026-10-19
updated: 2026-10-19
sources: ["[[sources/gci-01-foundations-of-cheminformatics]]", "[[sources/ciw-03-pattern-mining-diagrams-surfaces-and-reduced-graphs]]"]
status: developing
---

# KNIME

KNIME is an open-source graphical workflow system used in the course for cheminformatics workflows.

## Why it matters

It gives a node-based way to reproduce database import, filtering, descriptor calculation and pattern-mining workflows.

## How it works

```text
PROCEDURE KNIMEWorkflow(nodes, table)
  INPUT : ordered workflow graph and input table
  OUTPUT: final table or report

  for each executable node in topological order:
      output[node] <- apply node to input tables
  return selected output table
```

```mermaid
flowchart LR
    R["Reader"] --> S["RDKit Mol"]
    S --> A["Rule engine / shuffle"]
    A --> Split["Row splitter"]
    Split --> Join["Joiner"]
    Join --> W["Writer"]
```
*The GCI exercise sketches a KNIME workflow with readers, converters, rule engines, splitters, joiners and writers.*

## Practical notes

- GCI mentions DrugBank, PubChem, PDB and BRENDA tasks plus a KNIME workflow.
- CIW exercise E4 uses a KNIME MoSS node.

## Limitations / caveats

- Node settings are part of the scientific method; a workflow screenshot without settings is not enough to reproduce results.

## See also

- [[concepts/chemical-workflow-systems]]
- [[exercises/ciw-e4-moss-and-surfaces]]
- [[exercises/gci-e1-databases-workflows-and-smiles]]

## Sources

- [[sources/gci-01-foundations-of-cheminformatics]] (pp. 6, 8)
- [[sources/ciw-03-pattern-mining-diagrams-surfaces-and-reduced-graphs]] (exercise E4)
