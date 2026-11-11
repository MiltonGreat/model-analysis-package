# Model Analysis Package — IFRS 9 ECL & Credit Model Validation

**A portfolio of two credit-risk projects and the governance framework that connects them.**

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![IFRS 9](https://img.shields.io/badge/IFRS%209-Methodology%20Demo-orange)
![OSFI E-23](https://img.shields.io/badge/OSFI%20E--23-Aligned-lightgrey)
![SR 11-7](https://img.shields.io/badge/SR%2011--7-Partially%20Aligned-yellow)
![Status](https://img.shields.io/badge/Status-Portfolio%20Artifact-lightgrey)

---

## The business problem

A bank's credit risk model has two questions to answer before it can be deployed:

1. **Is the model fit for purpose?** (validation → [Go to Lending Club repo](https://github.com/MiltonGreat/credit-risk-model-validation/blob/main/README.md))
2. **What does it mean for capital and provisioning under stress?** (framework → [Go to Fannie Mae project](https://github.com/MiltonGreat/fannie-mae-ifrs9-portfolio/tree/main))

These are different questions, answered by different teams, under different regulatory frameworks. Most portfolio projects answer one or the other. This package answers both — and, critically, shows how the two answers connect through a shared governance layer.

**The story in two paragraphs.**

A model development team built a consumer credit risk model for collections prioritization. They reported AUC 0.865 and requested deployment. Independent validation found that nine post-origination features had inflated the reported performance by 27% (realistic AUC: 0.631), and that the model approved applicants in one U.S. region at 54% of the rate of the highest-approval region. The model was rejected.

Separately, a mortgage ECL pipeline was built on Fannie Mae data to demonstrate IFRS 9 stress testing — and, in the process, surfaced a capital-adequacy framing error that would have been cited against the institution in a model risk finding. Both projects are methodology demonstrations, and both are honest about what they do and do not prove.

---

## What's in this package

The package contains **three layers of artifacts** — the project deliverables, the governance framework, and the project governance artifacts — organized around **two projects**, each following the **twelve-deliverable MAP structure**.

**The three layers are the package-level view.** They describe how the artifacts are organized across the package. **The twelve-deliverable MAP structure is the per-project view** — it describes the structure within each project. A reader who wants the package's organization reads the three layers; a reader who wants the per-project structure reads the twelve-deliverable table in the [`EXECUTIVE_SUMMARY.md`](deliverables/EXECUTIVE_SUMMARY.md).

### Layer 1 — Project deliverables (7 files in `deliverables/`)

These are the cross-project records that summarize what each project found.

| # | Deliverable | Scope | File |
|---|---|---|---|
| 1 | **Model Risk Validation Report** | Lending Club only (independent validation opinion) | `deliverables/02_validation_report_lc.md` |
| 2 | **IFRS 9 Stress Testing Framework** | Fannie Mae only (ECL + capital coverage) | `deliverables/03_stress_testing_framework_fm.md` |
| 3 | **AI Interaction Record** | Cross-project (one template, two populated instances) | `deliverables/04_ai_interaction_record.md` |
| 4 | **Reproducibility Record** | Cross-notebook (one per project + manifest) | `deliverables/05_reproducibility_record.md` |
| 5 | **Model Risk Remediation Plan** | Cross-project, 10 findings in scope, 6-month roadmap | `deliverables/remediation_plan.md` |
| 6 | **Model Risk Remediation Plan (PDF render)** | A PDF render of item 5, for offline reading | `deliverables/Model Risk Remediation Plan .pdf` |
| 7 | **Executive Summary** | The package-level navigational document — the 12 MAP deliverables, the two paradigms, the side-by-side verdicts | `deliverables/EXECUTIVE_SUMMARY.md` |

### Layer 2 — Governance framework (3 files in `AI Policy/`)

These are the **enterprise-level standards** the two projects are assessed against. They are not project-specific — they are the governance layer the projects sit inside.

| # | Document | Purpose | File |
|---|---|---|---|
| 8 | **AI Governance Policy** | The bank's enterprise AI/ML governance policy: six AI-specific risk categories, roles and responsibilities, four-tier risk classification, five deployment gates. Both projects are assessed against this policy. | `AI Policy/AI_GOVERNANCE_POLICY.md` |
| 9 | **Regulatory Gap Analysis (OSFI E-23)** | The gap analysis that maps OSFI E-23 requirements to the bank's controls. 27 of 32 requirements met (84%); 5 partially met; 0 not met. This is the artifact that makes the policy's E-23 alignment claim demonstrable. | `AI Policy/REGULATORY_GAP_ANALYSIS.md` |
| 10 | **AI Vendor Governance Review Template** | A repeatable process for assessing third-party AI vendors: evidence hierarchy, five-dimension scorecard, tier-based thresholds, conditions and monitoring plan. | `AI Policy/VENDOR_GOVERNANCE_REVIEW_TEMPLATE.md` |

### Layer 3 — Project governance artifacts (23 files across the two project repos)

Each project has its own `governance/` folder containing the artifacts that support the project's Validation Report or Stress Testing Framework. These follow the 12-deliverable MAP structure. **Both folders are now complete.**

**Fannie Mae** — 11 files in `governance/`:
`analytical-specification.md`, `approval-record.md`, `code-analysis-results.md`, `consolidated-findings-register.md`, `data-specification.md`, `decision-criteria-register.md`, `feature-decision-logs.md`, `methodology-document.md`, `problem-definition.md`, `remediation-plan.md`, `risk-validation-plan.md`.

**Lending Club** — 12 files in `governance/`:
`analysis-code-results.md`, `analytical-specification.md`, `approval-record.md`, `consolidated-findings-register.md`, `data-specifications.md`, `decision-criteria-register.md`, `features-decision-log.md`, `methodology-document.md`, `problem_definition.md`, `remediation-plan.md`, `risk-validation-plan.md`, `validation-opinion.md`.

### The README is the entry point to 30+ artifacts

A reader opening this package for the first time sees **32 files across three categories**. The README is the artifact that names them, groups them, and states the synthesis that connects them. It is not a deliverable in the same sense as the seven files in `deliverables/` — it is the **navigational artifact** that makes the other 32 files readable as a package.

The synthesis itself is in the "What this package demonstrates" section below.

---

## The twelve MAP deliverables — the per-project structure

Both projects use the same twelve-deliverable structure. **This is the per-project view** — each project's `governance/` folder contains the twelve artifacts. A reader who wants the package-level view reads the three layers above; a reader who wants the per-project view reads this table.

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
| 10 | **Validation Opinion** | Authors the verdict (the human judgment) | ✅ | **N/A — framework, not validated model** |
| 11 | **Approval Record** | Records the formal decision and signatures | ✅ | ✅ |
| 12 | **Analysis Code & Results** | Indexes the code and summarizes the results | ✅ | ✅ |

**On the Fannie Mae Validation Opinion.** The FM Validation Opinion is **not absent by accident** — it is **intentionally N/A**. The Fannie Mae project is a framework, not a validated model. A framework that has not been independently validated should not have a Validation Opinion claiming it has. The FM `README`'s "what this framework does NOT demonstrate" section is the definitive statement.

**On the Lending Club Validation Opinion.** The LC Validation Opinion **exists** (this session's earlier work). It is the one document the LC `governance/` folder was missing; it has now been drafted.

**Folder completeness.** Before this session, the FM `governance/` folder had 9 of the 12 deliverables and the LC `governance/` folder had 11 of the 12. **After this session, both folders are complete** — 10 of 12 in FM (with the Validation Opinion N/A) and 12 of 12 in LC.

---

## How to read this package

**If you have 5 minutes:** read the [`EXECUTIVE_SUMMARY.md`](deliverables/EXECUTIVE_SUMMARY.md) (the deliverable file, not this README's executive summary below), then the two project READMEs' "How to read this project" sections.

**If you have 30 minutes:** read the two project READMEs in full, then deliverable 2 (Validation Report) and deliverable 3 (Stress Testing Framework). Those are the analytical payloads.

**If you are reviewing for governance rigor:** read the three AI Policy documents (Layer 2 above), then the AI Interaction Record and Reproducibility Record. Those are where the audit trail lives — and where the enterprise-level standards the projects instantiate are stated.

**If you are a hiring manager:** the "What this demonstrates about the analyst" section at the bottom is written for you.

**If you want the synthesis:** read this README from start to finish. The "What this package demonstrates" section is the synthesis; the two layers of artifacts above are the parts.

**On the two executive summaries.** This README has its own "Executive summary" section below, and there is also an [`EXECUTIVE_SUMMARY.md`](deliverables/EXECUTIVE_SUMMARY.md) deliverable. **They are different documents with different jobs:**
- **This README's executive summary** is the **package-level summary** — it summarizes the two projects for a reader who wants a two-paragraph version of each.
- **The `EXECUTIVE_SUMMARY.md` deliverable** is the **navigational document** — it presents the twelve MAP deliverables per project, the two-paradigm narrative, and the side-by-side verdicts.

A reader who reads only one gets a coherent picture. A reader who reads both gets the picture at two registers.

---

## Executive summary

### Lending Club — the validation artifact

An independent validation of a consumer credit risk model, following OSFI E-23 and SR 11-7 principles. **The executive summary names the top five findings by severity; the full register has 11** (2 CRITICAL, 7 HIGH, 2 MEDIUM; 10 open, 1 resolved).

- **Data leakage:** nine post-origination features inflated the developer-reported AUC from 0.631 (realistic) to 0.865 (claimed) — a **27.1% inflation**. CRITICAL, resolved.
- **Severe disparate impact:** region-level DI = 0.5414 (SEVERE, below the 0.60 threshold). CRITICAL, open. **This is the primary driver of the REJECT verdict.**
- **Walk-forward split not implemented:** random stratified split used instead. HIGH, open.
- **IFRS 9 misalignment:** 16+ day default threshold vs. IFRS 9's 30+ day. HIGH, open.
- **Weak discrimination:** KS = 0.2671, below the conventional 0.30 "weak" threshold. HIGH, open.

**The remaining six findings** (macro factors missing, low precision, HL degeneracy, counterintuitive SHAP, foreign data applicability, protected-attribute-as-proxy) are in the register.

**Verdict: 6/10 → HIGH → REJECT.** The rejection is fairness-driven, not performance-driven. AUC 0.631 contributes only 1 of 6 points; fairness (3) and calibration (2) dominate.

### Fannie Mae — the framework artifact

An IFRS 9 ECL stress-testing framework on a 100,000-loan Fannie Mae sample. **The full register has 13 findings** (0 CRITICAL, 5 HIGH, 5 MEDIUM, 3 LOW; 13 documented, 0 open). The framework demonstrates:

- Three-stage IFRS 9 classification (Stage 1: 89.1%, Stage 2: 9.9%, Stage 3: 1.0%)
- PD/LGD/EAD calibration with documented assumptions (PD 0.95% unconditional, LGD 44.28%, EAD $204,745)
- Probability-weighted ECL across four scenarios (45/30/15/10 weights): **$2,231 per loan**
- **Coverage diagnostic** (not capital adequacy): ECL as % of total assets = 22.31% weighted, 75.12% tail

**Two findings the framework reports that are not in its headline numbers:**

- **The Severely Adverse scenario is 1.27× the 2008–2010 historical average, below the 1.5× target in the DCR.** The notebook logs an AP-05 warning and an IT-05 investigation trigger. The correct reading is: the assumed scenario multipliers produce a scenario the register considers *insufficiently severe*, not that the portfolio is safe.
- **The PD cap does not bind in this run** — Tail Risk PD (4.29%) is below the 20% cap, so the cap-sensitivity analysis reports +0.0% understatement.

**The framework is a methodology demonstration, not a validated model.** It has documented limitations: SICR-by-construction (Stage 2 = top-decile proxy), PD-cap tail understatement in the appropriate runs, EAD ratio outside configured band (86.95% vs. 50–85%), and no fairness testing possible (no protected attributes in the dataset).

**On the two counts.** The Lending Club total (11) and the Fannie Mae total (13) are **not the same kind of count.** The LC findings include CRITICAL defects (leakage, fairness); the FM findings are all documented limitations (0 CRITICAL). A reader who compares the two totals sees the volume; a reader who compares the severities sees the *kind*. **The two registers are different sizes because the two projects have different scopes, not because one project is better or worse than the other.**

---

## What this package demonstrates

The package demonstrates **model risk governance at two levels**. Reading the two projects alone shows the project level. Reading the three AI Policy documents alongside them shows the enterprise level. Reading both shows how the two levels connect.

### Project level — the two pipelines

- **Effective challenge.** The Lending Club validation challenges the developer's performance claim, quantifies the challenge (0.234 AUC points), and reaches a verdict that is not the developer's verdict.
- **Separation of duties.** The Lending Club verdict lives in the validation notebook; the governance notebook inherits it and does not re-derive it. The `performance_summary_v2.json` artifact records `authored_by: "NB03"` so the chain is auditable.
- **Claim-authorization discipline.** The Fannie Mae pipeline deliberately does not write a compliance verdict. Every compliance status field is an `[ANALYST: insert status]` placeholder. The analyst writes the verdict; the notebook produces the evidence.
- **Honest framing.** Both projects name their limitations prominently. The Lending Club README says "not as claimed; no; partially; and not without remediation." The Fannie Mae README says "what this project does NOT demonstrate" before it says what it does.
- **Reproducibility.** Every artifact carries `run_id`, `notebook_version`, and a SHA-256-16 hash. Every notebook has an audit log. Same data + same seed = same artifacts.

### Enterprise level — the governance framework

- **A written policy that the projects are assessed against.** The AI Governance Policy defines six AI-specific risk categories (data leakage, fairness, explainability, drift, claim-authorization, third-party dependency), the roles that own each, and the four-tier risk classification that determines the approval path.
- **A gap analysis that makes the policy's alignment claim demonstrable.** The Regulatory Gap Analysis maps OSFI E-23 to the bank's controls: 27 of 32 requirements met (84%), 5 partially met, 0 not met. **The 84% is not an assertion — it is a table a reviewer can audit.**
- **A repeatable process for the third-party AI risk the two projects don't cover.** The AI Vendor Governance Review Template provides the evidence hierarchy, five-dimension scorecard, and monitoring plan that any vendor assessment would use.

### The synthesis across both levels

**The principle: the tool does not write the verdict.** This principle appears at both levels, in different forms, with different enforcement mechanisms.

- **At the project level**, it appears as **verdict-ownership enforcement** (Lending Club: `authored_by: "NB03"`) and **claim-authorization enforcement** (Fannie Mae: `[ANALYST: insert status]`). A validation pipeline needs a verdict-ownership chain because *somebody* has to write the verdict; a framework pipeline needs a claim-authorization discipline because *nobody* should.
- **At the enterprise level**, it appears as **the policy's declaration of the principle** (AI Governance Policy §6.5, claim-authorization control) and **the gap analysis's demonstration that the principle is implemented** (Regulatory Gap Analysis, §6.2 of the mapping).

**What the package demonstrates that neither level alone does:** the enterprise standards are **implementable**. The policy says "the tool does not write the verdict"; the Lending Club pipeline implements it as `authored_by: "NB03"`; the Fannie Mae pipeline implements it as `[ANALYST: insert status]`. **The policy is not a wish; it is a standard with two working instances in this package.** That is the synthesis — and it is why the two-level structure is the package's central claim, not just its filing system.

**A reader who wants to check this claim** can trace it in the artifacts. Project level: `performance_summary_v2.json` in the Lending Club repo (the `authored_by: "NB03"` field), and `ifrs9_compliance_report_v1_2.txt` in the Fannie Mae repo (the `[ANALYST: insert status]` placeholders). Enterprise level: `AI Policy/AI_GOVERNANCE_POLICY.md` §6.5 (the control specification), and `AI Policy/REGULATORY_GAP_ANALYSIS.md` §6.2 (the evidence that the control is implemented). **The principle is not a claim about what the projects say; it is a claim about what the policies require and the projects do.**

---

## The two paradigms — model validation vs. methodology validation

The package demonstrates **two paradigms of model risk validation**. The two projects use the same 12-deliverable MAP structure, but the two paradigms produce different verdicts, different controls, and different remediations.

| Dimension | Lending Club (model validation) | Fannie Mae (methodology validation) |
|---|---|---|
| **What's validated** | A model | A methodology |
| **Verdict** | HIGH / REJECT | Accepted as a demonstration |
| **Primary driver** | Fairness (DI 0.5414, SEVERE) | N/A — limitations documented |
| **Critical findings** | 2 CRITICAL (leakage, fairness) | 0 |
| **The control** | Verdict-ownership chain | Parameter-freeze + claim-authorization |
| **The verdict location** | In the pipeline (NB03) | In the MAP document (Validation Opinion) |
| **The remediation** | 8 actions, 3-month critical path | Documentation only — no fixes needed |
| **The story** | A model that failed validation, with a clear path to remediation | A methodology that is defensible because its limitations are explicit, not because it has none |

**The single-sentence distinction:**

> *A model needs to be corrected; a methodology needs to be scoped. The Lending Club project shows the correction path (REJECT → 8 remediation actions → re-validation). The Fannie Mae project shows the scoping path (10 limitations documented → accepted as a demonstration). Both are necessary; both are demonstrated here.*

**The `EXECUTIVE_SUMMARY.md` deliverable presents the same two paradigms in more detail** — the per-project narratives, the "what this demonstrates" lists, and the reader guidance are all in the summary. This section of the README is the paradigm comparison; the summary is the paradigm narration.

---

## What this package does NOT demonstrate

- **Production model deployment.** Both projects are methodology demonstrations. Neither is a production model.
- **Regulatory compliance.** Compliance is a determination an institution makes against its obligations. A portfolio project cannot make that determination for itself, and these projects do not.
- **Independent validation of the Fannie Mae framework.** The Fannie Mae project is a framework, not a validated model. There is no second-line validation of it. **No Fannie Mae Validation Opinion exists in this package, because the Fannie Mae project is not a validated model — it is a framework with documented limitations.** This is a deliberate design decision, not an omission.
- **A completed Lending Club Validation Opinion.** The Validation Report (`deliverables/02_validation_report_lc.md`) is the evidence base. **The Validation Opinion — the signed, single-document verdict — has been drafted this session and is in the LC `governance/` folder.** The draft is the current state; the signed version is the next milestone.
- **Canadian applicability.** Both projects use U.S. data. Neither is validated for Canadian portfolios (OSFI E-23 scope restriction).

The distinction between "the Lending Club project is validated" and "the Fannie Mae project is a framework" is the most important thing to understand about this package. It is why only one Validation Report exists, and why the Fannie Mae Validation Opinion is intentionally absent.

---

## Related repositories

- [lending-club-model-validation](https://github.com/MiltonGreat/credit-risk-model-validation/blob/main/README.md) — the independent validation artifact
- [fannie-mae-ifrs9-framework](https://github.com/MiltonGreat/fannie-mae-ifrs9-portfolio/tree/main) — the stress-testing framework artifact

## License

MIT
