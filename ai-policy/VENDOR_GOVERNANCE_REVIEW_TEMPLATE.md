# AI Vendor Governance Review + Scorecard — TEMPLATE

**Document ID:** VGR-TEMPLATE-001  
**Version:** 1.0  
**Author:** `[ANALYST: name]`  
**Owner:** `[ANALYST: role — Head of AI Governance]`  
**Date:** `[ANALYST: date]`  
**Classification:** Internal — Template  
**Related documents:** AI Governance Policy (POL-AI-001), Regulatory Gap Analysis (RGA-001)

---

## How to use this template

This template is a **repeatable process** for assessing a third-party AI vendor. It is designed to be filled in for each vendor the bank considers procuring. **Every review should use this template; every review should produce a document that can be compared against other reviews.**

**Before you begin:**

1. **Read the entire template first.** Each section explains *what to write* and *why it matters*. Skipping the guidance is the most common mistake.
2. **Gather the evidence before writing.** The scorecard is only as good as the evidence behind it. Collect contracts, audit reports, questionnaire responses, benchmarks, and marketing materials first.
3. **Classify the evidence using §3's hierarchy.** Not all evidence is equal — a contractual commitment is stronger than a marketing claim. Record the tier for every piece of evidence.
4. **Score each dimension using §4's scale.** The evidence tier caps the score. A "fully met" claim supported only by marketing scores 0.5, not 4.0.
5. **Write the conditions before the recommendation.** The conditions are what make an "approve with conditions" recommendation actionable. A recommendation without conditions is a wish.

**What this template produces:**

A completed review with:
- An evidence-based scorecard (five dimensions, weighted)
- A risk tier assignment (Tier 1–4, per Policy §5.1)
- A scoped recommendation (approve / approve with conditions / conditional review / reject)
- Specific conditions for approval (if applicable)
- A monitoring plan for the ongoing vendor relationship

**What this template does NOT do:**

- **It does not assess commercial terms.** Pricing, volume commitments, and SLAs are procurement's domain.
- **It does not assess technical integration.** API contract, latency, and throughput are engineering's domain.
- **It does not assess the vendor's financial stability.** That's vendor risk management's domain.
- **It does not draft the contract.** Legal drafts the contract; this review specifies the controls the contract must contain.

**The template is deliberately long.** The guidance in each section is what makes it usable by a new analyst, and what makes the review auditable by a governance committee. A shorter template would be a form, not a process.

---

## Section 1 — Purpose and scope

### 1.1 Purpose

**What to write:** one paragraph stating what this review is for and what it produces.

**Why it matters:** the purpose sets the scope. A review that says "assess the vendor" is too vague; a review that says "assess the vendor's security, data handling, model stability, liability, and audit rights for a specific use case" is specific enough to be auditable.

**Example:**

> This document records the governance review of `[Vendor name]` — the assessment of the vendor's evidence, the assignment of a risk tier, the scorecard result, and the procurement recommendation. It is the operational companion to the AI Governance Policy §7 (Third-Party AI), which sets the requirements; this document is the application of those requirements to this specific vendor.

**What to avoid:**

- *"Assess the vendor's AI."* — too vague; doesn't specify which dimensions
- *"Determine if the vendor is safe."* — "safe" is not a governance standard; the review assesses specific dimensions

### 1.2 In scope

**What to write:** a bulleted list of what this review assesses.

**Why it matters:** the in-scope list is the reviewer's contract with the reader. A reader who knows what's in scope knows what to expect; a reader who knows what's out of scope knows what questions to ask elsewhere.

**Typical in-scope items:**

- The vendor's security posture
- The vendor's data handling
- The vendor's model stability
- The vendor's liability and contract posture
- The vendor's audit rights
- The use case's fit within the bank's AI risk tier framework
- The controls the bank must add to accept residual risk
- The monitoring plan for the ongoing relationship

**What to avoid:**

- Including commercial terms or technical integration (those are separate reviews)
- Omitting the monitoring plan (a review without a monitoring plan is a snapshot, not a governance decision)

### 1.3 Out of scope

**What to write:** a bulleted list of what this review does not assess, with the owner of each.

**Why it matters:** the out-of-scope list prevents scope creep and makes the division of labor explicit. A reader who asks "what about the price?" gets the answer: "that's procurement's review, not this one."

**Typical out-of-scope items:**

| Item | Owner |
|---|---|
| Commercial terms (pricing, volume, SLAs) | Procurement |
| Technical integration (API, latency, throughput) | Engineering |
| Vendor financial stability | Vendor Risk Management |
| Contract drafting | Legal |
| Data residency assessment | Data Protection Officer |

**What to avoid:**

- Leaving out-of-scope items undocumented (they'll surface as open questions in the committee)
- Claiming this review covers items it doesn't (e.g., "the vendor is compliant" when only the governance dimensions were assessed)

### 1.4 Vendor profile

**What to write:** a structured profile of the vendor and the use case. This is the context that every subsequent section depends on.

**Required fields:**

| Field | What to write | Why it matters |
|---|---|---|
| **Vendor name** | The legal entity name | Procurement and legal need the exact entity |
| **Product** | The specific product being assessed | A vendor may have multiple products; this review covers one |
| **Use case** | What the product would be used for in the bank | The use case determines the risk tier and the dimensions' weights |
| **Integration model** | How the product would integrate (API, on-premise, hybrid) | The integration model determines the data flow and the security assessment |
| **Decision role** | Does the product make a decision, inform a decision, or assist a human? | This determines the risk tier (Tier 1 vs Tier 2 vs Tier 3) |
| **Proposed tier** | The tier the business unit proposes (per Policy §5.1) | The tier determines the approval path; this review confirms or adjusts it |

**Example:**

> **Vendor:** `[Vendor name]`  
> **Product:** `[Product name and version]`  
> **Use case:** `[What the product does, in one sentence]`  
> **Integration model:** `[API / on-premise / hybrid]`  
> **Decision role:** `[Makes / informs / assists]` a `[specific decision]`  
> **Proposed tier:** `[Tier 1 / 2 / 3 / 4]` — `[brief rationale]`

**What to avoid:**

- Describing the vendor's *marketing* ("industry-leading AI") instead of the *product* ("LLM-based document summarization")
- Leaving the "decision role" ambiguous — the tier depends on it
- Skipping the "proposed tier" — a review without a proposed tier is a review without a starting hypothesis

### 1.5 Evidence base

**What to write:** a summary of the evidence collected for this review, with the source of each.

**Why it matters:** the evidence base is what makes the review auditable. A reviewer who says "the vendor is secure" without evidence is asserting, not assessing. The evidence base records what was collected and what was not.

**Example table:**

| Evidence | Type | Source | Date |
|---|---|---|---|
| Contract (executed) | Contractual | Legal | `[date]` |
| SOC 2 Type II report | Audit report | Vendor | `[date]` |
| Penetration test report | Audit report | Vendor | `[date]` |
| Vendor questionnaire | Self-reported | Vendor | `[date]` |
| Published benchmark | Benchmark | Vendor (independent author) | `[date]` |

**What to avoid:**

- Listing marketing materials as evidence without labelling them as such
- Omitting evidence that was requested but not provided (the *absence* of evidence is itself information)
- Assuming a document is current because it was provided (record the date)

---

## Section 2 — Evidence hierarchy

### 2.1 Why an evidence hierarchy

**Read this section before scoring anything.** The evidence hierarchy is the template's foundational discipline. Without it, the scorecard is a checklist with numbers; with it, the scorecard is an assessment.

**The core insight:** **not all evidence is equal.** A contractual commitment is enforceable. An audit report is a snapshot. A vendor questionnaire is self-reported. Marketing is unverifiable. The hierarchy ranks evidence by probative value — how strongly it supports or contradicts a claim.

**Why this matters for AI vendors specifically:** AI vendors often provide marketing-heavy documentation and light on independent assurance. A scorecard that treats marketing as equal to a SOC 2 report would rate a marketing-heavy vendor highly. **The hierarchy is the correction.**

### 2.2 The five tiers

| Tier | Evidence type | Probative value | Why |
|---|---|---|---|
| **Tier 1** | **Contractual commitment** | Highest | Enforceable; creates legal liability; auditable |
| **Tier 2** | **Independent audit report** (SOC 2, ISO 27001, ISO 42001) | High | Produced by an independent party; snapshot in time |
| **Tier 3** | **Published benchmark or regulatory filing** | Moderate | Independently produced, but not specific to the bank's use case |
| **Tier 4** | **Vendor questionnaire response** | Low | Self-reported; not verified; subject to vendor bias |
| **Tier 5** | **Marketing material or sales claim** | Lowest | Unverified; no accountability |

**The hierarchy is fixed.** It is not adjusted per vendor. A vendor that provides only marketing evidence is not assessed against a different hierarchy — the vendor is assessed as having only Tier 5 evidence, and the score reflects it.

### 2.3 How to classify evidence

**For each piece of evidence, ask three questions:**

1. **Who produced it?** The vendor (Tier 4–5), an independent party (Tier 2–3), or the contract (Tier 1)?
2. **Is it enforceable?** A contractual commitment (Tier 1) creates legal liability. A marketing claim (Tier 5) does not.
3. **Is it specific to the bank's use case?** An audit report specific to the vendor's data centres (Tier 2) is stronger than a general industry benchmark (Tier 3).

**Edge cases to watch for:**

| Situation | Correct classification | Why |
|---|---|---|
| A vendor questionnaire that *cites* an audit report | **Tier 4**, unless the audit report itself is provided | The questionnaire is self-reported; the audit report is what matters |
| An audit report dated 14 months ago | **Tier 2**, but noted as stale | The tier reflects the *type* of evidence; the age is a separate factor that should lower the score |
| A "self-assessment" against ISO 42001 | **Tier 4**, not Tier 2 | A self-assessment is not an independent audit |
| A blog post by the vendor's CTO about security | **Tier 5** | Marketing-adjacent; not evidence |
| A published paper about the vendor's model architecture | **Tier 3** | Independently produced (if peer-reviewed) or vendor-produced (if not — check the author) |

### 2.4 What the hierarchy does not do

- **It does not reject lower-tier evidence.** A Tier 4 questionnaire is still evidence; it's just weaker evidence. The hierarchy informs the score; it doesn't determine it.
- **It does not replace judgment.** A Tier 2 report that is 14 months old is weaker than a Tier 2 report that is 6 months old. Age, scope, and independence matter *within* each tier.
- **It does not allow a vendor to "buy" a higher tier.** A vendor that provides a contract (Tier 1) for a criterion that the contract doesn't actually address is not Tier 1 for that criterion. **The tier reflects what the evidence actually shows, not what it claims.**

---

## Section 3 — Scorecard design

### 3.1 The five assessment dimensions

**This section is fixed.** The dimensions, weights, and rationale are the methodology, not the vendor-specific assessment. Every review uses the same dimensions and the same weights (unless the use case's risk tier is different — see §3.2).

| Dimension | Weight | Rationale |
|---|---|---|
| **Security** | 30% | A data breach in a credit workflow exposes customer financial data; the impact is severe and the risk is high. This is the primary dimension for any third-party AI in a credit process. |
| **Data handling** | 25% | The vendor processes customer financial data; data residency, retention, deletion, and no-training-on-bank-data commitments are essential. Second only to security in impact. |
| **Model stability** | 20% | The vendor's model can change without notice, changing the bank's outputs. Version pinning, change notification, and re-validation rights are required. |
| **Liability and contract** | 15% | The vendor must accept liability for model errors; the bank needs indemnification and contractual remedies. |
| **Audit rights** | 10% | The bank must have the right to audit the vendor's model, data handling, and security. This is the enforcement mechanism for the other four dimensions. |

**The weights sum to 100%.** The weighted score is the sum of (dimension score × weight).

### 3.2 Adjusting the weights for different risk tiers

**The default weights above are for a Tier 2 (High) AI system.** They are the weights this template uses unless the use case is Tier 1 or Tier 3–4.

**If the use case is Tier 1 (Critical):**

| Dimension | Tier 1 weight | Tier 2 weight (default) |
|---|---|---|
| Security | 35% | 30% |
| Data handling | 30% | 25% |
| Model stability | 15% | 20% |
| Liability and contract | 15% | 15% |
| Audit rights | 5% | 10% |

**Why:** Tier 1 systems have higher security and data handling risk (they make the decision, not just inform it), and the audit rights are less critical because the bank's own validation is more rigorous.

**If the use case is Tier 3 (Moderate):**

| Dimension | Tier 3 weight | Tier 2 weight (default) |
|---|---|---|
| Security | 30% | 30% |
| Data handling | 25% | 25% |
| Model stability | 20% | 20% |
| Liability and contract | 15% | 15% |
| Audit rights | 10% | 10% |

**Why:** the weights are the same as Tier 2 — the dimensions don't change, only the *thresholds* for "approve" change (see §3.4). A Tier 3 system uses the same weights but a lower approval threshold.

**If the use case is Tier 4 (Low):**

**The template is not used for Tier 4 systems.** Tier 4 systems require only a business-unit notification and an AI Governance acknowledgement (per Policy §5.1). A full scorecard is overkill for a system with no customer impact.

### 3.3 The score scale

**Each dimension is scored on a 0–4 scale with half-point increments.** The score is a function of both the assessment (is the criterion met?) and the evidence tier (what tier of evidence supports it?).

| Score | Meaning |
|---|---|
| **4.0** | Fully met; supported by Tier 1 or Tier 2 evidence |
| **3.0** | Fully met; supported by Tier 3 evidence |
| **2.0** | Partially met; supported by Tier 2 or Tier 3 evidence |
| **1.0** | Partially met; supported by Tier 4 evidence |
| **0.5** | Weakly met; supported only by Tier 5 evidence |
| **0.0** | Not met; no evidence, or evidence contradicts the claim |

**The evidence tier caps the score.** A criterion that is "fully met" by a vendor's marketing (Tier 5) scores 0.5, not 4.0. **This is the scorecard's core discipline.**

**The half-point increments allow for nuance.** A criterion that is fully met by Tier 2 evidence but has a noted weakness (e.g., a stale report) scores 3.5, not 4.0. A criterion that is partially met but has strong Tier 1 evidence for the part that *is* met scores 2.5, not 2.0.

### 3.4 The recommendation mapping

**The weighted score maps to a recommendation. The mapping differs by risk tier.**

**Tier 2 (High) — the default for this template:**

| Weighted score | Recommendation |
|---|---|
| **3.5 – 4.0** | **Approve** — no conditions |
| **2.5 – 3.4** | **Approve with conditions** — specific controls required |
| **1.5 – 2.4** | **Conditional review** — significant gaps; committee decision required |
| **0.0 – 1.4** | **Reject** — cannot be approved under current evidence |

**Tier 1 (Critical):**

| Weighted score | Recommendation |
|---|---|
| **3.75 – 4.0** | **Approve** |
| **3.0 – 3.74** | **Approve with conditions** |
| **2.0 – 2.99** | **Conditional review** |
| **0.0 – 1.99** | **Reject** |

**Why the thresholds are higher for Tier 1:** a Tier 1 system makes a decision (not just informs one); the tolerance for risk is lower.

**Tier 3 (Moderate):**

| Weighted score | Recommendation |
|---|---|
| **3.0 – 4.0** | **Approve** |
| **2.0 – 2.99** | **Approve with conditions** |
| **1.0 – 1.99** | **Conditional review** |
| **0.0 – 0.99** | **Reject** |

**Why the thresholds are lower for Tier 3:** a Tier 3 system has limited impact; the tolerance for risk is higher.

**The mapping is fixed per tier.** It is not adjusted per vendor. A vendor that asks for a lower threshold is asking for a policy change, not a review outcome.

---

## Section 4 — Scorecard assessment

**This is where the review is performed.** For each dimension, assess each sub-criterion, record the evidence, assign the evidence tier, assign the score, and write the interpretation.

**The sub-criteria are illustrative, not exhaustive.** Add sub-criteria as needed for the specific use case. **The dimensions are fixed; the sub-criteria are adaptable.**

### 4.1 Dimension 1 — Security (weight: `[30% / 35% / 30%]`)

**The claim:** state in one sentence what security property you're assessing.

*Example: "The vendor provides independent security assurance."*

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Independent security audit | | | | |
| Penetration testing | | | | |
| Incident response plan | | | | |
| Encryption at rest and in transit | | | | |
| Access controls and authentication | | | | |
| `[Additional sub-criterion]` | | | | |

**Scoring guidance:** see §3.3. The evidence tier caps the score.

**Common pitfalls for this dimension:**

- *Don't accept a vendor questionnaire as Tier 2 evidence.* A questionnaire is self-reported (Tier 4) even if it cites an audit report; the audit report itself must be provided to be Tier 2.
- *Don't score a stale audit report as 4.0.* A 14-month-old SOC 2 report is still Tier 2 evidence, but its age should be recorded in the notes and should reduce the score.
- *Don't conflate "fully met" with "high score."* A criterion fully met by marketing (Tier 5) scores 0.5.

**Dimension score:** weighted average of sub-criterion scores = `[sum] / [number of sub-criteria]` = `[score]`

**Interpretation:** one paragraph summarizing the dimension's posture and the main weakness.

*Example: "The security posture is partially met. The contractual encryption commitment is strong; the audit report is present but stale; the penetration test and incident response claims are unsubstantiated."*

### 4.2 Dimension 2 — Data handling (weight: `[25% / 30% / 25%]`)

**The claim:** state in one sentence what data handling property you're assessing.

*Example: "The vendor handles customer data in compliance with the bank's requirements."*

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Data residency | | | | |
| Retention and deletion | | | | |
| No training on bank data | | | | |
| Data breach notification | | | | |
| Sub-processor disclosure | | | | |
| `[Additional sub-criterion]` | | | | |

**Common pitfalls for this dimension:**

- *Don't accept "we don't retain data" without a contract.* A verbal assurance is Tier 4; the contract is Tier 1.
- *Don't confuse "no training" with "no use."* A vendor that uses data for "service improvement" without training the model is still using the data.
- *Don't skip the sub-processor question.* Many AI vendors use third-party LLMs; the sub-processor's data handling is part of the vendor's data handling.

**Dimension score:** `[score]`

**Interpretation:** `[paragraph]`

### 4.3 Dimension 3 — Model stability (weight: `[20% / 15% / 20%]`)

**The claim:** state in one sentence what model stability property you're assessing.

*Example: "The vendor's model is stable, and the bank can control changes."*

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Version pinning | | | | |
| Change notification | | | | |
| Re-validation right | | | | |
| Model performance stability | | | | |
| Deprecation / end-of-life policy | | | | |
| `[Additional sub-criterion]` | | | | |

**Common pitfalls for this dimension:**

- *Don't accept "we notify customers of changes" without a specific notice period.* 30 days is standard; 90 days is adequate for a Tier 2 system; 180 days is preferred for a credit workflow.
- *Don't confuse "version pinning" with "no changes."* Version pinning allows the bank to stay on a known version, but the vendor may still deprecate it.
- *Don't skip the re-validation right.* Without it, the bank cannot verify the model's performance after a change.

**Dimension score:** `[score]`

**Interpretation:** `[paragraph]`

### 4.4 Dimension 4 — Liability and contract (weight: `[15% / 15% / 15%]`)

**The claim:** state in one sentence what liability property you're assessing.

*Example: "The vendor accepts liability for model errors and provides adequate contractual remedies."*

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Liability cap | | | | |
| Indemnification | | | | |
| Service-level agreement | | | | |
| Termination rights | | | | |
| Governing law and jurisdiction | | | | |
| `[Additional sub-criterion]` | | | | |

**Common pitfalls for this dimension:**

- *Don't accept a liability cap of 12 months of fees for a credit workflow.* A wrong summary could lead to a materially wrong credit decision; the cap must reflect the potential loss.
- *Don't confuse indemnification for IP claims with indemnification for model errors.* The former is standard; the latter is essential.
- *Don't skip the governing law question.* A contract governed by a foreign jurisdiction may be difficult to enforce.

**Dimension score:** `[score]`

**Interpretation:** `[paragraph]`

### 4.5 Dimension 5 — Audit rights (weight: `[10% / 5% / 10%]`)

**The claim:** state in one sentence what audit right you're assessing.

*Example: "The bank can audit the vendor's model, data handling, and security."*

| Sub-criterion | Evidence | Tier | Score | Notes |
|---|---|---|---|---|
| Right to audit the model | | | | |
| Right to audit data handling | | | | |
| Right to audit security | | | | |
| Audit frequency | | | | |
| Audit cost allocation | | | | |
| `[Additional sub-criterion]` | | | | |

**Common pitfalls for this dimension:**

- *Don't accept "we're audited annually by a third party" as a substitute for the bank's right to audit.* An independent audit is Tier 2 evidence; the right to audit is Tier 1. **The bank needs both.**
- *Don't skip the cost allocation.* If the bank has the right to audit but must pay for the audit, the right is less usable.
- *Don't accept "on-site audits only."* In a cloud deployment, remote audits (or evidence packages) may be the only practical option.

**Dimension score:** `[score]`

**Interpretation:** `[paragraph]`

---

## Section 5 — Weighted score and risk tier

### 5.1 Weighted score

| Dimension | Score (from §4) | Weight | Weighted |
|---|---|---|---|
| Security | | `[30% / 35% / 30%]` | |
| Data handling | | `[25% / 30% / 25%]` | |
| Model stability | | `[20% / 15% / 20%]` | |
| Liability and contract | | `[15% / 15% / 15%]` | |
| Audit rights | | `[10% / 5% / 10%]` | |
| **Total** | | **100%** | |

**The weighted score is `[score]` out of 4.0.**

### 5.2 Recommendation

**Use the mapping from §3.4, matched to the use case's tier.**

- If the use case is **Tier 1**: apply the Tier 1 thresholds.
- If the use case is **Tier 2**: apply the Tier 2 thresholds.
- If the use case is **Tier 3**: apply the Tier 3 thresholds.

**Weighted score `[score]` → `[recommendation]`.**

**The recommendation is `[approve / approve with conditions / conditional review / reject]`.**

### 5.3 Risk tier confirmation

**What to write:** one paragraph confirming (or adjusting) the risk tier proposed in §1.4.

**Why it matters:** the tier drives the approval path and the scorecard weights. A review that doesn't confirm the tier is a review that doesn't know what it's assessing.

**Example:**

> The proposed tier is **Tier 2 (High)**. The review confirms the tier assignment:
>
> - The use case **informs** a credit decision (Tier 2 criterion)
> - The analyst remains the **decision-maker** (not Tier 1 — the tool doesn't make the decision)
> - The financial impact of a wrong summary is **significant but bounded** (not Tier 3 — the impact is not "limited")
>
> **The Tier 2 approval path is: AI Governance review → MRC approval.** This review is the AI Governance input; the MRC's approval is a separate step.

**What to avoid:**

- Accepting the proposed tier without assessing it against the policy
- Skipping the "why this tier and not the next one up/down" reasoning
- Forgetting to name the approval path

---

## Section 6 — Conditions for approval

### 6.1 When conditions are required

**Conditions are required when the recommendation is "approve with conditions" or "conditional review."** If the recommendation is "approve," skip this section. If the recommendation is "reject," conditions are not applicable.

**The conditions must be:**

- **Specific** — not "improve security" but "provide a SOC 2 Type II report dated within 12 months"
- **Verifiable** — not "demonstrate commitment" but "contract amendment signed by both parties"
- **Time-bound** — not "eventually" but "within 90 days of MRC approval"
- **Owned** — not "the vendor" but "the vendor, tracked by AI Governance"

**A condition without a verification method is a wish.**

### 6.2 The conditions

| # | Condition | Addresses | Verification | Owner | Timeline |
|---|---|---|---|---|---|
| **C-01** | `[Condition]` | `[Dimension / sub-criterion]` | `[How will we know it's done?]` | `[Who]` | `[When]` |
| **C-02** | `[Condition]` | `[Dimension / sub-criterion]` | `[Verification]` | `[Owner]` | `[Timeline]` |
| **C-03** | `[Condition]` | `[Dimension / sub-criterion]` | `[Verification]` | `[Owner]` | `[Timeline]` |
| `[Additional conditions]` | | | | | |

**Each condition must map to a specific weak dimension or sub-criterion.** A condition that doesn't address a specific weakness is a general wish.

### 6.3 Condition rationale

**For each condition, write one sentence explaining why it's required.**

**Example:**

> **C-01 — Liability cap renegotiation.** The current cap (12 months of fees) is inadequate for a credit workflow. A wrong summary could lead to a materially wrong credit decision, with losses that exceed 12 months of vendor fees. **The 3× annual contract value cap is a minimum; legal may negotiate higher.** The carve-out for model errors is essential — without it, the vendor's liability is capped regardless of the error's cause.

**What to avoid:**

- Conditions without rationale (a reader can't tell why they matter)
- Conditions that restate the policy without applying it (e.g., "the vendor must comply with the policy" — the vendor either does or doesn't; the condition is what makes the difference)

### 6.4 What happens if conditions are not satisfied

**What to write:** the consequence of non-satisfaction, and the time limit.

**Example:**

> If the conditions are not satisfied within 90 days of MRC approval:
>
> 1. The approval is **suspended** — the vendor cannot be deployed.
> 2. The AI Governance Committee **reviews the vendor's progress** at the next scheduled meeting.
> 3. If progress is insufficient, the MRC may **reject the vendor** — the approval is revoked.
>
> **The conditions are not a suggestion.** They're a requirement for deployment. A vendor that doesn't satisfy them is not approved.

**What to avoid:**

- Conditions with no consequence for non-satisfaction (they'll be ignored)
- Conditions with no time limit (they'll slip indefinitely)

---

## Section 7 — Residual risk and acceptance

### 7.1 Residual risk after conditions

**What to write:** a table of the residual risk per dimension, after the conditions are satisfied.

**Why it matters:** the residual risk is what the bank is accepting. A review that says "the vendor is approved" without saying what risk the bank is accepting is a review that doesn't know what it's approving.

**Example table:**

| Dimension | Residual risk | Reasoning |
|---|---|---|
| Security | `[Low / Medium / High]` | `[Why?]` |
| Data handling | `[Low / Medium / High]` | `[Why?]` |
| Model stability | `[Low / Medium / High]` | `[Why?]` |
| Liability | `[Low / Medium / High]` | `[Why?]` |
| Audit rights | `[Low / Medium / High]` | `[Why?]` |

**The residual risk is different from the vendor's risk.** The vendor's risk is what the vendor itself faces. The residual risk is what the bank faces *after* the vendor's controls and the bank's conditions are in place.

### 7.2 Risk acceptance

**What to write:** who accepts the residual risk, and what they accept.

**Example:**

> The residual risk is accepted by the **Chief Risk Officer**, on the recommendation of the AI Governance Committee. The acceptance is documented in the MRC's approval record.
>
> **The acceptance is scoped:** it covers the specific use case (credit memo drafting for commercial credit), not any use of the vendor's product. A new use case requires a new review.

**What to avoid:**

- Accepting residual risk without naming the accepting authority (an acceptance without a signer is not an acceptance)
- Accepting residual risk without specifying the scope (a blanket acceptance is a governance failure)

### 7.3 What the review does not approve

**What to write:** a bulleted list of what the approval does *not* cover.

**Why it matters:** the scope of the approval is as important as the approval itself. A reviewer who reads "the vendor is approved" might think the approval is broad; this section makes it clear it's not.

**Example:**

- **Any use of the vendor's product outside `[specific use case]`.** A new use case (e.g., customer-facing document processing) would require a new review.
- **The vendor's other products.** The review covers the specific product described in §1.4.
- **The vendor's future versions.** A material model change triggers a re-validation requirement under Policy §6.4.

**What to avoid:**

- Approving "the vendor" generically (the approval is always for a specific use case)
- Approving "the product line" (the review covers one product)
- Approving "all future versions" (a new version requires re-validation)

---

## Section 8 — Governance and decision record

### 8.1 Review completion

| Activity | Status | Date |
|---|---|---|
| Evidence collection | `[Complete / In progress]` | `[date]` |
| Scorecard assessment | `[Complete / In progress]` | `[date]` |
| Risk tier confirmation | `[Complete / In progress]` | `[date]` |
| Condition specification | `[Complete / In progress]` | `[date]` |
| Review finalized | `[Complete / In progress]` | `[date]` |

### 8.2 Decision record

| Role | Name | Recommendation | Signature | Date |
|---|---|---|---|---|
| **Reviewer** | `[name]` | `[Approve / Approve with conditions / Conditional review / Reject]` | `[signature]` | `[date]` |
| **Head of AI Governance** | `[name]` | `[Concur / Dissent]` | `[signature]` | `[date]` |
| **Chief Risk Officer** | `[name]` | `[Accept residual risk / Decline]` | `[signature]` | `[date]` |
| **MRC Chair** | `[name]` | `[Approve / Conditional / Reject]` | `[signature]` | `[date]` |

**The decision record is the review's formal conclusion.** The reviewer's recommendation is the input; the Head of AI Governance's concurrence is the governance check; the CRO's acceptance is the risk acceptance; the MRC's approval is the deployment authorization.

**The chain is not optional.** A review without the CRO's acceptance is a recommendation, not a risk acceptance. **The CRO's signature converts the residual risk into an accepted risk.**

### 8.3 Monitoring plan

**What to write:** the ongoing monitoring plan for the vendor relationship.

**Why it matters:** the review is not a one-time event. The vendor's behavior can change, the model can drift, the security posture can degrade. The monitoring plan is how the bank knows the vendor remains approved.

**Example table:**

| Monitoring activity | Frequency | Owner |
|---|---|---|
| SOC 2 refresh | Annual | AI Governance |
| Penetration test report | Annual | AI Governance |
| Model change notification | Per change | Business unit |
| Fallback path test | Semi-annual | Business unit + IT |
| Vendor performance review | Annual | AI Governance + procurement |
| Contract renewal review | Per renewal | AI Governance + legal |

**The monitoring is event-driven for model changes and annual for everything else.** Model changes are the highest-risk event — they trigger a re-validation requirement under Policy §6.4.

**What to avoid:**

- Monitoring plans that only track annual activities (model changes are more frequent)
- Monitoring plans without owners (a monitoring plan without an owner is a monitoring wish)
- Monitoring plans without a re-review trigger (when does the review get refreshed?)

---

## Appendices

### Appendix A — Scorecard summary (one-page view)

| Dimension | Weight | Score (0–4) | Weighted | Evidence tier |
|---|---|---|---|---|
| Security | `[weight]` | | | `[Mixed / Tier 1 / Tier 2 / ...]` |
| Data handling | `[weight]` | | | |
| Model stability | `[weight]` | | | |
| Liability and contract | `[weight]` | | | |
| Audit rights | `[weight]` | | | |
| **Weighted score** | **100%** | | | |
| **Recommendation** | | | | |

### Appendix B — Condition tracker

| Condition | Owner | Target date | Status |
|---|---|---|---|
| `[C-01]` | | | `[Not started / In progress / Complete]` |
| `[C-02]` | | | |
| `[C-03]` | | | |
| `[C-04]` | | | |

### Appendix C — Evidence index

| Evidence | Type | Tier | Date | Source |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |

---

## Document control

| Field | Value |
|---|---|
| **Document ID** | VGR-`[vendor_id]`-`[review_version]` |
| **Version** | `[1.0]` |
| **Status** | `[Draft / Approved / Approved with conditions / Rejected]` |
| **Supersedes** | `[None / previous review]` |
| **Next review** | `[At condition satisfaction / annual / per policy]` |
| **Related documents** | AI Governance Policy (POL-AI-001) §7; Regulatory Gap Analysis (RGA-001); MRC Approval Record |
| **Classification** | Internal — Confidential |

---

## Template version log

| Version | Date | Changes | Author |
|---|---|---|---|
| 1.0 | `[date]` | Initial template | `[author]` |
| | | | |

**When to update this template:**

- **New dimension or sub-criterion** → MINOR version bump (e.g., 1.0 → 1.1)
- **Changed weight** → MINOR version bump (but note the change in the log)
- **Changed threshold mapping** → MAJOR version bump (e.g., 1.0 → 2.0) — this affects every future review's recommendation
- **New evidence tier or changed hierarchy** → MAJOR version bump — this affects every score in every review
