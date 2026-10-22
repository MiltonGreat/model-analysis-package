# AI Interaction Record

**Document ID:** MAP-AIR-001  
**Version / Status:** 0.1 / Draft — template + two populated instances  
**Scope:** Cross-project (Lending Club + Fannie Mae)

---

## Records at a glance

| Record ID | Project | Pipeline run IDs | Status |
|---|---|---|---|
| AIR-LC-001 | Lending Club | NB01–NB05 (5 runs) | `[ANALYST: sign-off pending]` |
| AIR-FM-001 | Fannie Mae | NB01–NB06 (6 runs) | `[ANALYST: sign-off pending]` |

> **Note on the placeholders.** The `[ANALYST: ...]` fields below depend on your actual interaction history — prompts used, content rejected, judgment calls made. The code documents the run IDs, versions, and hashes; the narrative of *how* AI was used is yours to record.

---

## 1. Purpose

This record documents how AI was used in the production of the Lending Club and Fannie Mae pipelines and their governance artifacts. It is a **cross-project template with two populated instances** — one per pipeline — because the two pipelines were produced under the same AI-assisted workflow.

The record exists because:

- **Reproducibility:** a reviewer must be able to reconstruct what the human did and what the AI did.
- **Accountability:** the analyst retains judgment; the AI is a tool. The record distinguishes AI-produced content from human-reviewed content.
- **Auditability:** if the pipeline is later challenged, the record shows what was AI-assisted and what was independently verified.

---

## 2. Template structure

| Field | Description | Required? |
|---|---|---|
| `record_id` | Unique identifier (e.g., AIR-LC-001) | Yes |
| `project` | LC or FM | Yes |
| `pipeline_run_ids` | All run IDs covered by this record | Yes |
| `ai_system` | AI system used (name, version) | Yes |
| `interaction_dates` | Start and end dates of AI-assisted work | Yes |
| `prompts_summary` | Summary of prompt categories used | Yes |
| `ai_produced_artifacts` | Artifacts the AI produced or substantially drafted | Yes |
| `human_reviewed_artifacts` | Artifacts the human reviewed and accepted/modified | Yes |
| `human_rejected_content` | Content the human rejected (with reason) | Yes |
| `analyst_judgment_calls` | Judgment calls made by the human, not the AI | Yes |
| `reproducibility_evidence` | Links to run IDs, logs, hashes | Yes |
| `sign_off` | Analyst name, role, date, signature | Yes |

---

## 3. Populated instance — Lending Club

| Field | Value |
|---|---|
| `record_id` | AIR-LC-001 |
| `project` | Lending Club |
| `pipeline_run_ids` | NB01: `20261021_144955`; NB02: `20261021_145000`; NB03: `20261021_145017`; NB04: `20261021_145017`; NB05: `20261021_145018` |
| `ai_system` | `[ANALYST: name, version]` |
| `interaction_dates` | `[ANALYST: start, end]` |
| `prompts_summary` | `[ANALYST: summarize prompt categories — e.g., "code generation for notebooks," "interpretation drafting," "regulatory mapping"]` |
| `ai_produced_artifacts` | Notebook code (NB01–NB05); governance artifact drafts (LC-PDR-001, LC-DS-001, LC-FDL-001, LC-MD-001, LC-RVP-001, LC-DCR-001); interpretation narrative |
| `human_reviewed_artifacts` | All notebook outputs before acceptance; the verdict in NB03 (6/10 HIGH REJECT); the fairness test correction (per-state → region); the split-method disclosure |
| `human_rejected_content` | `[ANALYST: insert — e.g., "AI-drafted narrative asserting 'the model passes fair lending' was rejected because the test is out of scope for high-cardinality geography"]` |
| `analyst_judgment_calls` | (1) Verdict of 6/10 HIGH REJECT; (2) accepting the fairness finding as the primary rejection driver; (3) choosing region-level FD-05 over per-state DI; (4) documenting the random-split deviation rather than blocking the run |
| `reproducibility_evidence` | Manifest `outputs/manifest_pipeline_v1_2.csv` (126 files hashed); audit logs in `logs/`; content hashes in each JSON artifact; run IDs above |
| `sign_off` | `[ANALYST: name, role, date, signature]` |

---

## 4. Populated instance — Fannie Mae

| Field | Value |
|---|---|
| `record_id` | AIR-FM-001 |
| `project` | Fannie Mae |
| `pipeline_run_ids` | NB01: `20261021_121434`; NB02: `20261021_121539`; NB03: `20261021_121550`; NB04: `20261021_121552`; NB05: `20261021_121553`; NB06: `20261021_121555` |
| `ai_system` | `[ANALYST: name, version]` |
| `interaction_dates` | `[ANALYST: start, end]` |
| `prompts_summary` | `[ANALYST: summarize prompt categories]` |
| `ai_produced_artifacts` | Notebook code (NB01–NB06); governance artifact drafts (FM-PDR-001, FM-DS-001, FM-FDL-001, FM-MD-001, FM-RVP-001, FM-DCR-001); interpretation narrative; the claim-authorization discipline design |
| `human_reviewed_artifacts` | All notebook outputs; the claim-authorization assertions (NB05 Phase 7, NB06 Section 6); the Stage 2 "by construction" callout; the AP-03 EAD ratio flag; the scenario severity ratio (1.27×) and its treatment as IT-05 |
| `human_rejected_content` | `[ANALYST: insert — e.g., "AI-drafted 'capital adequacy' language was rejected and reframed as 'capital coverage' because the CET1 denominator is a scale artifact"]` |
| `analyst_judgment_calls` | (1) Accepting the EAD ratio as outside band and treating it as a finding (FM-R-08); (2) accepting the severity ratio 1.27× as below target and treating it as a remediation item (FM-R-06); (3) documenting Stage 2 as SICR-by-construction (FM-R-07); (4) designing the claim-authorization discipline (no notebook writes a verdict) |
| `reproducibility_evidence` | Manifest `outputs/manifest_pipeline_v1_2.csv`; audit logs in `logs/`; content hash of clean frame `bc5263ca06d29037`; parameter JSON `outputs/notebook_03_parameters.json`; results JSON `outputs/notebook_04_results.json`; run IDs above |
| `sign_off` | `[ANALYST: name, role, date, signature]` |

---

## 5. Cross-project notes

**The two pipelines share the same AI-assisted workflow** (Jupyter notebooks, iterative drafting, output review). The record distinguishes them because the Fannie Mae pipeline's claim-authorization discipline is a more deliberate design choice than the Lending Club pipeline's verdict separation.

**The analyst retains judgment.** The AI produced code and drafted narrative; the analyst made the judgment calls listed above and rejected the content listed above. The record is not a claim that the AI produced the deliverables — it is a record of what the AI contributed and what the human decided.

**The record is a living document.** If the pipeline is rerun with new AI-assisted work, a new AIR record is created with the new run IDs. The old record is retained.

---

*End of document.*
