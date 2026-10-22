# Model Risk Validation Report — Lending Club

**Document ID:** MAP-VR-LC-001  
**Version / Status:** 0.1 / Draft  
**Model under review:** Lending Club 4-model ensemble (best: Random Forest, AUC 0.6307)  
**Validation type:** Independent validation (second line)  
**Regulatory basis:** SR 11-7 / OSFI E-23 (reference only; no legal conclusion drawn)

---

## Verdict at a glance

| Field | Value |
|---|---|
| **Risk score** | **6 / 10** |
| **Risk rating** | **HIGH** |
| **Recommendation** | **REJECT for intended use; retain for methodology demonstration only** |
| **Primary driver** | Fairness (region-level DI = 0.5414, SEVERE) — **not** performance |

**Component breakdown:**

| Component | Score | Basis |
|---|---|---|
| Performance | 1 / 3 | AUC 0.631, MODERATE band |
| Stability | 0 / 2 | PSI not assessed (random split) |
| Calibration | 2 / 2 | XGBoost poor |
| **Fairness** | **3 / 3** | **DI 0.5414, SEVERE** |
| Leakage | 0 / 3 | Resolved |

> **The rejection is fairness-driven, not performance-driven.** AUC 0.631 is a MODERATE finding and contributes only 1 of the 6 points. The score reaches HIGH because fairness (3 points) and calibration (2 points) dominate. A reader who sees "AUC 0.631, REJECT" and concludes performance was the driver has misread the verdict.

---

## 1. Executive summary

**Overall model risk rating: HIGH.**  
**Recommendation: REJECT for intended use; retain for methodology demonstration only.**

The model was validated against the DCR's five-component risk score. It scores **6/10 → HIGH → REJECT**. The primary driver is **fairness**, not performance: region-level disparate impact is 0.5414 (SEVERE per DCR §3 FD-01), contributing 3 of the 6 points. Performance (AUC 0.6307) contributes 1 point; calibration (XGBoost poor) contributes 2; stability is not assessed (PSI on a random split is not meaningful) and contributes 0; leakage is resolved and contributes 0.

### Key approval conditions

If the model were ever to be approved (which it is not in this report), the conditions would be:

1. **Fairness** — region-level DI must reach ≥ 0.80 at FD-05-compliant cardinality.
2. **Calibration** — XGBoost HL p > 0.05, and the suspicious HL degeneracy resolved for the other three models.
3. **Split method** — walk-forward or a documented, DCR-approved amendment.

### Material limitations the model user must understand

- The 0.865 developer-claimed AUC is associated with leakage and is **not comparable** to the 0.6307 realistic AUC. The 0.234-point delta (27.1%) is the measured cost of the nine leakage features.
- **PSI is `not_assessed`** — it cannot be computed meaningfully on a random split.
- Fairness testing is region-level (FD-05-compliant) and uses a **state-as-region proxy**, not a direct protected attribute.
- The model is trained on a 100,000-row sample of U.S. Lending Club data and is **not validated for Canadian portfolios**.

---

## 2. Conceptual soundness

### Target definition

The target is a binary default indicator with a **16+ day-late threshold** (finding F-01.06 / F-03.10). This is **not** IFRS 9's 30+ day Stage 3 threshold. The misalignment is documented but not remediated. The conceptual soundness of the target depends on the intended use:

- For **collections prioritization** (the stated intended use per LC-PDR-001), a 16+ day threshold is defensible as an early-warning signal.
- For **IFRS 9 provisioning**, it is not defensible — the threshold is materially earlier than the accounting standard.

**The Validation Opinion should state which intended use it is evaluating against.** As drafted, this report evaluates against collections prioritization and notes that IFRS 9 provisioning is out of scope.

### Feature construction

The four models are trained on 10 included features (from the feature inventory) plus engineered features. The nine leakage features are removed in NB02. The IV column in the feature inventory is a **simplified screening heuristic** (`|corr| × 0.3`, capped at 0.5), not a textbook WOE-based IV — the Validation Opinion should not treat it as a defensible feature-selection statistic.

### Model choice

Four models were trained; Random Forest was selected by held-out AUC. The selection is **within noise** (0.631, 0.621, 0.604, 0.536 for the top four). The Validation Opinion should state that the "best model" choice is defensible but not decisive, and that the AUC spread across the top three is within what one would expect from sampling variation on a 2,000-row validation set.

### Methodology deviation

MD-001 §2 selected walk-forward validation; the run used a random stratified split. The deviation is disclosed (`split_disclosure.method == "random stratified (fallback)"`) and is a HIGH finding (F-02.02 / F-03.02). **The conceptual soundness of the validation is compromised by the split deviation** — a random split understates the model's out-of-time degradation, and the metrics in this report should be read as optimistically biased until a walk-forward rerun is available.

---

## 3. Data quality and inputs

### Source data

Public Lending Club data, used as a proxy for proprietary bank data. The dataset caveat is stated in NB01 Phase 1 and referenced in every downstream notebook. The caveat is **not cosmetic** — it means every conclusion in this report is illustrative, not a claim about any actual portfolio.

### Data quality score: 58.9/100 (POOR)

The score is a composite penalty (missingness 21.1, leakage 15, macro gap 5.0). The Validation Opinion should note:

- The score bands (GOOD ≥80, MODERATE ≥60, POOR ≥40) are **descriptive conventions**, not DCR thresholds.
- The missingness penalty is partly double-counted with the leakage penalty (two of the five high-missingness columns are also leakage features).

### Leakage

Nine features were identified and removed (F-03.01, CRITICAL, RESOLVED). The measured cost of the leakage is **0.234 AUC points** (0.865 → 0.631), or 27.1% of the developer-claimed figure. **This is the single most consequential finding in the validation.** The developer-claimed 0.865 should be cited as a historical claim, not as a benchmark.

### Missingness

Five columns above 20% missing are documented. Imputation strategy is median numeric / mode categorical. The missingness indicators are created and preserved. The Validation Opinion should note that **zero missing values after imputation does not mean the missingness was harmless** — the indicators are the mitigation, not the remedy.

### Macro gap

No macroeconomic indicators in the dataset (F-03.08, HIGH). The model cannot capture economic-cycle risk. This is a **structural limitation**, not a coding defect.

---

## 4. Outcome analysis and testing

### Discrimination

Held-out AUC 0.6307 (Random Forest). KS 0.2671 (Weak). PR-AUC 0.059. The Validation Opinion should state:

- AUC 0.6307 is a **MODERATE-band** finding per DCR §1. It contributes 1 point to the risk score; it does not by itself drive rejection.
- KS 0.2671 (Weak) and PR-AUC 0.059 together indicate limited tail separation — the model's ranking ability in the top decile is weak, which matters for collections prioritization.

### Calibration

XGBoost HL p ≤ 0.05 (poor). HL p ∈ {0.0, 1.0} for Logistic Regression, XGBoost, and Random Forest (suspicious). The Validation Opinion should distinguish:

- **Poor calibration** (XGBoost) is a real finding.
- **Suspicious HL degeneracy** (three models) is a diagnostic issue with the HL implementation, not a calibration finding. The notebook's `Diagnostic` field flags it; the Validation Opinion should not interpret a p-value of exactly 1.0 as evidence of good calibration.

### Fairness

Region-level DI = 0.5414 (SEVERE, cardinality 5, FD-05-compliant, FD-03 group sufficiency applied). This is the **primary rejection driver**. The Validation Opinion should state:

- The test is applied at region level, not per-state one-hot, per FD-05.
- The protected attribute is a **state-as-region proxy**, not a direct race attribute. Fair lending conclusions cannot be drawn from geographic proxies alone.
- The severe result is nonetheless a material finding: it drives the verdict, and it requires remediation before any consequential use.

### Stability

PSI `not_assessed` on a random split. The Validation Opinion should state that stability was **not tested**, not that it passed. The 0-point stability component reflects absence of evidence, not evidence of stability.

### Explainability

SHAP on 100 samples is indicative, not exhaustive. The monotonicity check flags four counterintuitive features (`loan_to_income`, `total_collection_amount_ever`, `annual_income`, `total_credit_limit`). The Validation Opinion should note that counterintuitive SHAP relationships warrant investigation but are not on their own evidence of model failure — they may reflect non-monotone or interaction effects.

### Adversarial testing

The per-state DI diagnostic (NB02 Phase 13) and the region-level FD-05 test (NB03 Phase 10) are both adversarial in spirit. The Validation Opinion should note that the pipeline tests model behaviour under extreme grouping and finds the region-level result material.

---

## 5. Model limitations and assumptions

| ID | Limitation | Impact | Mitigation | Reg ref |
|---|---|---|---|---|
| L1 | PD-LGD correlation is constructed | Convexity illustrative, not empirical | Documented | IFRS 9 §5.5.3 |
| L2 | SICR uses top-decile proxy | Stage 2 is illustrative, not observed SICR | Documented | IFRS 9 §5.5.9 |
| L3 | LGD is a function of PD | Average LGD 44.28% (inside benchmark) | Documented | IFRS 9 §5.5.3 |
| L4 | Prepayment/curtailment are assumptions | EAD approximate | Documented | IFRS 9 §5.5.3 |
| L5 | EIR is industry average | Discounting approximate | Documented | IFRS 9 §5.5.3 |
| L6 | PD cap masks tail convexity | Tail ECL understated pre-cap | NB04 quantifies | IFRS 9 §5.5.17 |
| L7 | Fairness testing incomplete | No direct protected attributes | Documented | ECOA / OSFI E-23 §6.0 |
| L8 | U.S. data as Canadian proxy | Results illustrative | Documented | — |
| L9 | Scenario weights/multipliers assumption-based | Scenario severity directional | Documented | IFRS 9 §5.5.18 |
| L10 | Capital coverage is diagnostic, not adequacy | CET1 is a ratio of RWA, not assets | Documented | Basel III |

**Note on L3:** the LGD-PD functional dependence is a specification choice, not a calibration result. The Validation Opinion should state whether this is acceptable for the intended use. For collections prioritization, it is likely acceptable; for provisioning, it is not.

---

## 6. Recommendations and action plan

**Recommendation: REJECT.** The model is not approved for any consequential use. The methodology demonstration is retained as the project's primary deliverable.

**Required actions** (cross-referenced to the Remediation Plan, MAP-RP-001):

1. **LC-R-01** (fairness): remove state features or reweight; revalidate region DI ≥ 0.80.
2. **LC-R-02** (split): implement walk-forward or document a DCR-approved amendment.
3. **LC-R-03** (calibration): Platt/isotonic for XGBoost; fix or replace HL.
4. **LC-R-04** (discrimination): investigate tail features.
5. **LC-R-05** (scope): IFRS 9 recalibration; macro factors; Canadian validation.

**Re-validation gate:** the model may not be re-submitted for validation until (a) LC-R-01, LC-R-02, and LC-R-03 are closed, and (b) a new pipeline run demonstrates the closure evidence. The re-validation must be performed by an independent reviewer, not the remediation owner.

---

## 7. Findings summary

| Finding ID | Severity | Status | Owner | Timeline |
|---|---|---|---|---|
| F-03.01 | CRITICAL | RESOLVED | Model Dev | Complete |
| F-03.02 | HIGH | OPEN | Model Dev | Next version |
| F-03.03 | CRITICAL | OPEN | Model Risk | 3 months |
| F-03.04 | HIGH | OPEN | Model Dev | 1 month |
| F-03.05 | MEDIUM | OPEN | Model Dev | Next version |
| F-03.06 | HIGH | OPEN | Model Dev | 2 months |
| F-03.07 | HIGH | OPEN | Model Dev | 2 weeks |
| F-03.08 | HIGH | OPEN | Model Dev | 6 months |
| F-03.09 | HIGH | OPEN | Model Risk | 6 months |
| F-03.10 | HIGH | OPEN | Model Dev | 3 months |
| F-03.11 | MEDIUM | OPEN | Model Dev | 1 month |

### Validation opinion sign-off

| Role | Name | Date | Signature |
|---|---|---|---|
| Independent validator | `[ANALYST: name, role]` | `[ANALYST: date]` | `[ANALYST: signature]` |
| Model Risk Committee approval | `[ANALYST: name, role]` | `[ANALYST: date]` | `[ANALYST: signature]` |

> **Note on the placeholders.** The `[ANALYST: ...]` fields are the analyst's contribution, not omissions. The report produces the structure and the evidence; the analyst produces the determination and the signature. A validation report that auto-fills its own sign-off is not an independent validation.

---

*End of document.*
