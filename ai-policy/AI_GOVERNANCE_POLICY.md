# AI Governance Policy

**Document ID:** POL-AI-001  
**Version:** 1.0  
**Review cycle:** Annual  
**Classification:** Internal  
**Related standards:** OSFI E-23 (Model Risk Management), ISO/IEC 42001 (AI Management Systems), SR 11-7 (Federal Reserve Model Risk Management), OSFI B-13 (Technology and Cyber Risk Management)

---

## 1. Purpose

This policy establishes the **enterprise governance framework for artificial intelligence (AI) and machine learning (ML) systems** used by the bank. It defines AI-specific risk categories, assigns governance roles and responsibilities, and establishes deployment gates that every AI system must pass before it can be used in a business process.

**The policy's premise:** AI systems introduce risks that traditional model risk management does not fully address — including data leakage, fairness, explainability, drift, third-party dependency, and the risk of the tool authoring its own verdict. **This policy extends the bank's existing model risk framework to cover those AI-specific risks explicitly.**

**The policy's scope:** all AI/ML systems — from a simple logistic regression used for collections prioritization to a large language model used for document summarization. The policy applies whether the system is **developed internally** or **acquired from a third party**.

---

## 2. Scope and applicability

### 2.1 In scope

| Category | Examples |
|---|---|
| **Predictive models** | Credit scoring, collections prioritization, fraud detection, churn prediction |
| **Generative AI** | LLM-based document summarization, code generation, customer service chatbots |
| **Decision-support systems** | Recommendation engines, pricing models, underwriting assistance |
| **Automated decisioning** | Any system that makes or informs a decision about a customer without human review |
| **Third-party AI** | Vendor-provided AI services integrated into bank processes |
| **AI-assisted workflows** | Human-in-the-loop systems where AI proposes and a human approves |

### 2.2 Out of scope

| Category | Reason |
|---|---|
| Traditional statistical models (e.g., linear regression without ML features) | Covered by the existing Model Risk Policy |
| Pure rule-based systems | Not AI — no learning, no probabilistic output |
| IT infrastructure (servers, networks) | Covered by OSFI B-13 |
| Data governance (data quality, lineage) | Covered by the Data Governance Policy |
| Cybersecurity | Covered by OSFI B-13 |

**Boundary cases:** a system that is primarily rule-based but includes a small ML component is **in scope** for the ML component. The rule-based portion is covered by the traditional framework; the ML portion by this policy.

### 2.3 Applicability matrix

| Business unit | Applicability | Notes |
|---|---|---|
| Retail banking (credit, collections, fraud) | **In scope** | All predictive models |
| Commercial banking | **In scope** | Credit models, relationship pricing |
| Wealth management | **In scope** | Robo-advisory, portfolio optimization |
| Operations | **In scope** | Document processing, workflow automation |
| HR | **In scope** | Resume screening, performance prediction |
| Legal / compliance | **Partial** | AI-assisted document review is in scope; legal judgment is not |
| IT | **Out of scope** | IT infrastructure is covered by OSFI B-13 |

---

## 3. AI-specific risk categories

Traditional model risk categories (performance, calibration, stability) are covered by the existing Model Risk Policy. **This policy adds six AI-specific risk categories** that are not fully addressed by the traditional framework:

### 3.1 Data leakage risk

**Definition:** the risk that a model uses information that would not be available at the moment of a real decision, inflating apparent performance and causing production failure.

**Example:** a collections model that uses `paid_total` (the amount the borrower eventually paid) as a feature. The feature is available in the training data, but not at the time of a collections decision.

**Control:** pre-registered leakage feature lists; mandatory leakage audit before any model is trained; reconciliation assertion between the leakage count in the data audit and the leakage count in the model development.

**Reference:** Lending Club project, F-03.01 (CRITICAL, RESOLVED); NB01 Phase 5; NB02 Phase 4.

### 3.2 Fairness and disparate impact risk

**Definition:** the risk that a model produces systematically different outcomes for different protected groups, violating fair lending or human rights obligations.

**Example:** a credit model that approves applicants from one region at a lower rate than applicants from another region, where region is a proxy for a protected class.

**Control:** mandatory fairness testing before any model is deployed; FD-05-compliant 4/5ths rule at low cardinality; documented treatment of high-cardinality attributes (region, state) as diagnostic, not binding.

**Reference:** Lending Club project, F-03.03 (CRITICAL, OPEN); NB03 Phase 10; German Credit cross-validation, NB05.

### 3.3 Explainability risk

**Definition:** the risk that a model's decisions cannot be explained to a customer, regulator, or internal reviewer, making the model indefensible if challenged.

**Example:** a black-box gradient boosting model whose predictions cannot be explained to a customer who was declined.

**Control:** mandatory SHAP analysis for any model that informs a customer-facing decision; monotonicity check against domain theory; documented explanation path for every model.

**Reference:** Lending Club project, F-03.07 (HIGH, OPEN); NB03 Phase 7.

### 3.4 Drift and stability risk

**Definition:** the risk that a model's performance degrades over time as the population or the relationship between features and outcomes changes.

**Example:** a credit model trained on 2018 data whose performance degrades in 2020 because the economic environment changed.

**Control:** mandatory PSI (Population Stability Index) monitoring for any model that has been in production for 6+ months; time-based validation whenever a usable date column exists; documented limitation when the data does not support time-based testing.

**Reference:** Lending Club project, F-03.02 (HIGH, OPEN); NB03 Phase 6 (PSI `not_assessed`); Fannie Mae project, L2 (age curve truncation).

### 3.5 Claim-authorization risk

**Definition:** the risk that the AI tool or the model pipeline **authors a verdict, compliance determination, or judgment** that should be authored by a human. This is unique to AI systems, because the tool can produce language that looks authoritative.

**Example:** a model pipeline that writes *"the model is compliant with OSFI E-23"* in its report — a claim the tool is not authorized to make.

**Control:** mandatory claim-authorization guardrail for any AI-generated report; the report must contain placeholders for the analyst's verdict, not the tool's; the analyst must sign off on every compliance determination.

**Reference:** Fannie Mae project, E-N05-04 (claim-authorization self-check); Lending Club project, NB03 Phase 14 (`authored_by: "NB03"` assertion); AI Interaction Record.

### 3.6 Third-party AI dependency risk

**Definition:** the risk that the bank's AI system depends on a third-party model (LLM, vendor API, pre-trained embedding) whose behavior can change without notice, whose data handling is opaque, or whose liability is unclear.

**Example:** a document-processing pipeline that uses a third-party LLM API. The vendor updates the model, the bank's outputs change, and the bank cannot reproduce the prior behavior.

**Control:** mandatory vendor assessment before any third-party AI is integrated; documented version pinning; fallback path if the vendor changes the model; contractual right to audit; data residency and privacy review.

**Reference:** this policy, §7 (third-party AI); not covered by Lending Club or Fannie Mae projects (both use open datasets and no third-party AI).

---

## 4. Governance roles and responsibilities

### 4.1 The three-lines-of-defense model

AI governance at the bank follows the **three lines of defense** model, adapted for AI-specific risks:

| Line | Role | Responsibility |
|---|---|---|
| **First line** | Business unit / Model developer | Builds the AI system; owns the model; implements controls; documents the model |
| **Second line** | Model Risk Management / AI Governance | Sets policy; reviews and challenges; validates models independently; reports to the board |
| **Third line** | Internal Audit | Audits the first and second lines; reports to the board audit committee |

### 4.2 AI-specific roles

| Role | Reports to | Responsibility |
|---|---|---|
| **Chief AI Officer (CAIO)** | CEO / Board | Owns the AI strategy; accountable for the AI governance framework |
| **Head of AI Governance** | CAIO / CRO | Owns this policy; chairs the AI Governance Committee; reports AI risk to the board |
| **AI Model Validator** | Head of AI Governance | Independently validates AI models; authors the Validation Opinion |
| **AI Ethics Officer** | CAIO / General Counsel | Reviews fairness, bias, and human rights impacts |
| **Data Protection Officer** | General Counsel | Reviews privacy and data residency for AI systems |
| **AI Governance Committee** | Board Risk Committee | Cross-functional committee that approves AI deployments and reviews AI risk |
| **Model Risk Committee (MRC)** | Board Risk Committee | Approves or rejects model deployments (existing role, extended to AI) |

### 4.3 Decision authority matrix

| Decision | Business unit | AI Governance | MRC | Board |
|---|---|---|---|---|
| Build a prototype | **Yes** | Notify | No | No |
| Deploy a low-risk model | Propose | **Approve** | Notify | No |
| Deploy a high-risk model | Propose | Review | **Approve** | Notify |
| Deploy a critical-risk model | Propose | Review | Review | **Approve** |
| Change a model's risk tier | Propose | **Approve** | Notify | No |
| Decommission a model | **Yes** | Notify | Notify | No |
| Override a validation verdict | No | No | **Yes** (with rationale) | Notify |

**The risk tier determines the approval path.** Low-risk models are approved by AI Governance alone; high-risk models require MRC approval; critical-risk models require board approval. **The tier is set by the risk classification in §5.**

### 4.4 Separation of duties

| Role | Cannot do |
|---|---|
| Business unit / developer | Approve their own model; author their own validation opinion |
| AI Governance | Build the model they govern; override the validator's verdict |
| MRC | Build the model; author the validation opinion |
| Board | Build the model; approve a model without MRC recommendation |

**The separation of duties is the policy's core control.** No single role can build, validate, approve, and deploy an AI system.

---

## 5. AI risk classification and deployment gates

### 5.1 Risk tier definitions

Every AI system is classified into one of four **risk tiers** before development begins. The tier determines the approval path, the validation requirements, and the deployment gates.

| Tier | Definition | Examples | Approval |
|---|---|---|---|
| **Tier 1 — Critical** | AI system that makes or informs decisions with material financial, legal, or human-rights impact | Credit approval, collections prioritization, fraud blocking, AML | Board + MRC |
| **Tier 2 — High** | AI system that informs decisions with significant operational or customer impact | Pricing, underwriting assistance, customer segmentation, collections ranking | MRC + AI Governance |
| **Tier 3 — Moderate** | AI system that informs decisions with limited impact | Marketing targeting, internal workflow prioritization, document routing | AI Governance |
| **Tier 4 — Low** | AI system with no customer impact and no decisioning role | Internal search, code assistance, draft summarization | Business unit + AI Governance notification |

**The tier is determined by the highest impact of the AI system, not the average.** A model that is Tier 3 on average but Tier 1 for 1% of decisions is **Tier 1**.

### 5.2 Deployment gates

Every AI system must pass **five gates** before deployment. The gates are cumulative — a Tier 1 model must pass all five; a Tier 4 model must pass gates 1 and 5.

| Gate | Requirement | Evidence | Applies to |
|---|---|---|---|
| **Gate 1 — Problem definition** | The problem, target, scope, and success criteria are documented | Problem Definition Record | All tiers |
| **Gate 2 — Data specification** | The data source, quality, leakage, and limitations are documented | Data Specification; leakage audit | All tiers |
| **Gate 3 — Methodology validation** | The model or methodology has been independently validated | Validation Opinion | Tier 1, 2, 3 |
| **Gate 4 — Governance approval** | The model has been approved by the required authority | Approval Record | Tier 1, 2 |
| **Gate 5 — Deployment readiness** | The model is reproducible, monitored, and documented | Reproducibility Record; monitoring plan | All tiers |

**A model that fails any gate cannot be deployed.** A model that passes all gates is **approved** — but approval is scoped: it covers the specific use case, not any use of the model.

### 5.3 Deployment gate evidence

For each gate, the evidence must be:

- **Documented** in the MAP (Model Analysis Package)
- **Signed** by the accountable role
- **Reproducible** from the artifacts alone
- **Traceable** to the validation pipeline (if the model was validated)

**A gate that is documented but not signed is not passed.** A gate that is signed but not reproducible is not passed. **All four conditions are required.**

---

## 6. AI-specific controls

### 6.1 Leakage control

- **Pre-registered leakage list:** every model must have a leakage feature list, frozen before data inspection.
- **Mandatory leakage audit:** the data audit must identify leakage features and produce a `leakage_findings.csv` artifact.
- **Reconciliation assertion:** the model development must reconcile its leakage count against the data audit's count. A mismatch is a CRITICAL finding.
- **Independent verification:** the validator must recompute the leakage count from the data, not trust the developer's count.

**Reference:** Lending Club project, F-03.01, NB01 Phase 5, NB02 Phase 4, NB03 Phase 4.

### 6.2 Fairness control

- **Mandatory fairness testing:** every model that makes or informs a customer-facing decision must be tested for disparate impact.
- **FD-05-compliant test:** the fairness test must use the 4/5ths rule at a cardinality of 50 or fewer. Higher-cardinality attributes are diagnostic, not binding.
- **FD-03 group-size rule:** groups with N < 30 are excluded from the DI calculation.
- **Documented limitation:** if the model has no protected attributes, fairness is documented as a limitation, not as "passed."

**Reference:** Lending Club project, F-03.03, NB03 Phase 10; Fannie Mae project, L7.

### 6.3 Explainability control

- **SHAP analysis:** every model that informs a customer-facing decision must have a SHAP analysis.
- **Monotonicity check:** the SHAP direction must be checked against domain theory. Counterintuitive features are HIGH findings.
- **Explanation path:** every model must have a documented explanation path (how a decision would be explained to a customer).

**Reference:** Lending Club project, F-03.07, NB03 Phase 7.

### 6.4 Drift and monitoring control

- **PSI monitoring:** any model in production for 6+ months must have PSI monitoring.
- **Time-based validation:** if a usable date column exists, the validation must be time-based (walk-forward). If not, the limitation is documented.
- **Monthly review:** the model's performance metrics are reviewed monthly by AI Governance.

**Reference:** Lending Club project, F-03.02, NB03 Phase 6; Fannie Mae project, L2.

### 6.5 Claim-authorization control

- **No verdict by the tool:** any AI-generated report must contain placeholders for the analyst's verdict, not the tool's.
- **Self-check:** the report must have a self-check that fails if the report contains verdict tokens ("Compliant," "PASS," "Validated").
- **Analyst sign-off:** every compliance determination must be signed by the analyst, not the tool.

**Reference:** Fannie Mae project, E-N05-04; Lending Club project, NB03 Phase 14.

### 6.6 Third-party AI control

- **Vendor assessment:** any third-party AI must be assessed for security, data handling, model stability, and liability.
- **Version pinning:** the third-party model version must be pinned, and changes must be re-validated.
- **Fallback path:** the bank must have a fallback if the vendor changes the model or the service is unavailable.
- **Data residency:** the vendor's data handling must comply with the bank's data residency requirements.

**Reference:** this policy, §7.

---

## 7. Third-party AI

Third-party AI systems are **in scope** for this policy, with additional requirements:

### 7.1 Vendor assessment

Before any third-party AI is integrated, the vendor must be assessed for:

| Dimension | Requirement |
|---|---|
| **Security** | SOC 2 Type II or equivalent; penetration test; incident response plan |
| **Data handling** | Data residency; retention; deletion; no training on bank data without consent |
| **Model stability** | Version pinning; change notification; re-validation right |
| **Liability** | Contractual liability for model errors; indemnification |
| **Audit** | Right to audit the vendor's model and data handling |

### 7.2 Integration requirements

- The third-party model must be **wrapped** in the bank's own validation pipeline — the bank's AI Governance team validates the wrapped model, not the raw vendor model.
- The wrapper must document the vendor's version, the input/output schema, and the fallback path.
- The bank's model risk tier is determined by the **use case**, not by the vendor's tier.

### 7.3 Ongoing monitoring

- The bank must monitor the vendor's version changes and re-validate the model after any change.
- The bank must monitor the model's performance in the bank's own environment, not just the vendor's benchmark.

---

## 8. Regulatory alignment

This policy is aligned with three regulatory frameworks:

### 8.1 OSFI E-23 (Model Risk Management)

| E-23 Principle | Policy section | Alignment |
|---|---|---|
| Pillar 1 — Model Development | §5 (gates), §6 (controls) | Model design, data, and implementation are covered by Gates 1–2 |
| Pillar 2 — Model Risk Governance | §4 (roles), §4.3 (authority) | Three-lines-of-defense model; MRC authority |
| Pillar 3 — Model Inventory & Validation | §5 (tier), §5.2 (gates) | Model tier drives validation requirements |
| Pillar 4 — Model Risk Reporting | §4.2 (roles), §6.4 (monitoring) | AI Governance reports to board |

### 8.2 ISO/IEC 42001 (AI Management Systems)

| ISO 42001 Clause | Policy section | Alignment |
|---|---|---|
| 4. Context of the organization | §2 (scope), §3 (risks) | AI-specific risk categories |
| 5. Leadership | §4 (roles) | CAIO, AI Governance Committee |
| 6. Planning | §5 (tier), §5.2 (gates) | Risk tier and deployment gates |
| 7. Support | §4 (roles), §6 (controls) | Training, awareness, documentation |
| 8. Operation | §5 (gates), §6 (controls) | Operational controls |
| 9. Performance evaluation | §6.4 (monitoring) | Monitoring and reporting |
| 10. Improvement | §9 (review) | Annual review cycle |

### 8.3 SR 11-7 (Federal Reserve Model Risk Management)

| SR 11-7 Principle | Policy section | Alignment |
|---|---|---|
| Model development | §5 (gates) | Gate 1–2 |
| Model validation | §5.2 (gate 3) | Independent validation |
| Model governance | §4 (roles) | Three-lines-of-defense |
| Model inventory | §5 (tier) | Risk classification |
| Model documentation | §5.2 (gates), §6 (controls) | Documentation requirements |

**The policy is aligned with all three frameworks, not just one.** A regulator reading the policy can find the mapping for OSFI E-23, ISO 42001, or SR 11-7.

---

## 9. Policy review and amendment

### 9.1 Review cycle

- **Annual review:** the policy is reviewed annually by the AI Governance Committee.
- **Event-driven review:** the policy is reviewed after any material change to the regulatory environment, the bank's AI portfolio, or a significant AI incident.
- **Version control:** every version is recorded in the policy log; changes require AI Governance Committee approval.

### 9.2 Amendment authority

| Change | Proposer | Approver |
|---|---|---|
| Minor clarification | AI Governance | Head of AI Governance |
| New AI-specific control | AI Governance | AI Governance Committee |
| Change to risk tier definitions | AI Governance | AI Governance Committee + CRO |
| Change to deployment gates | AI Governance | AI Governance Committee + Board Risk Committee |
| Change to scope | AI Governance | Board |

**No single role can change the policy unilaterally.** The amendment authority is distributed across the governance hierarchy.

### 9.3 Policy exceptions

**Exceptions to this policy are not permitted** for Tier 1 (critical) AI systems. For Tier 2–4 systems, exceptions may be granted by the AI Governance Committee, with documented rationale, a time limit, and a remediation plan.

**An exception is not a waiver of the control — it is a documented, time-bound deviation.**

---

## 10. Incident response

### 10.1 AI incidents

An AI incident is any of the following:

- A model produces a systematically incorrect output (e.g., a credit model approves an unqualified cohort)
- A model is found to have a leakage feature that was missed in validation
- A model is found to have a fairness violation that was missed in validation
- A third-party AI model changes behavior without notice
- A model's performance degrades beyond the monitoring threshold
- A model produces an unauthorized verdict or compliance determination

### 10.2 Incident response

| Step | Action | Owner | Timeline |
|---|---|---|---|
| 1. Detect | Monitor, alert, or report | AI Governance | Immediate |
| 2. Contain | Pause the model or limit its scope | Business unit | 24 hours |
| 3. Assess | Determine the severity, scope, and impact | AI Governance | 72 hours |
| 4. Report | Notify the MRC and, if material, the board | Head of AI Governance | 1 week |
| 5. Remediate | Fix the root cause; re-validate | Business unit + Validator | Per remediation plan |
| 6. Close | Confirm the fix; document the incident | AI Governance | After re-validation |

**The incident response is mandatory for Tier 1 and Tier 2 models.** For Tier 3–4, the response is scaled to the incident's impact.

---

## Document control

| Field | Value |
|---|---|
| **Document ID** | POL-AI-001 |
| **Version** | 1.0 |
| **Status** | Approved |
| **Supersedes** | None (first version) |
| **Related documents** | Model Risk Policy, Data Governance Policy, OSFI B-13 Technology Risk Policy, AI Ethics Framework |
| **Classification** | Internal |
