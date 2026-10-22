# Reproducibility Record

**Document ID:** MAP-RR-001  
**Version / Status:** 0.1 / Draft — one per project + pipeline manifest  
**Scope:** Cross-notebook (Lending Club + Fannie Mae)

---

## Records at a glance

| Record ID | Project | Run IDs | Notebook versions | Reproducibility status |
|---|---|---|---|---|
| RR-LC-001 | Lending Club | NB01–NB05 (5 runs) | NB01: 2.1 · NB02: 2.1 · NB03: 2.1 · NB04: 2.1 · NB05: 2.2 | Reproducible by re-running in order with seed 42 |
| RR-FM-001 | Fannie Mae | NB01–NB06 (6 runs) | NB01: 1.2 · NB02: 1.2 · NB03: 1.3 · NB04: 1.3 · NB05: 1.2 · NB06: 1.2 | Reproducible by re-running in order with seed 42 and `SAMPLE_SIZE` 100,000 |
| RR-MANIFEST-001 | Cross-project | Both | Both | Manifests + audit logs on disk |

---

## 1. Purpose

This record documents the reproducibility evidence for the Lending Club and Fannie Mae pipelines. It is structured as **two per-project records plus one pipeline manifest** because the two pipelines have independent run IDs, logs, and hashes, but share a common reproducibility discipline.

---

## 2. Record — Lending Club

| Field | Value |
|---|---|
| `record_id` | RR-LC-001 |
| `run_ids` | NB01: `20261021_144955`; NB02: `20261021_145000`; NB03: `20261021_145017`; NB04: `20261021_145017`; NB05: `20261021_145018` |
| `notebook_versions` | NB01: 2.1; NB02: 2.1; NB03: 2.1; NB04: 2.1; NB05: 2.2 |
| `random_state` | 42 (project-wide) |
| `source_file` | `loans_full_schema.csv` (hash `52872e7d4f8a388b`) |
| `data_quality_summary_hash` | `6a59c1c23b4703b8` |
| `feature_inventory_hash` | `4bdb0fc02a527c61` |
| `performance_summary_hash` | `1398909ea1ed5d64` |
| `findings_register_hashes` | NB01: `93e3062add5decd7`; NB02: `5fe5353af964424d`; NB03: `a4a3e1dc6d864eac` |
| `fairness_validation_hash` | `1cf9f26b4b8718af` |
| `german_credit_summary_hash` | `185b73ae79ef3b65` |
| `manifest` | `outputs/manifest_pipeline_v1_2.csv` (126 files) |
| `environment` | `[ANALYST: Python version, key package versions, OS]` |
| `re-run instructions` | Run NB01–NB05 in order; do not substitute files; do not change `random_state`; verify hashes against this record |

---

## 3. Record — Fannie Mae

| Field | Value |
|---|---|
| `record_id` | RR-FM-001 |
| `run_ids` | NB01: `20261021_121434`; NB02: `20261021_121539`; NB03: `20261021_121550`; NB04: `20261021_121552`; NB05: `20261021_121553`; NB06: `20261021_121555` |
| `notebook_versions` | NB01: 1.2; NB02: 1.2; NB03: 1.3; NB04: 1.3; NB05: 1.2; NB06: 1.2 |
| `random_state` | 42 (project-wide) |
| `sample_size` | 100,000 (from 1,672,822 rows) |
| `source_file` | `Fannie Mae.zip` → `train4.csv` |
| `clean_frame_content_hash` | `bc5263ca06d29037` |
| `clean_frame_file_hash` | `[ANALYST: insert from manifest_notebook_01.csv]` |
| `assumptions_register_hash` | `[ANALYST: insert from manifest]` |
| `parameters_json_hash` | `0973eb632a92acae` |
| `results_json_hash` | `0411830e1212ee3e` |
| `limitations_hashes` | NB03: `25179aa270d77e83`; NB04: `6a3b924ab9d2d8ea`; fairness: `c8eda3dd26ea07ec` |
| `powerbi_export_manifest` | `powerbi_exports/manifest.csv` (9 exports + manifest) |
| `environment` | `[ANALYST: Python version, key package versions, OS]` |
| `re-run instructions` | Run NB01–NB06 in order; do not substitute files; do not change `random_state` or `SAMPLE_SIZE`; verify content hash `bc5263ca06d29037` and parameter/results JSON hashes; verify Power BI promotion assertion passes |

---

## 4. Pipeline manifest — cross-project

| Field | Value |
|---|---|
| `record_id` | RR-MANIFEST-001 |
| `lc_manifest` | `outputs/manifest_pipeline_v1_2.csv` (LC pipeline) |
| `fm_manifest` | `outputs/manifest_pipeline_v1_2.csv` (FM pipeline — same filename, different project) |
| `powerbi_manifest` | `powerbi_exports/manifest.csv` (FM dashboard exports) |

### Audit logs

| Notebook | Log filename |
|---|---|
| LC NB01 | `logs/eda_audit_trail_*.log` |
| LC NB02 | `logs/model_dev_audit_trail_*.log` |
| LC NB03 | `logs/validation_audit_trail_*.log` |
| LC NB04 | `logs/governance_audit_trail_*.log` |
| LC NB05 | `logs/german_credit_audit_trail_*.log` |
| FM NB01 | `logs/ecl_audit_trail_*.log` |
| FM NB02 | `logs/eda_audit_trail_*.log` **(note: filename collision with LC NB01)** |
| FM NB03 | `logs/calibration_audit_trail_*.log` |
| FM NB04 | `logs/stress_testing_audit_trail_*.log` |
| FM NB05 | `logs/reporting_audit_trail_*.log` |
| FM NB06 | `logs/powerbi_export_audit_trail_*.log` |

> **A note on the log filename collision.** The FM NB02 log uses `eda_audit_trail_*.log` — the same prefix as the LC NB01 log. A reviewer finding a log by filename alone cannot tell which pipeline it belongs to. **Recommended fix:** prefix the FM logs with `fm_` or move them to `logs/fm/`. This is a MINOR version bump across the FM pipeline.

---

## 5. Reproducibility statement

Both pipelines are **reproducible by re-running the notebooks in order with the recorded run IDs, notebook versions, and random seeds**. The content hashes (clean frame, parameter JSON, results JSON) allow run-to-run comparison. The manifests allow file-level verification.

### What is not reproducible without re-running

- Model pickles are not content-hashed, so the model files cannot be verified without loading them and comparing predictions.
- The Fannie Mae raw ZIP (1,672,822 rows) is not retained in the manifest — only the sampled 100,000 rows. Re-running the sample requires the original ZIP.
- The German Credit source file (`german_credit_data2.csv`) hash `42be3b82a2e5073b` is recorded in the NB05 summary, but the file is not in the manifest.

### What is reproducible

- Every artifact hash is recorded.
- Every run ID is recorded.
- Every notebook version is recorded.
- Every audit log is on disk.

---

*End of document.*
