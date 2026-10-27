# Model Analysis Package — Executive Summary

**Author:** `[ANALYST: name]`  
**Role:** `[ANALYST: role — Model Risk / Independent Validator]`  
**Status:** Portfolio demonstration — two independent model risk projects  
**Last updated:** `[ANALYST: date]`

---

## What this is

This repository contains a **Model Analysis Package (MAP)** — the standard set of twelve deliverables a model risk function produces when it validates a model or a methodology. It is demonstrated on **two independent projects**, each with a different dataset, audience, and validation paradigm:

| Project | Dataset | What's validated | Verdict |
|---|---|---|---|
| **Lending Club Credit Default Model** | Lending Club public loan data (10,000 records) | A **model** — fit for deployment? | **HIGH / REJECT** |
| **Fannie Mae IFRS 9 ECL Demonstration** | Fannie Mae Single-Family Loan Performance (100,000 records) | A **methodology** — fit to be cited? | **Accepted as a demonstration** |

The two projects share a common structure — the twelve MAP deliverables, the same audit discipline, the same regulatory framing (OSFI E-23, SR 11-7) — but they answer different questions. **Read together, they demonstrate both paradigms of model risk validation.**

---

## The two projects at a glance

### Lending Club — Model Validation

**The question:** Is this collections-prioritization model fit to be deployed?

**The story:** A model was built with a developer-claimed AUC of 0.865. Independent validation found that 9 post-origination leakage features were inflating the performance — realistic AUC is **0.631**, a 27.1% drop. With the leakage removed, the model fails 6 of 7 testable success criteria. The verdict is **HIGH / REJECT**, driven primarily by **fairness** (region-level disparate impact DI = 0.5414, below the SEVERE threshold of 0.60).

**What this demonstrates:**
- Leakage detection via pre-registered list (not post-hoc scan)
- Independent recomputation of metrics (not trusting the developer's numbers)
- FD-05-compliant fairness testing (region grouping, not per-state one-hot)
- Verdict-ownership chain (developer → validator → governance → committee)
- A REJECT verdict that is **mechanical**, not judgmental — 6 of 7 criteria fail

**Audience:** Model Risk Committee members.

**Bundle:** [Lending Club standalone →](./lending-club/)

---

### Fannie Mae — Methodology Validation

**The question:** Is this IFRS 9 ECL methodology fit to be cited as a demonstration?

**The story:** A pipeline was built to demonstrate IFRS 9 parameterization — PD, LGD, EAD, staging, and probability-weighted ECL — on historical mortgage data. The methodology has **no critical findings**. Its 10 limitations (L1–L10) are documented, quantified, and mapped to IFRS 9 paragraphs. The register guards fire as designed: AP-02 (LGD band) passes, AP-03 (EAD ratio 86.95%) fires as **expected** on a young portfolio, AP-04 (ECL ratio 1.09%) passes. The verdict is **accepted as a demonstration**.

**What this demonstrates:**
- Parameter construction with frozen formulas (not fitted parameters)
- IFRS 9 staging with a documented SICR proxy
- Probability-weighted ECL across four scenarios
- Register guards that fire as designed (AP-03 is expected, not a defect)
- Claim-authorization (the pipeline produces evidence; the analyst authors the verdict)
- A methodology story where the limitations are the deliverable

**Audience:** IFRS 9 modellers, internal audit, regulators.

**Bundle:** [Fannie Mae standalone →](./fannie-mae/)

---

## The verdicts, side by side

| Dimension | Lending Club | Fannie Mae |
|---|---|---|
| **What's validated** | A model | A methodology |
| **Verdict** | HIGH / REJECT | Accepted as a demonstration |
| **Primary driver** | Fairness (DI 0.5414, SEVERE) | N/A — limitations documented |
| **Critical findings** | 4 (2 distinct issues: leakage, fairness) | 0 |
| **Findings total** | 26 | 13 |
| **The "killer" metric** | Region-level DI ≥ 0.80 (currently 0.5414 — fails) | AP-03 EAD ratio ≤ 85% (currently 86.95% — expected) |
| **The "expected failure"** | None — all failures are remediable | AP-03 is expected on a young portfolio |
| **Remediation** | 8 actions, 3-month critical path | Documentation only — no fixes needed |
| **Verdict location** | In the pipeline (NB03) | In the MAP document (Validation Opinion) |
| **Approval authority** | Model Risk Committee Chair | Methodology Owner |

**The single-sentence distinction:**

> *Lending Club asks "is this model fit to be deployed?" and the answer is no — 6 of 7 criteria fail. Fannie Mae asks "is this methodology fit to be cited?" and the answer is yes, with documented limitations.*

---

## The twelve MAP deliverables

Both projects use the same twelve-deliverable structure. Each is a standalone document.

| # | Deliverable | What it does | Lending Club | Fannie Mae |
|---|---|---|---|---|
| 1 | **Problem Definition Record** | Defines the problem, target, scope, success criteria | ✅ | ✅ |
| 2 | **Analytical Specification** | Specifies what the analysis must produce | ✅ | ✅ |
| 3 | **Data Specification** | Documents the data, quality, leakage, limitations | ✅ | ✅ |
| 4 | **Feature Decision Log** | Records every feature's include/exclude decision | ✅ | ✅ |
| 5 | **Methodology Document** | Describes how the model/methodology works | ✅ | ✅ |
| 6 | **Risk & Validation Plan** | Specifies what will be tested, and who decides | ✅ | ✅ |
| 7 | **Decision Criteria Register** | Records every threshold, band, and weight | ✅ | ✅ |
| 8 | **Findings Register** | Consolidates every finding across the pipeline | ✅ | ✅ |
| 9 | **Remediation Plan** | Specifies how to move from verdict to re-validation | ✅ | ✅ |
| 10 | **Validation Opinion** | Authors the verdict (the human judgment) | ✅ | TBD |
| 11 | **Approval Record** | Records the formal decision and signatures | ✅ | ✅ |
| 12 | **Analysis Code & Results** | Indexes the code and summarizes the results | ✅ | ✅ |

**Supporting artifacts:** AI Interaction Record, Reproducibility Record, cleaned notebooks (11 total), changelog files (2).

---

## The two validation paradigms

Reading both projects side by side reveals the **two paradigms of model risk validation**:

### 1. Model validation (Lending Club)

- **The verdict is in the pipeline.** NB03 authors the verdict; NB04 inherits it; NB05 reads it as context.
- **The verdict-ownership chain is the control.** No notebook can short-circuit the chain.
- **The verdict is mechanical.** 6 of 7 criteria fail; the REJECT is arithmetic, not judgment.
- **The verdict is remediable.** 8 conditions, 3-month critical path, re-validation trigger.

**The story:** A model that failed validation, with a clear path to remediation.

### 2. Methodology validation (Fannie Mae)

- **The verdict is in the MAP document.** The pipeline produces evidence; the Validation Opinion authors the verdict.
- **The parameter-freeze is the control.** Every parameter is in `IFRS9Config`; changing any of them is a MAJOR version bump.
- **The verdict is documentation-based.** The methodology has 0 critical findings, 5 HIGH limitations — all documented.
- **The verdict is scoped.** Accepted as a demonstration, not for production use.

**The story:** A methodology that is defensible because its limitations are explicit, not because it has none.

---

## The portfolio-level insight

The most important thing this portfolio demonstrates is not a model or a methodology — it's the **two paradigms**.

A model risk function that only does model validation would not know how to validate a methodology. A model risk function that only does methodology validation would not know how to validate a model. **The portfolio demonstrates both.**

**The insight in one sentence:**

> *A model needs to be corrected; a methodology needs to be scoped. The Lending Club project shows the correction path (REJECT → 8 remediation actions → re-validation). The Fannie Mae project shows the scoping path (10 limitations documented → accepted as a demonstration). Both are necessary; both are demonstrated here.*

---

## What a reader should look at first

**For an interviewer or hiring manager:**

1. **This executive summary** — you're reading it.
2. **[Lending Club Validation Opinion](./lending-club/docs/validation_opinion.md)** — the model validation verdict, in full.
3. **[Lending Club Findings Register](./lending-club/docs/findings_register.md)** — the 26 findings, 4 CRITICAL, cross-referenced.
4. **[Fannie Mae Methodology Document](./fannie-mae/docs/methodology.md)** — the IFRS 9 parameterization, in full.
5. **[Fannie Mae Findings Register](./fannie-mae/docs/findings_register.md)** — the 13 documented limitations.

**For a validator or model risk professional:**

1. **[Lending Club Decision Criteria Register](./lending-club/docs/dcr.md)** — the thresholds that determine the verdict.
2. **[Lending Club Risk & Validation Plan](./lending-club/docs/rvp.md)** — the validation contract.
3. **[Fannie Mae Decision Criteria Register](./fannie-mae/docs/dcr.md)** — the register guards and parameter bounds.
4. **[Fannie Mae Risk & Validation Plan](./fannie-mae/docs/rvp.md)** — the methodology-validation contract.

**For a regulator or auditor:**

1. **[Lending Club Approval Record](./lending-club/docs/approval_record.md)** — the formal decision.
2. **[Lending Club Remediation Plan](./lending-club/docs/remediation_plan.md)** — the path to re-validation.
3. **[Fannie Mae Approval Record](./fannie-mae/docs/approval_record.md)** — the methodology acceptance.
4. **[Fannie Mae AI Interaction Record](./fannie-mae/docs/ai_interaction_record.md)** — the AI-assisted changes.

---

## Repository structure

```
model-analysis-package/
├── README.md  (this file)
├── executive_summary.md
│
├── lending-club/
│   ├── README.md
│   ├── notebooks/  (NB01–NB05)
│   ├── docs/  (the 12 MAP deliverables)
│   ├── artifacts/  (models, predictions, JSONs, CSVs)
│   └── changelog.md
│
├── fannie-mae/
│   ├── README.md
│   ├── notebooks/  (NB01–NB06)
│   ├── docs/  (the 12 MAP deliverables)
│   ├── artifacts/  (parameters, manifests, Power BI exports)
│   └── changelog.md
│
└── supporting/
    ├── ai_interaction_record.md
    ├── reproducibility_record.md
    └── two_paradigms.md  (the portfolio-level insight)
```

**Two standalone bundles + one umbrella.** The Lending Club and Fannie Mae bundles are **self-contained** — each has its own README, its own 12 MAP deliverables, and its own artifacts. The umbrella introduces both and links to them. **A reader can start from either project, or from the umbrella.**

---

## How this portfolio was built

**The AI was a tool, not an author.** Every verdict, every severity assignment, every scope decision was human-authored. The AI's contributions are documented in the [AI Interaction Record](./supporting/ai_interaction_record.md):

- **AI-assisted:** code structure, documentation, diagnostic narratives, suggested fixes (E-MXX edits)
- **Human-authored:** the verdict, the fairness thresholds, the attribution of the REJECT to fairness (not AUC), the scope decisions ("direction only, not magnitude"), the severity assignments
- **Never AI-assisted:** any decision that appears in the Validation Opinion or the Approval Record

**Reproducibility:** every artifact carries a `run_id` and `notebook_version`. Every notebook uses seed 42. Every run produces an audit log. A reviewer can reproduce the results from the artifacts alone.

---

## Status

| Project | Status | Next milestone |
|---|---|---|
| Lending Club | Validation Opinion signed (REJECT) | MRC decision; remediation plan approval |
| Fannie Mae | Methodology documented and accepted | MAP Validation Opinion sign-off |

**Nothing here is production-ready.** The Lending Club model is REJECTed (awaiting remediation). The Fannie Mae methodology is accepted as a demonstration, not for production use. **Both are portfolio demonstrations, not deployed systems.**

---  
**LinkedIn:** `[ANALYST: linkedin]`

**Questions about this portfolio:** open an issue in the relevant sub-bundle, or reach out directly.
