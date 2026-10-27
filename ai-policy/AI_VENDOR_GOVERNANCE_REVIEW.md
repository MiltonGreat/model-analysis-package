# AI Vendor Governance Review + Scorecard

**Document ID:** VGR-001  
**Version:** 1.0  
**Classification:** Internal — Confidential  
**Related documents:** AI Governance Policy (POL-AI-001), Regulatory Gap Analysis (RGA-001), Third-Party AI requirements (Policy §7)

---

## 1. Purpose and scope

### 1.1 Purpose

This document records the **governance review of a proposed third-party AI vendor** — the assessment of the vendor's evidence, the assignment of a risk tier, the scorecard result, and the procurement recommendation. It is the **operational companion** to the AI Governance Policy §7 (Third-Party AI), which sets the requirements; this document is the application of those requirements to a specific vendor.

**The document's premise:** a vendor's claims are **not evidence**. A vendor saying *"we are secure"* is a marketing statement; a SOC 2 Type II report is evidence; a contractual audit right is a stronger form of evidence because it's enforceable. **The review is the process of weighing heterogeneous evidence and deciding whether it supports a procurement recommendation.**

**The document's audience:** the AI Governance Committee (for approval), the Chief Risk Officer (for risk acceptance), and the procurement team (for contract negotiation).

### 1.2 In scope

- The vendor's security, data handling, model stability, liability, and audit posture
- The use case's fit within the bank's AI risk tier framework
- The controls the bank must add (wrapper, fallback, audit right) to accept the residual risk
- The monitoring plan for the ongoing vendor relationship

### 1.3 Out of scope

- **Commercial terms** — pricing, volume commitments, and service-level agreements are assessed by procurement separately
- **Technical integration** — the API contract, latency, and throughput are assessed by engineering
- **Vendor financial stability** — assessed by vendor risk management
- **Contract drafting** — the legal team drafts the contract; this document specifies the controls the contract must contain

**The review is scoped to governance risk, not commercial, technical, or financial risk.** Those are separate reviews with separate owners.

### 1.4 The vendor profile (synthetic)

> **Vendor:** CloudSummarize AI Inc. (synthetic — not a real vendor)  
> **Product:** LLM-based document summarization for credit memo drafting  
> **Use case:** The bank's commercial credit team drafts credit memos for loan approvals. The vendor's product would summarize supporting documents (financial statements, appraisals, KYC records) into a draft summary that the credit analyst edits and signs. The analyst remains the decision-maker; the tool accelerates the drafting.
> **Integration model:** Vendor-hosted API; documents are sent to the vendor's servers for processing; summaries are returned to the bank's workflow.
> **Proposed tier:** High (Tier 2) — the tool informs a credit decision but the analyst remains the decision-maker.

**The vendor profile is synthetic** because the review is a portfolio demonstration, not a real procurement. The vendor name, product, and use case are plausible but fictional. **The assessment methodology is real.**

---

## 2. Evidence hierarchy

### 2.1 Why an evidence hierarchy

Third-party AI assessments produce **heterogeneous evidence**: contracts, audit reports, published benchmarks, vendor questionnaires, marketing materials. These are not equal in probative value.

**A contractual commitment is enforceable.** An audit report is a snapshot. A vendor questionnaire is self-reported. Marketing is unverifiable. **The evidence hierarchy ranks evidence by probative value — how strongly it supports or contradicts a claim.**

**Without an evidence hierarchy, a review becomes a checklist** — every piece of evidence gets equal weight, and the vendor's marketing is treated as equal to the vendor's audit report. **The hierarchy is what makes the review an assessment, not a checklist.**

### 2.2 The five tiers of evidence

| Tier | Evidence type | Probative value | Why |
|---|---|---|---|
| **Tier 1** | **Contractual commitment** | Highest | Enforceable; creates legal liability; auditable |
| **Tier 2** | **Independent audit report** (SOC 2, ISO 27001, ISO 42001) | High | Produced by an independent party; snapshot in time |
| **Tier 3** | **Published benchmark or regulatory filing** | Moderate | Independently produced, but not specific to the bank's use case |
| **Tier 4** | **Vendor questionnaire response** | Low | Self-reported; not verified; subject to vendor bias |
| **Tier 5** | **Marketing material or sales claim** | Lowest | Unverified; no accountability |

### 2.3 How the hierarchy is applied

**For each scorecard criterion, the review records:**

1. The **claim** being assessed (e.g., "the vendor provides independent security assurance")
2. The **evidence tier** of the strongest evidence supporting the claim
3. The **assessment** — does the evidence support the claim?
4. The **residual gap** — what evidence is missing, and what would close it?

**A criterion supported only by Tier 4 evidence is not the same as a criterion supported by Tier 1 evidence**, even if both are "Met." **The evidence tier is recorded alongside the score.** A "Met (Tier 4)" is weaker than a "Met (Tier 1)" — and the scorecard should reflect that.

**The scorecard's numeric score is a weighted average of the evidence-tier-weighted assessments.** A criterion supported by Tier 1 evidence scores higher than the same criterion supported by Tier 4 evidence.

### 2.4 What the hierarchy does not do

**The hierarchy does not reject lower-tier evidence.** A vendor's questionnaire response is still evidence — it's just weaker evidence. **The hierarchy informs the score; it doesn't determine it.**

**The hierarchy does not replace judgment.** A Tier 2 audit report that is 14 months old is weaker than a Tier 2 audit report that is 6 months old. **The age, scope, and independence of the evidence matter within each tier.**

---

## 3. Scorecard design

### 3.1 The five assessment dimensions

The scorecard assesses the vendor across **five dimensions**, each weighted by its importance for a Tier 2 (High) AI system in a credit workflow:

| Dimension | Weight | Rationale |
|---|---|---|
| **Security** | 30% | A data breach in a credit workflow exposes customer financial data; the impact is severe and the risk is high. This is the primary dimension for any third-party AI in a credit process. |
| **Data handling** | 25% | The vendor processes customer financial data; data residency, retention, deletion, and no-training-on-bank-data commitments are essential. Second only to security in impact. |
| **Model stability** | 20% | The vendor's model can change without notice, changing the bank's outputs. Version pinning, change notification, and re-validation rights are required. |
| **Liability and contract** | 15% | The vendor must accept liability for model errors; the bank needs indemnification and contractual remedies. |
| **Audit rights** | 10% | The bank must have the right to audit the vendor's model, data handling, and security. This is the enforcement mechanism for the other four dimensions. |

**The weights are anchored to the bank's risk appetite for Tier 2 AI systems.** A Tier 1 system would weight security higher (35–40%); a Tier 3 system would weight model stability and audit rights lower. **The weights are a policy choice, not an arbitrary allocation.**

**The weights sum to 100%.** The weighted score is the sum of (dimension score × weight).

### 3.2 The score scale

Each dimension is scored on a **0–4 scale**, with **half-point increments**:

| Score | Meaning |
|---|---|
| **4.0** | Fully met; supported by Tier 1 or Tier 2 evidence |
| **3.0** | Fully met; supported by Tier 3 evidence |
| **2.0** | Partially met; supported by Tier 2 or Tier 3 evidence |
| **1.0** | Partially met; supported by Tier 4 evidence |
| **0.5** | Weakly met; supported only by Tier 5 evidence |
| **0.0** | Not met; no evidence, or evidence contradicts the claim |

**The score is a function of both the assessment and the evidence tier.** A criterion that is "fully met" by a vendor's marketing (Tier 5) scores 0.5, not 4.0. **This is the scorecard's core discipline:** the evidence tier caps the score.

### 3.3 The recommendation mapping

The weighted score maps to a recommendation:

| Weighted score | Recommendation |
|---|---|
| **3.5 – 4.0** | **Approve** — no conditions |
| **2.5 – 3.4** | **Approve with conditions** — specific controls required |
| **1.5 – 2.4** | **Conditional review** — significant gaps; committee decision required |
| **0.0 – 1.4** | **Reject** — cannot be approved under current evidence |

**The mapping is deliberately not symmetric.** A score of 3.4 is "approve with conditions" while a score of 3.5 is "approve" — the threshold between conditions and no-conditions is a **policy choice**, and it's set high because the use case is Tier 2. **For a Tier 3 use case, the "approve" threshold would be 3.0, not 3.5.**

---

## 4. Scorecard assessment

### 4.1 Dimension 1 — Security (weight 30%)

**The claim:** the vendor provides independent security assurance.

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Independent security audit | SOC 2 Type II report, dated 14 months ago | **Tier 2** | 2.5 | Report exists but is 14 months old; vendor has not committed to annual refresh |
| Penetration testing | Vendor states "annual pen test" in questionnaire; no report provided | **Tier 4** | 1.0 | Self-reported; no evidence provided |
| Incident response plan | Vendor states "incident response plan in place"; no plan provided | **Tier 4** | 1.0 | Self-reported |
| Encryption at rest and in transit | Contract specifies AES-256 at rest and TLS 1.2+ in transit | **Tier 1** | 4.0 | Contractual commitment; enforceable |

**Dimension score:** weighted average of sub-criteria = (2.5 + 1.0 + 1.0 + 4.0) / 4 = **2.125**

**Interpretation:** The security posture is **partially met**. The contractual encryption commitment is strong; the audit report is present but stale; the penetration test and incident response claims are unsubstantiated. **A SOC 2 refresh and a pen test report would raise this dimension to 3.0+.**

### 4.2 Dimension 2 — Data handling (weight 25%)

**The claim:** the vendor handles customer data in compliance with the bank's requirements.

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Data residency | Contract specifies data processing in the bank's jurisdiction | **Tier 1** | 4.0 | Contractual commitment |
| Retention and deletion | Contract specifies 30-day retention and deletion on request | **Tier 1** | 4.0 | Contractual commitment |
| No training on bank data | Contract specifies the vendor will not train on bank data | **Tier 1** | 4.0 | Contractual commitment |
| Data breach notification | Contract specifies 72-hour notification | **Tier 1** | 4.0 | Contractual commitment |

**Dimension score:** weighted average = **4.0**

**Interpretation:** The data handling posture is **fully met**. Every sub-criterion is supported by Tier 1 evidence — the contract. **This is the strongest dimension in the review.** The vendor's data handling commitments are enforceable and specific.

**The strength of this dimension is not accidental.** The vendor was selected in part *because* its contract template included these commitments. **A vendor with weaker data handling would have been rejected at the procurement stage before reaching this review.**

### 4.3 Dimension 3 — Model stability (weight 20%)

**The claim:** the vendor's model is stable, and the bank can control changes.

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Version pinning | Vendor's API supports version pinning; contract commits to 90-day notice of version changes | **Tier 1** | 3.5 | Contractual commitment; 90-day notice is adequate but not ideal (180-day preferred) |
| Change notification | Contract specifies 90-day notice of model changes | **Tier 1** | 3.5 | Same as version pinning |
| Re-validation right | Contract gives the bank the right to re-validate the model after changes | **Tier 1** | 4.0 | Contractual commitment |
| Model performance stability | Vendor provides a benchmark report; dated 6 months ago | **Tier 3** | 3.0 | Independently produced benchmark; not specific to the bank's use case |

**Dimension score:** weighted average = (3.5 + 3.5 + 4.0 + 3.0) / 4 = **3.5**

**Interpretation:** The model stability posture is **mostly met**. The contractual commitments are strong; the 90-day notice period is adequate but not ideal. **The 90-day notice is the weakest link** — a 180-day notice period would be preferred for a credit workflow, because it allows the bank to re-validate before the change affects decisions.

### 4.4 Dimension 4 — Liability and contract (weight 15%)

**The claim:** the vendor accepts liability for model errors and provides adequate contractual remedies.

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Liability cap | Contract caps liability at 12 months of fees | **Tier 1** | 2.0 | Contractual commitment; cap is **too low** for a credit workflow |
| Indemnification | Contract provides indemnification for third-party IP claims, but not for model errors | **Tier 1** | 2.0 | Partial coverage |
| Service-level agreement | Contract specifies 99.5% uptime | **Tier 1** | 3.0 | Standard SLA; adequate for a Tier 2 system |
| Termination rights | Contract allows termination for breach with 30-day cure period | **Tier 1** | 3.0 | Standard termination clause |

**Dimension score:** weighted average = (2.0 + 2.0 + 3.0 + 3.0) / 4 = **2.5**

**Interpretation:** The liability posture is **partially met**. The liability cap of 12 months of fees is **materially too low** for a credit workflow — if the vendor's model produces a materially wrong summary that leads to an incorrect credit decision, the bank's loss could exceed 12 months of vendor fees by orders of magnitude. **This is the review's most significant gap.** The conditions section (§6) requires the liability cap to be renegotiated before procurement.

### 4.5 Dimension 5 — Audit rights (weight 10%)

**The claim:** the bank can audit the vendor's model, data handling, and security.

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Right to audit the model | Contract gives the bank the right to audit the model | **Tier 1** | 4.0 | Contractual commitment |
| Right to audit data handling | Contract gives the bank the right to audit data handling | **Tier 1** | 4.0 | Contractual commitment |
| Right to audit security | Contract gives the bank the right to audit security | **Tier 1** | 4.0 | Contractual commitment |
| Audit frequency | Contract allows annual audit | **Tier 1** | 4.0 | Adequate for a Tier 2 system |

**Dimension score:** weighted average = **4.0**

**Interpretation:** The audit rights posture is **fully met**. The bank has the right to audit the model, data handling, and security, and the audit frequency is adequate. **This is the second-strongest dimension.**

**The audit rights are the enforcement mechanism for the other four dimensions.** Without them, the security, data handling, and model stability commitments would be unverifiable. **Their strength compensates, in part, for the weakness in liability.**

---

## 5. Weighted score and risk tier

### 5.1 Weighted score

| Dimension | Score | Weight | Weighted |
|---|---|---|---|
| Security | 2.125 | 30% | 0.6375 |
| Data handling | 4.0 | 25% | 1.0000 |
| Model stability | 3.5 | 20% | 0.7000 |
| Liability and contract | 2.5 | 15% | 0.3750 |
| Audit rights | 4.0 | 10% | 0.4000 |
| **Total** | | **100%** | **3.1125** |

**The weighted score is 3.11 out of 4.0.**

### 5.2 Recommendation

**Weighted score 3.11 → Approve with conditions.**

**The score is above 2.5 (the "approve with conditions" threshold) but below 3.5 (the "approve" threshold).** The vendor is **approvable**, but with specific conditions attached.

**The score is driven by the two strong dimensions (data handling, audit rights) and the two weak dimensions (security, liability).** The conditions in §6 address both weaknesses.

### 5.3 Risk tier confirmation

**The proposed tier is Tier 2 (High).** The review confirms the tier assignment:

- **The use case informs a credit decision** (Tier 2 criteria)
- **The analyst remains the decision-maker** (not Tier 1 — the tool doesn't make the decision)
- **The financial impact of a wrong summary is significant but bounded** (not Tier 3 — the impact is not "limited")

**The Tier 2 approval path is: AI Governance review → MRC approval.** This review is the AI Governance input; the MRC's approval is a separate step.

**The tier is not elevated to Tier 1** even though the use case is in a credit workflow, because the analyst's review and signature are the decisioning controls. **A tool that made the decision would be Tier 1.**

---

## 6. Conditions for approval

### 6.1 The four conditions

The vendor is **approved with conditions**. The conditions must be satisfied before deployment.

| # | Condition | Addresses | Verification |
|---|---|---|---|
| **C-01** | **Liability cap renegotiated** to at least 3× the annual contract value, with carve-out for model errors | Dimension 4 (liability) | Contract addendum signed |
| **C-02** | **Annual SOC 2 Type II refresh** contractually committed; first refresh within 12 months | Dimension 1 (security) | Contract amendment; SOC 2 report at refresh |
| **C-03** | **Penetration test report** provided before deployment; annual refresh contractually committed | Dimension 1 (security) | Pen test report; contract amendment |
| **C-04** | **Fallback path** operational: the bank can draft credit memos without the vendor if the vendor's service is unavailable or the model changes materially | Dimension 3 (model stability) | Fallback process documented; tested |

### 6.2 Condition rationale

**C-01 — Liability cap.** The current cap (12 months of fees) is inadequate for a credit workflow. A wrong summary could lead to a materially wrong credit decision, with losses that exceed 12 months of vendor fees. **The 3× annual contract value cap is a minimum; the legal team may negotiate higher.** The carve-out for model errors is essential — without it, the vendor's liability is capped regardless of the error's cause.

**C-02 — SOC 2 refresh.** The current SOC 2 report is 14 months old — beyond the standard 12-month validity window. **An annual refresh is the minimum.** The vendor's commitment to annual refresh is a Tier 1 evidence commitment (contractual), which raises the security dimension's evidence tier.

**C-03 — Penetration test.** The vendor's questionnaire states "annual pen test" but provides no report. **A Tier 4 claim is not sufficient for a Tier 2 system.** The report is required before deployment; the annual commitment is required for ongoing assurance.

**C-04 — Fallback path.** The vendor's 90-day change notice period is adequate but not ideal. **A fallback path ensures that a material model change doesn't disrupt the bank's credit workflow.** The fallback must be operational (tested), not theoretical.

### 6.3 Post-approval monitoring

**If the conditions are satisfied, the vendor is approved. The approval is monitored via:**

| Monitoring activity | Frequency | Owner |
|---|---|---|
| SOC 2 refresh | Annual | AI Governance |
| Penetration test report | Annual | AI Governance |
| Model change notification | Per change | Business unit |
| Fallback path test | Semi-annual | Business unit + IT |
| Vendor performance review | Annual | AI Governance + procurement |
| Contract renewal review | Per renewal | AI Governance + legal |

**The monitoring is event-driven for model changes and annual for everything else.** Model changes are the highest-risk event — they trigger a re-validation requirement under the AI Governance Policy §6.4.

---

## 7. Residual risk and acceptance

### 7.1 Residual risk after conditions

**If the four conditions are satisfied, the residual risk is: LOW–MEDIUM.**

| Dimension | Residual risk | Reasoning |
|---|---|---|
| Security | **Low** | SOC 2 refresh + pen test report + contractual commitments |
| Data handling | **Low** | Contractual commitments are strong; no further action needed |
| Model stability | **Low–Medium** | Fallback path mitigates the 90-day notice gap |
| Liability | **Medium** | 3× annual contract value cap is better but still not unlimited; model errors may exceed the cap in extreme cases |
| Audit rights | **Low** | Contractual audit rights are strong |

**The residual risk is medium for liability** because even with the renegotiated cap, the bank retains some risk that the vendor's liability is insufficient. **This is the nature of third-party AI — the bank cannot fully transfer the liability, only bound it.**

### 7.2 Risk acceptance

**The residual risk is accepted by the Chief Risk Officer, on the recommendation of the AI Governance Committee.** The acceptance is documented in the MRC's approval record.

**The acceptance is scoped:** it covers the specific use case (credit memo drafting for commercial credit), not any use of the vendor's product. **A new use case requires a new review.**

### 7.3 What the review does not approve

**The review does not approve:**

- **Any use of the vendor's product outside credit memo drafting.** A new use case (e.g., customer-facing document processing) would require a new review.
- **The vendor's other products.** The review covers the specific product described in §1.4.
- **The vendor's future versions.** A material model change triggers a re-validation requirement under Policy §6.4.

**The approval is narrow by design.** A broad approval would be a governance failure — it would accept risk the review didn't assess.

---

## 8. Governance and decision record

### 8.1 Review completion

| Activity | Status | Date |
|---|---|---|
| Evidence collection | Complete | `[ANALYST: date]` |
| Scorecard assessment | Complete | `[ANALYST: date]` |
| Risk tier confirmation | Complete | `[ANALYST: date]` |
| Condition specification | Complete | `[ANALYST: date]` |
| Review finalized | Complete | `[ANALYST: date]` |

### 8.2 Decision record

| Role | Name | Recommendation | Date |
|---|---|---|---|
| **Reviewer** | `[ANALYST: name]` | Approve with conditions (C-01 through C-04) | `[ANALYST: date]` |
| **Head of AI Governance** | `[ANALYST: name]` | `[ANALYST: concur / dissent]` | `[ANALYST: date]` |
| **Chief Risk Officer** | `[ANALYST: name]` | `[ANALYST: accept residual risk]` | `[ANALYST: date]` |
| **MRC Chair** | `[ANALYST: name]` | `[ANALYST: approve / conditional / reject]` | `[ANALYST: date]` |

**The decision record is the review's formal conclusion.** The reviewer's recommendation is the input; the Head of AI Governance's concurrence is the governance check; the CRO's acceptance is the risk acceptance; the MRC's approval is the deployment authorization.

**The chain is not optional.** A review without the CRO's acceptance is a recommendation, not a risk acceptance. **The CRO's signature converts the residual risk into an accepted risk.**

### 8.3 What happens if the conditions are not satisfied

**If the conditions are not satisfied within 90 days of MRC approval:**

1. The approval is **suspended** — the vendor cannot be deployed.
2. The AI Governance Committee **reviews the vendor's progress** at the next scheduled meeting.
3. If progress is insufficient, the MRC may **reject the vendor** — the approval is revoked.

**The conditions are not a suggestion.** They're a requirement for deployment. **A vendor that doesn't satisfy them is not approved.**

---

## 9. What this review demonstrates (portfolio note)

This Vendor Governance Review demonstrates a skill the other portfolio artifacts don't: **evidence assessment and procurement judgment**.

**The Lending Club and Fannie Mae projects demonstrate model validation** — recompute, compare, decide. **The Vendor Review demonstrates a different discipline:** weighing heterogeneous evidence (contracts, audit reports, questionnaires, marketing) and deciding whether the evidence supports a procurement recommendation.

**The review's intellectual contribution is the evidence hierarchy (§2).** It says: *"Not all evidence is equal."* A contractual commitment is enforceable; an audit report is a snapshot; a questionnaire is self-reported; marketing is unverifiable. **The hierarchy is what makes the scorecard an assessment, not a checklist.**

**The review's governance contribution is the scoped approval (§7.3).** The vendor is approved **for a specific use case**, not for any use of its product. **The scope is the discipline** — a broad approval would accept risk the review didn't assess.

**The review's honesty is the residual risk (§7.1).** Even with the conditions satisfied, the residual risk is **medium** for liability. The bank cannot fully transfer the liability of a third-party AI system — it can only bound it. **The review documents what the bank accepts, not what the vendor promises.**

**The review is the artifact a hiring manager reads when they want to know:** *"Can this person assess a vendor's claims without being swayed by the vendor's marketing?"* **The answer is in the evidence hierarchy, the scorecard's evidence-tier weighting, and the scoped approval.**

---

## Document control

| Field | Value |
|---|---|
| **Document ID** | VGR-001 |
| **Version** | 1.0 |
| **Status** | Approved with conditions |
| **Supersedes** | None (first version) |
| **Next review** | At condition satisfaction (target: 90 days from MRC approval) |
| **Related documents** | AI Governance Policy (POL-AI-001) §7; Regulatory Gap Analysis (RGA-001); MRC Approval Record |
| **Classification** | Internal — Confidential |

---

## Appendix A — Scorecard summary (one-page view)

| Dimension | Weight | Score (0–4) | Weighted | Evidence tier |
|---|---|---|---|---|
| **Security** | 30% | 2.125 | 0.6375 | Mixed (Tier 1–4) |
| **Data handling** | 25% | 4.000 | 1.0000 | Tier 1 |
| **Model stability** | 20% | 3.500 | 0.7000 | Mixed (Tier 1, 3) |
| **Liability and contract** | 15% | 2.500 | 0.3750 | Tier 1 |
| **Audit rights** | 10% | 4.000 | 0.4000 | Tier 1 |
| **Weighted score** | **100%** | | **3.1125** | |
| **Recommendation** | | | **Approve with conditions** | |

**The scorecard is the review's summary.** A reader who wants the full picture without reading §4 reads this table — and then reads the conditions in §6.

## Appendix B — Condition tracker

| Condition | Owner | Target date | Status |
|---|---|---|---|
| **C-01** Liability cap renegotiation | Legal + procurement | 90 days | `[ANALYST: status]` |
| **C-02** SOC 2 annual refresh commitment | Vendor + procurement | 90 days | `[ANALYST: status]` |
| **C-03** Penetration test report | Vendor + AI Governance | 90 days | `[ANALYST: status]` |
| **C-04** Fallback path operational | IT + business unit | 90 days | `[ANALYST: status]` |

**The tracker is the review's operational continuation.** It's how the AI Governance Committee knows whether the conditions are being satisfied.

## Appendix C — Evidence index

| Evidence | Type | Tier | Date | Source |
|---|---|---|---|---|
| Contract (executed) | Contractual | 1 | `[ANALYST: date]` | Legal |
| SOC 2 Type II report | Audit report | 2 | 14 months ago | Vendor |
| Vendor questionnaire | Self-reported | 4 | `[ANALYST: date]` | Vendor |
| Published benchmark report | Benchmark | 3 | 6 months ago | Vendor (independent author) |
| Marketing materials | Marketing | 5 | `[ANALYST: date]` | Vendor |

**The evidence index is the review's audit trail.** A reader can trace every score back to a specific piece of evidence and its tier.
