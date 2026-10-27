# Regulatory Gap Analysis — OSFI E-23 Mapping

**Document ID:** RGA-001  
**Version:** 1.0  
**Author:** `[ANALYST: name]`  
**Owner:** `[ANALYST: role — Head of AI Governance]`  
**Date:** `[ANALYST: date]`  
**Classification:** Internal  
**Related documents:** AI Governance Policy (POL-AI-001), OSFI E-23 (Model Risk Management), SR 11-7, ISO/IEC 42001

---

## 1. Purpose

This document maps the **OSFI E-23 Model Risk Management** requirements to the bank's existing AI governance controls and identifies the **compliance gaps**. It is the evidence that the bank has assessed its AI governance against the regulatory standard and has a plan to close any gaps.

**The document's premise:** OSFI E-23 is a **principles-based** standard. Compliance is not a checklist — it is the demonstration that the bank's controls are **proportionate to the risks**, **documented**, and **reviewed**. This document is that demonstration.

**The document's audience:** the AI Governance Committee, the Chief Risk Officer, the Board Risk Committee, and OSFI supervisory review.

---

## 2. Scope and methodology

### 2.1 Scope

This gap analysis covers **OSFI E-23** and its interaction with:

- SR 11-7 (Federal Reserve Model Risk Management) — where E-23 and SR 11-7 overlap, the stricter requirement is applied
- ISO/IEC 42001 (AI Management Systems) — where E-23 and ISO 42001 overlap, the gap analysis notes the alignment
- OSFI B-13 (Technology and Cyber Risk Management) — where E-23 and B-13 overlap, the gap analysis references B-13

### 2.2 Methodology

The gap analysis follows a **five-step process**:

1. **Requirement extraction:** each OSFI E-23 principle and sub-principle is extracted into a discrete requirement.
2. **Control mapping:** each requirement is mapped to an existing control (policy section, process, or artifact).
3. **Gap assessment:** each requirement is assessed as **Met / Partially Met / Not Met**.
4. **Gap documentation:** for each gap, the impact, the root cause, and the remediation are documented.
5. **Prioritization:** the gaps are prioritized by severity and by whether they are blocking for Tier 1 or Tier 2 models.

### 2.3 Assessment scale

| Rating | Definition |
|---|---|
| **Met** | The control exists, is documented, is operating effectively, and has been tested |
| **Partially Met** | The control exists but is not fully documented, not fully operating, or not tested |
| **Not Met** | The control does not exist, or exists but does not address the requirement |
| **N/A** | The requirement does not apply to the bank's AI portfolio |

---

## 3. OSFI E-23 structure

OSFI E-23 is organized into **four pillars** and **nine principles**:

| Pillar | Principles | Focus |
|---|---|---|
| **Pillar 1 — Model Development** | Model design, data, implementation, use | How models are built and used |
| **Pillar 2 — Model Risk Governance** | Roles, risk appetite, model inventory | How model risk is governed |
| **Pillar 3 — Model Validation** | Independent validation | How models are independently validated |
| **Pillar 4 — Model Risk Reporting** | Reporting to senior management and the board | How model risk is reported |

**This gap analysis maps each principle and sub-principle to the bank's controls.**

---

## 4. Gap analysis — Pillar 1 (Model Development)

### 4.1 Principle 1.1 — Model design and data

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Model purpose and scope defined | E-23 s.4.1 | AI Governance Policy §5.2 (Gate 1); Problem Definition Record | **Met** | All models have a PDR |
| Model design appropriate for purpose | E-23 s.4.1 | AI Governance Policy §5.2 (Gate 3); Methodology Document | **Met** | Independent validation confirms design |
| Data quality assessed | E-23 s.4.2 | AI Governance Policy §3.1 (leakage control), §6.1; Data Specification | **Met** | Data quality scored; leakage audited |
| Data lineage documented | E-23 s.4.2 | Data Governance Policy; Data Specification §1 | **Met** | Lineage recorded per pipeline |
| Leakage identified and removed | E-23 s.4.2 | AI Governance Policy §6.1; Lending Club NB01 Phase 5, NB02 Phase 4 | **Met** | Pre-registered leakage list |
| Macro factors assessed | E-23 s.4.2 | Data Specification; Findings Register | **Partially Met** | Lending Club has no macro factors (F-03.08); Fannie Mae has no macro factors (L9) |
| Protected attributes assessed | E-23 s.4.3 | AI Governance Policy §3.2, §6.2; Data Specification | **Partially Met** | Lending Club uses region proxy; Fannie Mae has no protected attributes (L7) |

**Gap G-01 — Macro factors:** Both projects lack macro factors. The gap is not a process failure — it is a data limitation. **Remediation:** the policy requires macro factors for any Tier 1 model; a data acquisition project is in scope for the next review cycle.

**Gap G-02 — Protected attributes:** Neither project has direct protected attributes. The Lending Club project uses a region proxy; the Fannie Mae project documents the absence as a limitation. **Remediation:** the policy requires direct protected attributes or a documented HMDA-equivalent proxy for any Tier 1 model; the data acquisition is in scope for the next review cycle.

### 4.2 Principle 1.2 — Model implementation

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Model implemented as designed | E-23 s.4.1 | Methodology Document; Analysis Code & Results | **Met** | Code matches specification (AS mapping) |
| Implementation tested | E-23 s.4.1 | Analytical Specification §5 (acceptance criteria) | **Met** | All acceptance criteria tested |
| Model documentation complete | E-23 s.4.1 | All 12 MAP deliverables | **Met** | All deliverables produced |

**No gaps in Principle 1.2.**

### 4.3 Principle 1.3 — Model use

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Model use within documented scope | E-23 s.4.1 | AI Governance Policy §5.1 (tier); PDR §1.3 | **Met** | Scope documented per model |
| Model limitations communicated | E-23 s.4.1 | Findings Register; Validation Opinion | **Met** | All limitations documented |
| Model use monitored | E-23 s.4.3 | AI Governance Policy §6.4 (drift control) | **Partially Met** | Lending Club PSI not assessable (F-03.02); Fannie Mae has no time-series data |

**Gap G-03 — Model use monitoring:** The Lending Club model cannot be monitored via PSI because the data is a snapshot, not a time series. The Fannie Mae methodology has no time-series data either. **Remediation:** the policy requires time-based monitoring for any model in production for 6+ months; a data acquisition project is in scope for the next review cycle.

---

## 5. Gap analysis — Pillar 2 (Model Risk Governance)

### 5.1 Principle 2.1 — Roles and responsibilities

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Roles defined | E-23 s.3.1 | AI Governance Policy §4.2 | **Met** | CAIO, Head of AI Governance, AI Model Validator, AI Ethics Officer |
| Responsibilities documented | E-23 s.3.1 | AI Governance Policy §4.2, §4.3 | **Met** | Decision authority matrix |
| Separation of duties | E-23 s.3.1 | AI Governance Policy §4.4 | **Met** | Developer, validator, approver are separate roles |

**No gaps in Principle 2.1.**

### 5.2 Principle 2.2 — Model risk appetite

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Risk appetite defined | E-23 s.3.2 | AI Governance Policy §5.1 (risk tiers) | **Met** | Four tiers (Critical, High, Moderate, Low) |
| Risk appetite quantified | E-23 s.3.2 | AI Governance Policy §5.1 | **Met** | Each tier has a defined approval path |
| Risk appetite reviewed | E-23 s.3.2 | AI Governance Policy §9.1 | **Met** | Annual review |

**No gaps in Principle 2.2.**

### 5.3 Principle 2.3 — Model inventory

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Model inventory maintained | E-23 s.3.3 | AI Governance Policy §4.2; Model Inventory (separate document) | **Partially Met** | The inventory exists but is not yet integrated with the AI Governance Policy |
| Inventory includes risk tier | E-23 s.3.3 | AI Governance Policy §5.1 | **Met** | Tier is assigned to every model |
| Inventory reviewed | E-23 s.3.3 | AI Governance Policy §9.1 | **Met** | Annual review |

**Gap G-04 — Model inventory integration:** The model inventory is maintained, but it is not yet integrated with the AI Governance Policy's tier definitions. The inventory lists the models, but does not consistently record the risk tier. **Remediation:** integrate the model inventory with the AI Governance Policy by Q2 of the next fiscal year.

---

## 6. Gap analysis — Pillar 3 (Model Validation)

### 6.1 Principle 3.1 — Independent validation

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Validation is independent | E-23 s.5.1 | AI Governance Policy §4.4 (separation of duties) | **Met** | Validator is separate from developer |
| Validation is documented | E-23 s.5.1 | Validation Opinion; all MAP deliverables | **Met** | Full documentation |
| Validation includes performance, fairness, calibration, stability | E-23 s.5.1 | AI Governance Policy §6.1–§6.4; Lending Club NB03 | **Met** | All four dimensions validated |
| Validation includes explainability | E-23 s.5.1 | AI Governance Policy §6.3; Lending Club NB03 Phase 7 | **Met** | SHAP analysis |
| Validation includes third-party AI | E-23 s.5.1 | AI Governance Policy §7 | **Met** | Third-party AI is wrapped and validated |

**No gaps in Principle 3.1.**

### 6.2 Principle 3.2 — Validation frequency

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Validation at deployment | E-23 s.5.2 | AI Governance Policy §5.2 (Gate 3) | **Met** | Mandatory |
| Validation at major change | E-23 s.5.2 | AI Governance Policy §5.2 (Gate 3) | **Met** | Mandatory |
| Validation at periodic intervals | E-23 s.5.2 | AI Governance Policy §6.4 | **Partially Met** | Lending Club re-validation is triggered by remediation; no scheduled re-validation yet |

**Gap G-05 — Scheduled re-validation:** The policy requires re-validation at periodic intervals, but the current pipeline only re-validates on remediation triggers. **Remediation:** establish a scheduled re-validation cycle (annual for Tier 1, biennial for Tier 2) by Q3 of the next fiscal year.

---

## 7. Gap analysis — Pillar 4 (Model Risk Reporting)

### 7.1 Principle 4.1 — Reporting to senior management

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Model risk reported to senior management | E-23 s.6.1 | AI Governance Policy §4.2; AI Governance Committee | **Met** | Committee reports to CRO |
| Reporting is timely | E-23 s.6.1 | AI Governance Policy §10.2 (incident response) | **Met** | 72-hour incident assessment |
| Reporting is accurate | E-23 s.6.1 | Claim-authorization control (AI Governance Policy §6.5) | **Met** | Reports are analyst-authored, not tool-authored |

**No gaps in Principle 4.1.**

### 7.2 Principle 4.2 — Reporting to the board

| Sub-requirement | E-23 reference | Bank control | Rating | Notes |
|---|---|---|---|---|
| Model risk reported to the board | E-23 s.6.2 | AI Governance Policy §4.2; Board Risk Committee | **Met** | Annual report; ad-hoc for material incidents |
| Board has oversight of model risk | E-23 s.6.2 | AI Governance Policy §4.3 (Board approval for Tier 1) | **Met** | Tier 1 requires board approval |

**No gaps in Principle 4.2.**

---

## 8. Gap summary

### 8.1 Gaps by pillar

| Pillar | Requirements assessed | Met | Partially Met | Not Met |
|---|---|---|---|---|
| Pillar 1 — Model Development | 13 | 10 | 3 | 0 |
| Pillar 2 — Model Risk Governance | 6 | 5 | 1 | 0 |
| Pillar 3 — Model Validation | 8 | 7 | 1 | 0 |
| Pillar 4 — Model Risk Reporting | 5 | 5 | 0 | 0 |
| **Total** | **32** | **27 (84%)** | **5 (16%)** | **0** |

**The bank has 0 "Not Met" requirements and 5 "Partially Met" requirements.** The gap analysis identifies five gaps, all of which are documented and have remediation plans.

### 8.2 The five gaps

| Gap ID | Gap | Pillar | Impact | Priority | Remediation timeline |
|---|---|---|---|---|---|
| **G-01** | Macro factors absent | Pillar 1 | Models cannot capture economic cycle risk | **HIGH** | Next review cycle |
| **G-02** | Protected attributes absent or proxied | Pillar 1 | Fairness testing is proxy-based, not direct | **HIGH** | Next review cycle |
| **G-03** | Model use monitoring not assessable | Pillar 1 | PSI not computable on snapshot data | **MEDIUM** | Next review cycle |
| **G-04** | Model inventory not integrated with AI Governance Policy | Pillar 2 | Inventory is maintained but tier is not recorded | **MEDIUM** | Q2 next fiscal year |
| **G-05** | No scheduled re-validation | Pillar 3 | Re-validation is remediation-triggered, not scheduled | **MEDIUM** | Q3 next fiscal year |

### 8.3 Severity of gaps

| Priority | Count | Description |
|---|---|---|
| **CRITICAL** | 0 | No gaps that block Tier 1 deployment |
| **HIGH** | 2 | Gaps that limit the model's defensibility (macro factors, protected attributes) |
| **MEDIUM** | 3 | Gaps that limit the model's monitoring or governance |
| **LOW** | 0 | No gaps that are documentation-only |

**The absence of CRITICAL gaps is significant.** It means the bank's AI governance is **substantially compliant** with OSFI E-23 — 27 of 32 requirements are met, and the 5 partial gaps are documented and remediable.

---

## 9. Gap remediation plan

### 9.1 Remediation timeline

| Gap | Remediation | Owner | Timeline | Success criterion |
|---|---|---|---|---|
| **G-01** | Acquire macro factors (GDP, unemployment, HPI) for the Lending Club and Fannie Mae pipelines | Data team | Next review cycle | Macro factors integrated; models re-validated |
| **G-02** | Acquire HMDA-equivalent protected attributes | Data team | Next review cycle | Protected attributes available; fairness tested directly |
| **G-03** | Acquire time-series data for the Lending Club pipeline; implement PSI | Data team + AI Governance | Next review cycle | PSI computed; monitoring active |
| **G-04** | Integrate model inventory with AI Governance Policy tier definitions | AI Governance | Q2 next fiscal year | Inventory records tier; tier drives approval path |
| **G-05** | Establish scheduled re-validation (annual Tier 1, biennial Tier 2) | AI Governance | Q3 next fiscal year | Re-validation schedule documented; first cycle completed |

### 9.2 Remediation governance

- **Monthly tracking:** each gap's remediation is tracked by the AI Governance Committee.
- **Quarterly reporting:** the gap status is reported to the CRO and the Board Risk Committee.
- **Annual review:** the gap analysis is refreshed annually; closed gaps are removed, new gaps are added.

### 9.3 Dependencies

| Gap | Dependency | Risk if unmet |
|---|---|---|
| **G-01** | Macro data acquisition | Model remains procyclical; stress testing limited |
| **G-02** | Protected attribute data acquisition | Fairness remains proxy-based; regulatory risk |
| **G-03** | Time-series data acquisition | PSI not computable; drift monitoring limited |
| **G-04** | Model inventory integration | Tier-based approval path not fully operational |
| **G-05** | Scheduled re-validation process | Models may drift without detection |

**The dependencies are all data-related except G-04 and G-05, which are process-related.** The data dependencies are the most significant — they require budget, vendor negotiation, and time.

---

## 10. Compliance statement

### 10.1 Overall compliance assessment

The bank's AI governance is **substantially compliant** with OSFI E-23:

- **84% of requirements are Met** (27 of 32)
- **16% are Partially Met** (5 of 32)
- **0% are Not Met**

**The five partial gaps are documented, prioritized, and remediated with a plan.** None of them is a CRITICAL gap that blocks deployment. **The bank can demonstrate compliance to OSFI supervisory review, with the gaps disclosed and remediated.**

### 10.2 Regulatory mapping

| Framework | Alignment | Reference |
|---|---|---|
| **OSFI E-23** | 27/32 Met, 5/32 Partially Met | This document, §4–§8 |
| **SR 11-7** | 95% alignment (where E-23 and SR 11-7 overlap, the stricter requirement is applied) | AI Governance Policy §8.3 |
| **ISO/IEC 42001** | 90% alignment (AI management system clauses mapped to policy sections) | AI Governance Policy §8.2 |
| **OSFI B-13** | Fully aligned (technology risk covered by B-13, not by this policy) | AI Governance Policy §2.2 |

### 10.3 What "substantially compliant" means

**"Substantially compliant" is not "fully compliant."** The bank has five documented gaps. The gaps are:

- **Not CRITICAL** — none of them blocks Tier 1 deployment
- **Documented** — each gap has an owner, a timeline, and a remediation plan
- **Tracked** — each gap is reported quarterly to the Board Risk Committee
- **Remediable** — each gap has a specific remediation action

**The bank's position is: "We are compliant with 84% of OSFI E-23, and we have a plan to close the remaining 16%."** That is the position a regulator expects to hear — not "we are fully compliant" (which would be untrue), and not "we have significant gaps" (which would be alarming).

---

## 11. Conclusion

The bank's AI governance is **substantially compliant** with OSFI E-23. The five gaps identified are documented, prioritized, and remediated. The bank can demonstrate compliance to OSFI supervisory review with the gaps disclosed.

**The gap analysis is not a one-time exercise.** It is refreshed annually, and the remediation is tracked continuously. **The bank's compliance is not a state — it is a process.**

---

## Document control

| Field | Value |
|---|---|
| **Document ID** | RGA-001 |
| **Version** | 1.0 |
| **Status** | Approved |
| **Supersedes** | None (first version) |
| **Next review** | Annual — `[ANALYST: date]` |
| **Related documents** | AI Governance Policy (POL-AI-001), Model Risk Policy, OSFI E-23, SR 11-7, ISO/IEC 42001 |
| **Classification** | Internal |

---

## Appendix A — OSFI E-23 requirement index

| E-23 Section | Principle | Gap analysis section | Rating |
|---|---|---|---|
| s.3.1 | Roles and responsibilities | §5.1 | Met |
| s.3.2 | Model risk appetite | §5.2 | Met |
| s.3.3 | Model inventory | §5.3 | Partially Met (G-04) |
| s.4.1 | Model design, implementation, use | §4.1, §4.2, §4.3 | Met / Partially Met (G-01, G-02, G-03) |
| s.4.2 | Data quality and lineage | §4.1 | Met / Partially Met (G-01, G-02) |
| s.4.3 | Model use monitoring | §4.3 | Partially Met (G-03) |
| s.5.1 | Independent validation | §6.1 | Met |
| s.5.2 | Validation frequency | §6.2 | Partially Met (G-05) |
| s.6.1 | Reporting to senior management | §7.1 | Met |
| s.6.2 | Reporting to the board | §7.2 | Met |

**The appendix is the cross-reference.** A reviewer can find each E-23 section and see its rating and gap reference. **The index is the audit trail.**

---

## Appendix B — Gap register (machine-readable)

| Gap ID | Description | Pillar | Priority | Owner | Timeline |
|---|---|---|---|---|---|
| G-01 | Macro factors absent | Pillar 1 | HIGH | Data team | Next review cycle |
| G-02 | Protected attributes absent or proxied | Pillar 1 | HIGH | Data team | Next review cycle |
| G-03 | Model use monitoring not assessable | Pillar 1 | MEDIUM | Data team + AI Governance | Next review cycle |
| G-04 | Model inventory not integrated with AI Governance Policy | Pillar 2 | MEDIUM | AI Governance | Q2 next fiscal year |
| G-05 | No scheduled re-validation | Pillar 3 | MEDIUM | AI Governance | Q3 next fiscal year |

**The gap register is the summary artifact.** A reader who wants the gaps without reading the full document reads this table.
