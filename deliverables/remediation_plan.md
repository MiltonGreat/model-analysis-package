# Model Risk Remediation Plan

**Document ID:** MAP-RP-001  
**Version / Status:** 0.1 / Draft  
**Scope:** Cross-project (Lending Club + Fannie Mae)  
**Findings in scope:** 10 (selected from both pipelines' registers; selection rationale below)  
**Roadmap horizon:** 6 months from approval

---

## Findings at a glance

| # | Finding ID | Source project | Severity | Tier | SLA | Status |
|---|---|---|---|---|---|---|
| 1 | LC-R-01 | Lending Club | CRITICAL | Tier 1 | M3 | OPEN |
| 2 | LC-R-02 | Lending Club | HIGH | Tier 1 | M3 | OPEN |
| 3 | LC-R-03 | Lending Club | HIGH | Tier 2 | M1 / next version | OPEN |
| 4 | LC-R-04 | Lending Club | HIGH | Tier 2 | M2 | OPEN |
| 5 | LC-R-05 | Lending Club | HIGH | Tier 1 | M3 / M6 | OPEN |
| 6 | FM-R-06 | Fannie Mae | HIGH | Tier 2 | M2 | OPEN |
| 7 | FM-R-07 | Fannie Mae | HIGH | Tier 2 | M3 | OPEN |
| 8 | FM-R-08 | Fannie Mae | HIGH | Tier 1 | M1 / M2 | OPEN |
| 9 | FM-R-09 | Fannie Mae | HIGH | Tier 2 | M6 | OPEN |
| 10 | FM-R-10 | Fannie Mae | MEDIUM | Tier 3 | M6 (ongoing) | OPEN |

> **What this table is not.** It is not a status tracker — the live tracker is the MRM dashboard described in Section 7. This table is a reading aid so a reviewer can see the scope of the plan in one view before reading the root-cause detail.

---

## 1. Purpose and scope

This plan tracks the closure of model risk findings raised across the Lending Club and Fannie Mae pipelines. It is **not a validation opinion** and does not itself authorize or reject any model. It records what is broken, who owns the fix, how the fix will be evidenced, and when the fix must be closed — the audit trail between a finding being raised and a finding being closed.

Ten findings are in scope. They were selected because they are:

- **(a)** severity CRITICAL or HIGH in the source registers,
- **(b)** material to the deployability of the model they affect, and
- **(c)** closeable within a 6-month horizon with identifiable evidence.

Findings that are documentation-only, or that require data the project does not have (e.g., acquisition of direct protected attributes), are recorded in the Validation Opinions but **not** in this remediation plan — they are not closeable within the horizon and belong in a longer-horizon roadmap.

### Scope exclusions

- **Legal conclusions** about ECOA, OSFI E-23, SR 11-7, or IFRS 9 compliance are out of scope. The plan tracks the *model risk* findings, not the regulatory determinations.
- **Production deployment**, Canadian portfolio validation, and full protected-class fairness assessment are out of scope — they are downstream of closure, not part of it.

---

## 2. Issue identification and root cause analysis

| Finding ID | Source | Severity | Root cause category |
|---|---|---|---|
| LC-R-01 | LC F-03.01 / F-03.03 | CRITICAL | Conceptual — fairness |
| LC-R-02 | LC F-02.02 / F-03.02 | HIGH | Methodology — split |
| LC-R-03 | LC F-02.04 / F-03.04 | HIGH | Calibration |
| LC-R-04 | LC F-03.06 | HIGH | Discrimination |
| LC-R-05 | LC F-03.08 / F-03.09 / F-03.10 | HIGH | Data / scope |
| FM-R-06 | FM NB03 AP-04 (no fire) / NB04 AP-05 | HIGH | Scenario calibration |
| FM-R-07 | FM NB03 stage output | HIGH | Methodology — SICR |
| FM-R-08 | FM NB03 AP-03 | HIGH | EAD calibration |
| FM-R-09 | FM NB04 fairness | HIGH | Fairness — scope |
| FM-R-10 | FM NB04 L3 / NB03 L6 | MEDIUM | Parameter stability |

### Root cause detail

**LC-R-01 — Conceptual (fairness).** Region-level DI = 0.5414 (SEVERE). State features act as a region proxy for protected-class membership. The model's learned relationship between geography and default is a **proxy-validity problem**, not a coding defect.

**LC-R-02 — Methodology (split).** Random stratified split used instead of MD-001's intended walk-forward split. Root cause: `issue_month` (the only date candidate) is a leakage feature, so no origination-date column survives leakage removal. The methodology could not be executed as specified on this dataset.

**LC-R-03 — Calibration.** XGBoost HL p ≤ 0.05. Additionally, HL p ∈ {0.0, 1.0} for three of four models (suspicious/degenerate). Root cause: HL implementation and/or prediction concentration. The calibration finding is real; the degeneracy is a separate diagnostic issue.

**LC-R-04 — Discrimination.** KS = 0.2671 (Weak), PR-AUC = 0.059. Tail separation is limited. Root cause: weak univariate signal from the available origination features on a low-frequency event, combined with class imbalance.

**LC-R-05 — Data / scope.** No macro factors; U.S. data not validated for Canada; 16+ day target vs IFRS 9 30+ day. Root cause: dataset scope. These are structural limitations, not coding defects.

**FM-R-06 — Scenario calibration.** Severity ratio 1.27× vs 1.5× target. Scenario multipliers not calibrated to the portfolio. Root cause: multipliers are analyst-specified from 2008 heuristics, not fitted.

**FM-R-07 — Methodology (SICR).** Stage 2 is SICR-by-construction (top-decile proxy), not observed credit deterioration. Root cause: dataset lacks current credit characteristics. Stage 2 fraction is a construction, not a measurement.

**FM-R-08 — EAD calibration.** EAD ratio 86.95%, outside the 50–85% band. Root cause candidates:

- **(a)** young loan sample (avg 16 months) so prepayment/curtailment factors near 1.0;
- **(b)** `ORG_UPB` used as exposure base instead of current UPB.

The notebook flags the band breach; it does not resolve the cause.

**FM-R-09 — Fairness (scope).** Fairness testing on geographic proxies at cardinality 52/328/638 is degenerate (DI = 0.00%, UNRELIABLE). Root cause: no direct protected attributes; 4/5ths rule misapplied at high cardinality. Same structural limitation as LC-R-05, different mechanism.

**FM-R-10 — Parameter stability.** PD cap (20%) understates tail convexity. Current run cap effect = 0.0% understated, but the cap fires if base PD rises. Root cause: stability measure that is anti-conservative for tail PD.

---

## 3. Model tiering and prioritization

Tiering is a function of **(a)** financial materiality, **(b)** complexity, and **(c)** usage scale. Both projects are methodology demonstrations, not production models, so the tier assignment reflects **the tier the model would carry if it were promoted to its stated intended use**, not its current demonstration status.

| Finding ID | Tier | Materiality rationale | Remediation SLA |
|---|---|---|---|
| LC-R-01 | Tier 1 (High) | Fairness finding drives the REJECT verdict; a model with SEVERE DI cannot be used for any consequential decision | 3 months |
| LC-R-02 | Tier 1 (High) | Random split understates out-of-time degradation; walk-forward is a prerequisite for any production claim | 3 months (or documented DCR amendment) |
| LC-R-03 | Tier 2 (Medium) | Calibration affects threshold-based decisions; XGBoost poor + HL degeneracy | 1 month (calibration) / next version (HL implementation) |
| LC-R-04 | Tier 2 (Medium) | KS 0.2671 limits collections prioritization utility | 2 months |
| LC-R-05 | Tier 1 (High) | Structural limitations gate any Canadian deployment and any IFRS 9 provisioning claim | 6 months (macro + Canadian validation) / 3 months (IFRS 9 recalibration) |
| FM-R-06 | Tier 2 (Medium) | Scenario severity is directional; the 1.27× ratio is an investigation trigger, not a failure | 2 months |
| FM-R-07 | Tier 2 (Medium) | SICR-by-construction is a scope limitation; it affects the interpretation of Stage 2 ECL, not the computation | 3 months (data acquisition) / documented limitation otherwise |
| FM-R-08 | Tier 1 (High) | EAD ratio outside band affects every ECL number downstream | 1 month (diagnosis) / 2 months (resolution) |
| FM-R-09 | Tier 2 (Medium) | Fairness testing is incomplete, not failed; the limitation is structural | 6 months (data acquisition) |
| FM-R-10 | Tier 3 (Low) | PD cap effect is 0.0% in the current run; monitor | 6 months (monitoring) |

### Prioritization order for the 6-month roadmap

1. **Month 1:** FM-R-08 diagnosis (EAD ratio — resolve `ORG_UPB` vs current UPB, confirm prepayment/curtailment factor calibration); LC-R-03 XGBoost calibration (Platt scaling).
2. **Months 1–2:** FM-R-08 resolution; LC-R-04 feature-set investigation for tail discrimination.
3. **Months 2–3:** LC-R-01 fairness remediation (remove state features or reweight); LC-R-02 walk-forward implementation or DCR amendment; FM-R-06 scenario multiplier recalibration.
4. **Months 3–4:** LC-R-05 IFRS 9 recalibration (16+ → 30+ day); FM-R-07 data acquisition for current credit characteristics (or documented permanent limitation).
5. **Months 4–6:** LC-R-05 macro factors + Canadian validation; FM-R-09 protected-attribute data acquisition; FM-R-10 monitoring.

---

## 4. Remediation actions and milestones

Each row has an **action owner** (role), a **milestone date** (relative to plan approval), and **evidence that closure will require**.

| Finding ID | Action | Owner | Milestone | Closure evidence |
|---|---|---|---|---|
| LC-R-01 | Remove state features from feature set; rerun NB02/NB03; confirm region DI ≥ 0.80 or document why reweighting is preferable | Model Development + Model Risk | M3 | New NB03 run with DI ≥ 0.80 at FD-05-compliant cardinality, or documented reweighting methodology approved by Model Risk |
| LC-R-02 | Implement walk-forward split using a date column that survives leakage removal; or amend MD-001 §2 with a documented DCR-approved exception | Model Development | M3 | New NB02 with `split_disclosure.method == "walk-forward"`, or signed DCR amendment |
| LC-R-03 | Apply Platt scaling or isotonic regression to XGBoost; re-assess HL; fix HL implementation (or replace with Spiegelhalter Z-test) | Model Development | M1 (calibration) / next version (HL) | New NB02 calibration table with HL p > 0.05 and no suspicious p ∈ {0.0, 1.0} |
| LC-R-04 | Investigate feature set for tail discrimination; consider ensemble or richer features; document why 0.2671 KS is or is not acceptable for the intended use | Model Development | M2 | New NB03 KS result, or documented acceptance with business rationale |
| LC-R-05 | (a) Add macro indicators; (b) validate on Canadian data; (c) recalibrate to 30+ day IFRS 9 target | Model Development + Model Risk | M3 (IFRS 9) / M6 (macro + Canada) | New NB01/NB02/NB03 artifacts demonstrating each sub-item |
| FM-R-06 | Recalibrate scenario multipliers against portfolio-specific historical data; document the calibration source | Model Development | M3 | New NB04 with severity ratio ≥ 1.5×, or documented rationale for accepting < 1.5× |
| FM-R-07 | Acquire current credit characteristics (or document permanent limitation); recalibrate Stage 2 logic if data acquired | Model Development + Data Owner | M3 (or documented limitation) | New NB03 stage output with observed SICR, or signed limitation in Validation Opinion |
| FM-R-08 | Diagnose EAD ratio: confirm whether `ORG_UPB` or current UPB is the correct exposure base; recalibrate prepayment/curtailment factors if needed | Model Development | M1 (diagnosis) / M2 (resolution) | New NB03 with EAD ratio in 50–85% band, or documented rationale for the band definition |
| FM-R-09 | Acquire direct protected attributes (HMDA-equivalent); rerun fairness at low cardinality | Model Risk + Data Owner | M6 | New NB04 fairness result at cardinality ≤ 50, or documented permanent limitation |
| FM-R-10 | Monitor PD cap effect across runs; recalibrate cap if base PD rises | Model Development | M6 (ongoing) | Monitoring report showing cap effect across runs |

---

## 5. Compensating controls

While permanent fixes are under development, the following compensating controls apply:

| Finding ID | Compensating control | Owner | Duration |
|---|---|---|---|
| LC-R-01 | Do not use the model for any consequential decision. Scores may be used for research and methodology demonstration only. If a decision is required, use a documented manual override with Model Risk approval. | Model Risk | Until M3 |
| LC-R-02 | Treat all metrics as in-sample optimistic; do not cite AUC/KS as evidence of out-of-time performance. | Model Development | Until M3 |
| LC-R-03 | Use Logistic Regression (HL p = 1.0 but flagged suspicious, not poor) instead of XGBoost for any threshold-based use, with the caveat that LR held-out AUC is 0.536. If a calibrated model is required, apply a post-hoc calibration layer. | Model Development | Until M1 |
| LC-R-04 | Do not use the model for tail prioritization (top-decile collections); the KS/PR-AUC results do not support it. | Model Risk | Until M2 |
| LC-R-05 | Label every output as U.S. proxy, illustrative only. Do not cite in Canadian regulatory submissions or IFRS 9 provisioning. | Model Risk | Until M6 |
| FM-R-06 | Label the severely adverse scenario as directional only; do not cite the 1.27× ratio as evidence of scenario adequacy. | Model Development | Until M3 |
| FM-R-07 | Label Stage 2 as "SICR by construction" in every downstream report; do not present 9.9% as observed SICR. | Model Development | Until M3 |
| FM-R-08 | Do not rely on EAD or ECL numbers until the EAD ratio is resolved. If ECL is cited, include the EAD ratio and the AP-03 warning. | Model Risk | Until M2 |
| FM-R-09 | Label fairness testing as incomplete, not failed; do not cite DI = 0.00% as evidence of unfairness or of fairness. | Model Risk | Until M6 |
| FM-R-10 | Include PD-cap effect in every ECL report; do not present tail ECL without the cap disclosure. | Model Development | Ongoing |

---

## 6. Independent re-validation and sign-off

Each finding's closure requires **independent re-validation**, not self-attestation by the remediation owner. The re-validation must be performed by a reviewer who did not implement the fix, and the evidence must be a **new pipeline run** (not a narrative claim).

### Closure evidence template per finding

- Finding ID and severity
- Root cause (from Section 2)
- Action taken (from Section 4)
- New run ID(s) and artifact hashes for the evidence
- Before / after comparison (metric, direction, magnitude)
- Residual risk (what remains after the fix)
- Independent reviewer name, role, date, signature
- Closure approval (Model Risk Committee or delegate)

### Sign-off table

> **Note on the placeholders.** The `[ANALYST: insert]` fields below are the analyst's contribution, not omissions. The plan produces the structure; the analyst produces the closure evidence and the signature. This is deliberate — a remediation plan that auto-fills its own sign-off is not an independent re-validation.

| Finding ID | Closure evidence run ID | Residual risk | Independent reviewer | Date | Approved |
|---|---|---|---|---|---|
| LC-R-01 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |
| LC-R-02 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |
| LC-R-03 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |
| LC-R-04 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |
| LC-R-05 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |
| FM-R-06 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |
| FM-R-07 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |
| FM-R-08 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |
| FM-R-09 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |
| FM-R-10 | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` | `[ANALYST: insert]` |

---

## 7. Executive tracking and reporting

The plan is tracked in the **MRM dashboard** with the following fields per finding:

- **Status:** OPEN / IN PROGRESS / CLOSED / DEFERRED
- **Days open** (from finding raise to closure)
- **Days remaining** to SLA
- **SLA breach flag** (red / amber / green)
- **Escalation flag** (CRITICAL findings escalate to MRC immediately; HIGH findings escalate on SLA breach)
- **Owner**
- **Evidence artifact** (link to the new run's manifest)

### Monthly reporting to the Model Risk Committee

- Findings closed this month
- Findings slipping past SLA
- Findings with residual risk above threshold
- Any finding where the remediation action has changed scope

### Board-level visibility

For the two CRITICAL findings (LC-R-01, LC-R-03 at CRITICAL-band calibration; FM-R-08 is HIGH but material) and for any finding where SLA is breached by more than 30 days.

---

*End of document.*
