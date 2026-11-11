# AI Interaction Record

**Document ID:** MAP-AIR-001  
**Version / Status:** 0.2 / Template — structured fields filled; narrative fields marked  
**Scope:** Cross-project (Lending Club + Fannie Mae)  
**Owner:** `[ANALYST: name, role]`  
**Companion documents:** [`05_reproducibility_record.md`](05_reproducibility_record.md), [`02_validation_report_lc.md`](02_validation_report_lc.md), [`03_stress_testing_framework_fm.md`](03_stress_testing_framework_fm.md)

---

> **This is a template with filled structured fields.** The **structured fields** — run IDs, notebook versions, file hashes — are sourced from the notebook outputs and the two project READMEs. The **narrative fields** — prompts used, content rejected, analyst judgment calls — are the analyst's contribution and cannot be sourced from the notebook outputs. A notebook that recorded the analyst's narrative would be a notebook that violates the claim-authorization discipline: the notebook computes, the analyst declares. **The narrative fields are marked `[ANALYST: ...]` for this reason.** When the analyst fills them, the document becomes complete.

---

## Records at a glance

| Record ID | Project | Pipeline run IDs | Status |
|---|---|---|---|
| AIR-LC-001 | Lending Club | NB01–NB05 (5 runs) | `[ANALYST: sign-off pending]` — structured fields filled; narrative fields marked |
| AIR-FM-001 | Fannie Mae | NB01–NB06 (6 runs) | `[ANALYST: sign-off pending]` — structured fields filled; narrative fields marked |

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

**On the two kinds of fields.** The **structured fields** (`record_id`, `project`, `pipeline_run_ids`, `ai_system`, `interaction_dates`, `reproducibility_evidence`) are factual and can be sourced from the notebook outputs. The **narrative fields** (`prompts_summary`, `ai_produced_artifacts` in narrative form, `human_reviewed_artifacts`, `human_rejected_content`, `analyst_judgment_calls`) are the analyst's contribution. The `sign_off` field is the analyst's by definition.

---

## 3. Populated instance — Lending Club

### 3.1 — Structured fields (sourced)

| Field | Value |
|---|---|
| `record_id` | AIR-LC-001 |
| `project` | Lending Club |
| `pipeline_run_ids` | NB01: `20261021_144955`; NB02: `20261021_145000`; NB03: `20261021_145017`; NB04: `20261021_145017`; NB05: `20261021_145018` |
| `ai_system` | `[ANALYST: name, version]` |
| `interaction_dates` | `[ANALYST: start, end]` |
| `reproducibility_evidence` | Manifest `outputs/manifest_pipeline_v1_2.csv` (126 files hashed); audit logs in `logs/`; content hashes in each JSON artifact; run IDs above; see [`05_reproducibility_record.md`](05_reproducibility_record.md) §2 |

### 3.2 — Narrative fields (analyst's contribution)

| Field | Value |
|---|---|
| `prompts_summary` | `[ANALYST: summarize prompt categories — e.g., "code generation for notebooks," "interpretation drafting," "regulatory mapping"]` |
| `ai_produced_artifacts` | `[ANALYST: list the artifacts the AI produced or substantially drafted — e.g., NB01–NB05 code, governance artifact drafts]` |
| `human_reviewed_artifacts` | `[ANALYST: list the artifacts the human reviewed and accepted or modified]` |
| `human_rejected_content` | `[ANALYST: list the content the human rejected, with reason — e.g., "AI-drafted narrative asserting 'the model passes fair lending' was rejected because the test is out of scope for high-cardinality geography"]` |
| `analyst_judgment_calls` | `[ANALYST: list the judgment calls made by the human, not the AI — e.g., "verdict of 6/10 HIGH REJECT," "accepting the fairness finding as the primary rejection driver," "choosing region-level FD-05 over per-state DI"]` |
| `sign_off` | `[ANALYST: name, role, date, signature]` |

---

## 4. Populated instance — Fannie Mae

### 4.1 — Structured fields (sourced)

| Field | Value |
|---|---|
| `record_id` | AIR-FM-001 |
| `project` | Fannie Mae |
| `pipeline_run_ids` | NB01: `20261021_121434`; NB02: `20261021_121539`; NB03: `20261021_121550`; NB04: `20261021_121552`; NB05: `20261021_121553`; NB06: `20261021_121555` |
| `ai_system` | `[ANALYST: name, version]` |
| `interaction_dates` | `[ANALYST: start, end]` |
| `reproducibility_evidence` | Manifest `outputs/manifest_pipeline_v1_2.csv`; audit logs in `logs/`; content hash `bc5263ca06d29037`; parameter JSON `outputs/notebook_03_parameters.json`; results JSON `outputs/notebook_04_results.json`; run IDs above; see [`05_reproducibility_record.md`](05_reproducibility_record.md) §3 |

### 4.2 — Narrative fields (analyst's contribution)

| Field | Value |
|---|---|
| `prompts_summary` | `[ANALYST: summarize prompt categories used]` |
| `ai_produced_artifacts` | `[ANALYST: list the artifacts the AI produced or substantially drafted — e.g., NB01–NB06 code, governance artifact drafts, the claim-authorization discipline design]` |
| `human_reviewed_artifacts` | `[ANALYST: list the artifacts the human reviewed and accepted or modified]` |
| `human_rejected_content` | `[ANALYST: list the content the human rejected, with reason — e.g., "AI-drafted 'capital adequacy' language was rejected and reframed as 'capital coverage' because the CET1 denominator is a scale artifact"]` |
| `analyst_judgment_calls` | `[ANALYST: list the judgment calls made by the human — e.g., "accepting the EAD ratio as outside band and treating it as a finding (FM-R-08)," "documenting Stage 2 as SICR-by-construction (FM-R-07)," "designing the claim-authorization discipline (no notebook writes a verdict)"]` |
| `sign_off` | `[ANALYST: name, role, date, signature]` |

---

## 5. Cross-project notes

**The two pipelines share the same AI-assisted workflow** (Jupyter notebooks, iterative drafting, output review). The record distinguishes them because the Fannie Mae pipeline's claim-authorization discipline is a more deliberate design choice than the Lending Club pipeline's verdict separation.

**The analyst retains judgment.** The AI produced code and drafted narrative; the analyst made the judgment calls and rejected the content listed above. The record is not a claim that the AI produced the deliverables — it is a record of what the AI contributed and what the human decided.

**The record is a living document.** If the pipeline is rerun with new AI-assisted work, a new AIR record is created with the new run IDs. The old record is retained.

---

## 6. Document control

| Field | Value |
|---|---|
| **Document ID** | MAP-AIR-001 |
| **Version** | 0.2 |
| **Status** | Template with structured fields filled; narrative fields marked `[ANALYST: ...]` |
| **Owner** | `[ANALYST: name, role]` |
| **Supersedes** | None (first version) |
| **Related documents** | [`05_reproducibility_record.md`](05_reproducibility_record.md), [`02_validation_report_lc.md`](02_validation_report_lc.md), [`03_stress_testing_framework_fm.md`](03_stress_testing_framework_fm.md) |
| **Next review** | At the next re-run of either pipeline with AI-assisted work |

---

*End of document.*
