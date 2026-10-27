---
title: CiW Lecture 1 — Drug Action, Protein–Ligand Interactions and Lead Discovery
type: source
raw: raw/ciw_1.pdf
tags: [lecture, foundations, pharmacology, protein-ligand, thermodynamics]
date_ingested: 2026-09-30
pages: 22
---

# CiW Lecture 1 — Drug Action, Protein–Ligand Interactions and Lead Discovery

Handwritten German summary of lecture 1 (pages 1–20) plus exercise sheet E1 (pages 21–22).
Content below is translated to English; original German terms of art are kept in parentheses.

## Summary

- **Drug development** splits into *preclinical* (hit finding → lead development → mechanism
  of action → toxicity/ADME → testing cascade receptors/proteins → cells → organs → animals)
  and *clinical* (Phase 1 healthy subjects, Phase 2 selected patients, Phase 3 patient
  groups → approval, Phase 4 post-marketing). See [[concepts/drug-discovery-pipeline]].
- **Hit** = any compound with binding activity to the biological target.
  **Lead** (Leitstruktur) = compound with pharmacological activity that still needs optimisation.
- Computers enter at **target discovery** (bioinformatics) and at **lead generation /
  lead optimisation** (cheminformatics & molecular modelling): compound management,
  physico-chemical property prediction, screening library design, virtual screening,
  screening data analysis, ADME/Tox prediction, lead-series activity prediction.
- **Optimisation is multi-objective**: potency, solubility, absorption, specificity,
  metabolic stability, safety — each pulls in a different direction in property space.
- **Pharmacological level**: *Arznei* (drug product) vs *Wirkstoff* (active ingredient);
  pharmacodynamics = analysis of the biological effect, pharmacokinetics = analysis of the
  drug concentration in the body. See [[concepts/pharmacokinetics-and-pharmacodynamics]].
- Six **boundary conditions** (Randbedingungen) a drug must satisfy: suitability for the
  dosage form, bioavailability, specificity, non-toxicity, elimination, synthetic accessibility.
  Conditions 1–5 correspond to the **ADMET** parameters. See [[concepts/admet]].
- **Biochemical level**: metabolic networks (energy, anabolism/catabolism) and regulatory
  networks (information transmission/processing/storage). Enzymes are biocatalysts;
  inhibitors act competitively or allosterically, reversibly or irreversibly.
  See [[concepts/enzymes-and-receptors]].
- **Protein–ligand complex formation** is specific, energetically favourable, reversible and
  based on steric + physico-chemical **complementarity** (lock-and-key), with both partners
  flexible. Eight-stage binding process from diffusion to saturation.
  See [[concepts/protein-ligand-binding]].
- Water is a first-class participant: hydration shell, **desolvation**, hydrophobic effect,
  solvent-mediated (bridging) interactions. See [[concepts/desolvation-and-water]].
- **Interaction types**: covalent, hydrogen bonds, ionic/salt bridges, metal complexation,
  hydrophobic effect, entropic contributions. See [[concepts/intermolecular-interactions]],
  [[concepts/hydrogen-bond]], [[concepts/hydrophobic-effect]].
- **Thermodynamics**: Kᵢ, ΔG = RT ln Kᵢ, ΔG = ΔH − TΔS, IC₅₀; enthalpy–entropy compensation
  means affinity is **not additive** and does not correlate with H-bond count or lipophilic
  surface alone. See [[concepts/binding-thermodynamics]],
  [[concepts/enthalpy-entropy-compensation]].
- **Lead finding strategies**: traditional design, (high-throughput) screening, virtual
  screening (structure- or ligand-based), similarity searching, de novo design — all feeding
  a design cycle with experimental validation. See [[concepts/lead-finding-strategies]],
  [[concepts/virtual-screening]], [[concepts/de-novo-design]],
  [[concepts/high-throughput-screening]].
- **Open challenge**: modelling protein flexibility (protonation states, terminal group
  rotation, side-chain and loop conformation, domain orientation) across many timescales.
  See [[concepts/protein-flexibility]].

## Key concepts introduced

| Page(s) | Concept | Wiki page |
|---|---|---|
| 1 | Preclinical/clinical phases, hit vs lead, role of computers | [[concepts/drug-discovery-pipeline]] |
| 2 | Multi-objective optimisation of drug properties | [[concepts/drug-discovery-pipeline]] |
| 3 | Pharmacodynamics, pharmacokinetics, routes of administration | [[concepts/pharmacokinetics-and-pharmacodynamics]] |
| 3–4 | Six boundary conditions, ADMET | [[concepts/admet]] |
| 5, 8 | Metabolic/regulatory networks, enzymes, receptors | [[concepts/enzymes-and-receptors]] |
| 5–6 | Complex formation, 8-stage binding process | [[concepts/protein-ligand-binding]] |
| 7, 13 | Hydration shell, desolvation, bridging waters | [[concepts/desolvation-and-water]] |
| 9 | Molecular structure, conformation, stereoisomerism | [[concepts/molecular-structure-and-stereochemistry]] |
| 10 | Kᵢ, ΔG, IC₅₀, enthalpy, entropy | [[concepts/binding-thermodynamics]] |
| 11–13 | Interaction types, H-bonds, ionic, hydrophobic | [[concepts/intermolecular-interactions]], [[concepts/hydrogen-bond]], [[concepts/hydrophobic-effect]] |
| 14–16 | Entropic contributions, enthalpy–entropy compensation | [[concepts/enthalpy-entropy-compensation]] |
| 17 | Rules of thumb for optimisation | [[concepts/lead-optimization-heuristics]] |
| 18–19 | Screening, virtual screening, de novo design | [[concepts/lead-finding-strategies]] |
| 20 | Computer applications, protein flexibility | [[concepts/protein-flexibility]] |
| 21–22 | Exercise E1 | [[exercises/ciw-e1-thermodynamics-and-hydrogen-bonds]] |

## Formulas & algorithms

```text
Kᵢ = [Ligand]·[Protein] / [Ligand·Protein]        # dissociation constant, mol/L
ΔG = R·T·ln Kᵢ                                     # free binding enthalpy, kJ/mol
ΔG = ΔH − T·ΔS                                     # Gibbs free energy
ΔH = ΔU − volume work                              # enthalpy at constant pressure
IC₅₀ = ligand concentration at which protein activity drops to 50 %
```

Reference values stated in the lecture:
- very good inhibitor: Kᵢ = 10⁻⁹ M = 1 nM, ΔG ≈ −53.4 kJ/mol
- ΔG < 0 → reaction runs spontaneously; ΔH negative is good; ΔS large is good
- hydrophobic effect contributes ≈ −50 to −200 J·mol⁻¹·Å⁻² of buried surface

## Exam-relevant points

- Definitions: hit, lead, *Arznei* vs *Wirkstoff*, pharmacodynamics vs pharmacokinetics.
- The six boundary conditions and their mapping to A-D-M-E-T.
- The eight stages of the binding process, in order.
- H-bond geometry: N–O distance 2.8–3.2 Å, N–H···O angle > 150°, C=O···H angle 100–180°.
- Ionic interaction (salt bridge) distance 2.7–3.0 Å.
- Enthalpy–entropy compensation ⇒ **no additivity** of interaction contributions.
- The Tyrosyl-tRNA-synthetase example: NH → CH₂ exchange is roughly neutral for Kᵢ,
  NH → O exchange costs **three orders of magnitude** in Kᵢ.

## Open questions

- The lecture writes "Tyrosyl-RNA-Synthase"; the standard name is tyrosyl-tRNA synthetase.
  Recorded in [[open-questions]].
- The hydrophobic-effect coefficient is written as "−50 … −200 J/mol/Å²"; the more common
  textbook figure is ≈ 25–30 cal·mol⁻¹·Å⁻² (≈ 105–125 J·mol⁻¹·Å⁻²). Unit/magnitude to verify.

## Pages touched by this ingest

Created: 15 concept pages, 1 exercise page (see table above).
Updated: [[index]], [[log]], [[overview]], [[synthesis]], [[open-questions]].
