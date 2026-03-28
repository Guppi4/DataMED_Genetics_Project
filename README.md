# VARCHEK — Automated Genomic Variant Analysis Tool

> DataMED Lab × Maccabi Healthcare Services | Tel Aviv University

A semi-automated variant interpretation support tool for clinical geneticists. Given a genetic variant and patient phenotype, VARCHEK aggregates evidence from public genomic databases, applies ACMG/AMP classification rules, and generates a structured evidence dossier with a preliminary classification.

---

## Overview

The system is designed as a **decision-support tool** — not a fully autonomous classifier — with explicit human review checkpoints at critical stages.

```
Clinician Input (variant + phenotype)
         ↓
Stage 1: Normalization       → VariantValidator, Ensembl Variant Recoder
         ↓
Stage 2: Evidence Gathering  → gnomAD, ClinVar, ClinGen, VEP, LitVar2, PubMed
         ↓
Stage 3: ACMG Classification → deterministic rule engine + LLM for literature
         ↓
Stage 4: Clinical Output     → structured dossier + clinician-friendly report
```

---

## Key Features

- **Variant normalization** — resolves any notation (HGVS, rsID, genomic) to canonical form
- **Multi-source evidence** — parallel queries to 8+ genomic databases
- **ACMG/AMP rule engine** — automated criteria with manual-review flags
- **LLM-assisted literature extraction** — structured evidence from PubMed abstracts
- **Auditable cases** — versioned evidence snapshots for reevaluation over time
- **Human-in-the-loop** — 3 clinician checkpoints, not fully autonomous

---

## Data Sources (MVP)

| Source | Purpose |
|--------|---------|
| VariantValidator | Variant normalization (HGVS canonicalization) |
| gnomAD v4.1 | Population allele frequency, constraint scores |
| ClinVar | Existing classifications, submitter conflicts |
| ClinGen + GenCC | Gene-disease validity, inheritance mode |
| Ensembl VEP | Variant consequence, transcript, NMD prediction |
| myvariant.info | Aggregated scores: REVEL, CADD, SpliceAI, BayesDel |
| PubMed + LitVar2 | Variant-specific literature, case reports |
| HPO + Monarch | Phenotype standardization, gene-phenotype matching |

---

## Tech Stack

- **Language:** Python 3.11+
- **Data processing:** pandas, numpy, requests, biopython
- **LLM:** Anthropic Claude API
- **Database:** SQLite (MVP) → PostgreSQL (production)
- **Rule engine:** Custom Python — deterministic, no ML
- **UI (Phase 2):** Streamlit / Gradio (TBD)

---

## Project Structure

```
DataMED_Genetics_Project/
├── varchek/
│   ├── src/
│   │   ├── normalization/      # VariantValidator + Ensembl Variant Recoder
│   │   ├── evidence/           # API connectors (gnomAD, ClinVar, ClinGen, VEP...)
│   │   ├── literature/         # LitVar2 + PubMed + LLM extraction
│   │   ├── rules/              # ACMG/AMP classification engine
│   │   └── output/             # Report generation
│   ├── tests/
│   │   ├── variant_cdh1.py     # Validation: CDH1 c.1008G>T
│   │   └── variant_ush2a.py    # Validation: USH2A c.4338_4339del
│   └── docs/
│       └── pipeline_draft_v0.2.docx
├── CLAUDE.md
└── README.md
```

---

## Status

- [x] Project specification received (Prof. Lina Basel-Salmon, Maccabi)
- [x] Pipeline architecture designed
- [ ] Core data layer — API connectors
- [ ] Variant normalization module
- [ ] Evidence aggregation layer
- [ ] ACMG rule engine
- [ ] Literature extraction (LLM-assisted)
- [ ] Validation against CDH1 / USH2A test cases

---

## Team

DataMED Lab, Tel Aviv University × Maccabi Healthcare Services
