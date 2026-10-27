# Model Analysis Package — IFRS 9 ECL & Credit Model Validation

**A portfolio of two credit-risk projects and the five governance deliverables that connect them.**

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![IFRS 9](https://img.shields.io/badge/IFRS%209-Methodology%20Demo-orange)
![OSFI E-23](https://img.shields.io/badge/OSFI%20E--23-Aligned-lightgrey)
![SR 11-7](https://img.shields.io/badge/SR%2011--7-Partially%20Aligned-yellow)
![Status](https://img.shields.io/badge/Status-Portfolio%20Artifact-lightgrey)

---

## The business problem

A bank's model risk function has two questions to answer about any credit model before it can be deployed:

1. **Is the model fit for purpose?** (validation —> [Go to Lending Club repo](https://github.com/MiltonGreat/credit-risk-model-validation/blob/main/README.md))
2. **What does it mean for capital and provisioning under stress?** (framework —> [Go to Fannie Mae project](https://github.com/MiltonGreat/fannie-mae-ifrs9-portfolio/tree/main))

These are different questions, answered by different teams, under different regulatory frameworks. Most portfolio projects answer one or the other. This package answers both — and, critically, shows how the two answers connect through a shared governance layer.

**The story in one paragraph.** A model development team built a consumer credit risk model for collections prioritization. They reported AUC 0.865 and requested deployment. Independent validation found that nine post-origination features had inflated the reported performance by 27% (realistic AUC: 0.631), and that the model approved applicants in one U.S. region at 54% of the rate of the highest-approval region. The model was rejected. Separately, a mortgage ECL pipeline was built on Fannie Mae data to demonstrate IFRS 9 stress testing — and, in the process, surfaced a capital-adequacy framing error that would have been cited against the institution in a model risk finding. Both projects are methodology demonstrations, and both are honest about what they do and do not prove.

---

## What's in this package

Five deliverables, drawn from two project repositories:

| # | Deliverable | Scope | Where it lives |
|---|---|---|---|
| 1 | **Model Risk Remediation Plan** | Cross-project, 10 findings, 6-month roadmap | This repo: `deliverables/01_remediation_plan.md` |
| 2 | **Model Risk Validation Report** | Lending Club only (independent validation opinion) | This repo: `deliverables/02_validation_report_lc.md` |
| 3 | **IFRS 9 Stress Testing Framework** | Fannie Mae only (ECL + capital coverage) | This repo: `deliverables/03_stress_testing_framework_fm.md` |
| 4 | **AI Interaction Record** | Cross-project (one template, two instances) | This repo: `deliverables/04_ai_interaction_record.md` |
| 5 | **Reproducibility Record** | Cross-notebook (one per project + manifest) | This repo: `deliverables/05_reproducibility_record.md` |

**Two project repositories feed these deliverables:**

- [`lending-club-model-validation`](https://github.com/MiltonGreat/credit-risk-model-validation/blob/main/README.md) — the independent validation artifact. **This is where the validation verdict lives.**
- [`fannie-mae-ifrs9-framework`](https://github.com/MiltonGreat/fannie-mae-ifrs9-portfolio/tree/main) — the stress-testing framework artifact. **This is where the ECL methodology lives.**

---

## How to read this package

**If you have 5 minutes:** read the [Executive Summary](https://github.com/MiltonGreat/model-analysis-package/blob/main/deliverables/EXECUTIVE_SUMMARY.md) below, then the two project READMEs' "How to read this project" sections.

**If you have 30 minutes:** read the two project READMEs in full, then deliverable 2 (Validation Report) and deliverable 3 (Stress Testing Framework). Those are the analytical payloads.

**If you are reviewing for governance rigor:** read all five deliverables, then the AI Interaction Record and Reproducibility Record — those are where the audit trail lives.

**If you are a hiring manager:** the "What this demonstrates about the analyst" section at the bottom is written for you.

---

## Executive summary

### Lending Club — the validation artifact

An independent validation of a consumer credit risk model, following OSFI E-23 and SR 11-7 principles. The validation found:

- **Data leakage:** nine post-origination features inflated the developer-reported AUC from 0.631 (realistic) to 0.865 (claimed) — a **27.1% inflation**. CRITICAL, resolved.
- **Severe disparate impact:** region-level DI = 0.5414 (SEVERE, below the 0.60 threshold). CRITICAL, open. **This is the primary driver of the REJECT verdict.**
- **Walk-forward split not implemented:** random stratified split used instead. HIGH, open.
- **IFRS 9 misalignment:** 16+ day default threshold vs IFRS 9's 30+ day. HIGH, open.
- **Weak discrimination:** KS = 0.2671, below the conventional 0.30 "weak" threshold. HIGH, open.

**Verdict: 6/10 → HIGH → REJECT.** The rejection is fairness-driven, not performance-driven. AUC 0.631 contributes only 1 of 6 points; fairness (3) and calibration (2) dominate.

### Fannie Mae — the framework artifact

An IFRS 9 ECL stress-testing framework on a 100,000-loan Fannie Mae sample. The framework demonstrates:

- Three-stage IFRS 9 classification (Stage 1: 89.1%, Stage 2: 9.9%, Stage 3: 1.0%)
- PD/LGD/EAD calibration with documented assumptions (PD 0.95% unconditional, LGD 44.28%, EAD $204,745)
- Probability-weighted ECL across four scenarios (45/30/15/10 weights): **$2,231 per loan**
- **Coverage diagnostic** (not capital adequacy): ECL as % of total assets = 22.31% weighted, 75.12% tail

**The framework is a methodology demonstration, not a validated model.** It has documented limitations: SICR-by-construction (Stage 2 = top-decile proxy), PD-cap tail understatement (~30.7%), EAD ratio outside configured band (86.95% vs 50–85%), and no fairness testing possible (no protected attributes in the dataset).

---

## What this package demonstrates

The package is a demonstration of **model risk governance in practice**. It shows:

- **Effective challenge.** The Lending Club validation challenges the developer's performance claim, quantifies the challenge (0.234 AUC points), and reaches a verdict that is not the developer's verdict.
- **Separation of duties.** The Lending Club verdict lives in the validation notebook; the governance notebook inherits it and does not re-derive it. The `performance_summary_v2.json` artifact records `authored_by: "NB03"` so the chain is auditable.
- **Claim-authorization discipline.** The Fannie Mae pipeline deliberately does not write a compliance verdict. Every compliance status field is an `[ANALYST: insert status]` placeholder. The analyst writes the verdict; the notebook produces the evidence.
- **Honest framing.** Both projects name their limitations prominently. The Lending Club README says "not as claimed; no; partially; and not without remediation." The Fannie Mae README says "what this project does NOT demonstrate" before it says what it does.
- **Reproducibility.** Every artifact carries `run_id`, `notebook_version`, and a SHA-256-16 hash. Every notebook has an audit log. Same data + same seed = same artifacts.

---

## What this package does NOT demonstrate

- **Production model deployment.** Both projects are methodology demonstrations. Neither is a production model.
- **Regulatory compliance.** Compliance is a determination an institution makes against its obligations. A portfolio project cannot make that determination for itself, and these projects do not.
- **Independent validation of the Fannie Mae framework.** The Fannie Mae project is a framework, not a validated model. There is no second-line validation of it. **No Fannie Mae Validation Opinion exists in this package, because the Fannie Mae project is not a validated model — it is a framework with documented limitations.**
- **Canadian applicability.** Both projects use U.S. data. Neither is validated for Canadian portfolios (OSFI E-23 scope restriction).

The distinction between "the Lending Club project is validated" and "the Fannie Mae project is a framework" is the most important thing to understand about this package. It is why only one Validation Report exists.
