# IFRS 9 Stress Testing Framework — Fannie Mae

**Document ID:** MAP-STF-FM-001  
**Version / Status:** 0.1 / Draft  
**Model under review:** Fannie Mae mortgage PD/LGD/EAD and illustrative ECL scenario pipeline  
**Framework basis:** IFRS 9 §5.5.3, §5.5.9, §5.5.11, §5.5.17, §5.5.18 (reference only; no compliance conclusion drawn)

---

## Framework at a glance

| Component | Implemented? | Evidence | Key limitation |
|---|---|---|---|
| PD calibration | Yes | NB03 §3 | Summary statistic, not fitted |
| LGD calibration | Yes | NB03 §4 | Deterministic, function of PD |
| EAD calculation | Yes | NB03 §5 | `ORG_UPB` base; AP-03 band breach (86.95%) |
| Stage classification | Yes | NB03 §3 | SICR-by-construction; C6 default×5 |
| ECL per stage | Yes | NB03 §6 | Single-period |
| Probability-weighted ECL | Yes | NB04 §4 | Scenario multipliers not calibrated |
| Macro conditioning | **No** | — | Multipliers are narrative, not computational |
| Transition matrices | **No** | — | Single-period snapshot, not projection |
| Front-loading / cliff effects | **No** | — | Not modelled |
| Capital adequacy | **No** | — | Coverage diagnostic only |

**Headline numbers (per loan):** PD 0.95% · LGD 44.28% · EAD ~$204,745 · probability-weighted ECL ~$2,231 · coverage diagnostic 22.31% of assumed total assets.

> **This framework does not declare IFRS 9 compliance.** The Fannie Mae pipeline computes the components IFRS 9 requires, but the pipeline's own claim-authorization discipline stops it from writing a compliance verdict. Every compliance status field in NB05 is an analyst placeholder. This document presents the framework as the pipeline implements it, states the evidence, and **leaves the compliance determination to the Validation Opinion**.

---

## 1. Framework scope and claim-authorization discipline

**This framework does not declare IFRS 9 compliance.** The Fannie Mae pipeline computes the components IFRS 9 requires (PD, LGD, EAD, staging, probability-weighted ECL), but the pipeline's own claim-authorization discipline stops it from writing a compliance verdict. Every compliance status field in NB05 is an analyst placeholder (`[ANALYST: insert status]`). This document is the analyst's contribution: it presents the framework as the pipeline implements it, states the evidence, and **leaves the compliance determination to the Validation Opinion**.

The pipeline's claim-authorization discipline is the framework's central governance feature. It is why this framework can be used as a methodology demonstration without over-claiming. The framework document should be read as **"here is what the pipeline computes and how"**, not as **"here is what the regulator will conclude."**

---

## 2. Macroeconomic conditioning

**The pipeline does not condition on macroeconomic variables.** The scenario ECLs are driven by analyst-specified PD and LGD multipliers (1.0×/1.8×/3.0×/4.5× for PD; 1.0×/1.2×/1.5×/2.0× for LGD), not by GDP/unemployment/HPI projections. The scenario definitions include macro assumptions (GDP, unemployment, HPI) for narrative context, but those assumptions are **not inputs to the calculation**.

This is a material limitation. A true IFRS 9 stress test would map macro scenarios to PD/LGD via a calibrated satellite model. The pipeline does not. The framework document should state:

- The scenario multipliers are **analyst-specified heuristics**, not calibrated to the portfolio.
- The macro assumptions are **narrative**, not computational.
- Recalibration to macro-conditional PD/LGD is **required** before the framework can be used for any accounting or regulatory purpose.

**Suggested remediation:** FM-R-06 in the Remediation Plan (recalibrate scenario multipliers against portfolio-specific historical data).

---

## 3. Stage migration and transition matrices

**The pipeline does not implement transition matrices.** Stage classification is a single-period assignment:

- **Stage 3:** `default == 1` (the `delinquency_state >= 3` condition is equivalent, because `delinquency_state` is constructed as `default × 5` in NB01 — the C6 limitation).
- **Stage 2:** top-decile of non-Stage-3 loans by `pd_estimate` (**SICR-by-construction**, not observed credit deterioration).
- **Stage 1:** all other loans.

### The Stage 2 mechanism is the framework's most important interpretive point

A reader must not read "Stage 2 = 9.9%" as "9.9% of the portfolio had a significant increase in credit risk." It means "the top-decile proxy assigns 9.9% of loans to Stage 2." The framework document should state this prominently, and the NB03 callout (see appendix) should carry the same language.

### Transition matrices are required for a true IFRS 9 stress test

They model how loans migrate between stages over the stress horizon. The pipeline does not implement this. The framework document should state:

- The stage distribution is a **point-in-time snapshot**, not a projection.
- The stress horizon is **not modelled** — the scenario ECLs are single-period, not multi-period.
- Transition matrices and Markov-chain migration are **out of scope** for this framework and would be required for a production IFRS 9 implementation.

**Suggested remediation:** FM-R-07 (acquire current credit characteristics; implement observed SICR); a longer-horizon roadmap item for transition matrices.

---

## 4. Front-loading and cliff effects

**The pipeline does not model front-loading.** The scenario ECLs are single-period expected losses, not a projection of impairment provisions over time. The framework does not implement the IFRS 9 acceleration of impairment recognition (the "front-loading" of provisions in the first 12–24 months).

The framework document should state:

- The pipeline computes a **point-in-time ECL** (per-loan, per-scenario), not a **provisioning trajectory**.
- Front-loading and cliff effects are **not modelled**.
- A production IFRS 9 implementation would require a multi-period projection with stage transition.

---

## 5. Single scenario vs multi-scenario adjustments

**The pipeline implements multi-scenario probability-weighted ECL.** Four scenarios (baseline, adverse, severely adverse, tail risk) with weights 45/30/15/10. This is the IFRS 9 §5.5.17 requirement.

**The scenario weights are analyst-specified, not calibrated.** The framework document should state:

- Weights sum to 1.00 (verified in NB04 config).
- The weights are not calibrated to any specific portfolio's loss distribution.
- The severity check (ratio 1.27× vs historical 2008 average) is **directional**, not empirical.

**The 1.27× ratio is an investigation trigger (AP-05, IT-05).** The framework should state that the severely adverse scenario is **not severe enough by the DCR's 1.5× target**, and that this is a HIGH finding (FM-R-06) requiring recalibration.

---

## 6. Capital coverage — a note on the reframe

**The pipeline computes capital coverage, not capital adequacy.** The distinction is material:

- **Coverage:** "How much of an assumed asset base would be consumed by ECL under stress?" The ECL-as-%-of-assets metric answers this.
- **Adequacy:** "Does the bank have enough capital to survive the stress?" This requires RWA, actual CET1, and institution-specific buffers. None of those are in the pipeline.

The framework reports:

| Metric | Value |
|---|---|
| ECL as % of assets (weighted) | 22.31% |
| ECL as % of assets (tail) | 75.12% |
| ECL/CET1 ratio (weighted) | **495.8% — diagnostic only, not a capital adequacy finding** |

**The framework document must not present ECL/CET1 as a capital adequacy finding.** The CET1 figure is 4.5% of total assets, not 4.5% of RWA — the ratio is a scale artifact. The framework should present the coverage metric as the headline and the ECL/CET1 as a footnote with the scale-mismatch disclaimer.

**Suggested remediation:** FM-R-08 (EAD ratio) and FM-R-10 (PD cap disclosure) both affect the ECL-as-%-of-assets metric. Both should be resolved before the coverage metric is cited.

---

## 7. Framework observations for the reader

The following observations are **not findings** — they are scope limitations and interpretive points the reader must understand when citing this framework.

**Observation 1 — EAD ratio outside configured band (FM-R-08).** The EAD ratio is 86.95% against a configured 50–85% band. AP-03 fired. The notebook says "check CCF first"; the notebook's own CCF=0 assertion means the cause is elsewhere. Two candidate causes: young loan sample (avg 16 months) means prepayment/curtailment factors near 1.0; `ORG_UPB` used as exposure base instead of current UPB. The reader should not cite EAD or ECL without disclosing the ratio and the AP-03 warning.

**Observation 2 — Stage 2 is by construction.** Stage 2 = 9.9% is the top-decile proxy, not observed SICR. The reader must not present 9.9% as a portfolio SICR rate. It must present it as "the top-decile proxy assigns 9.9% of loans to Stage 2."

**Observation 3 — PD cap effect is zero in the current run.** The cap (20%) does not fire at the per-loan scenario level because tail PD = 4.29% < 20%. The cap would fire if base PD rose. The reader must disclose the cap and its conditional effect.

**Observation 4 — Severity ratio below target.** The 1.27× ratio is below the 1.5× target. The reader must decide whether to accept the scenario as-is (with the IT-05 trigger documented) or require recalibration (FM-R-06).

**Observation 5 — Fairness testing incomplete.** Geographic proxies at cardinality 52/328/638 produce degenerate DI = 0.00%. Fairness testing is **incomplete, not failed**. The 4/5ths rule is misapplied at high cardinality. The correct conclusion is a data limitation.

**Observation 6 — Reconciliation warnings on `base_pd` are expected.** The dataframe's mean `pd_estimate` is 5.8%, while NB03's `unconditional_pd` is 0.95%. These are different by design (per-loan score vs sample default rate). The reconciliation warning is not an error.

**Observation 7 — Claim-authorization discipline.** No notebook in the pipeline writes a compliance verdict. Every status field is an analyst placeholder. The reader should state this explicitly as a governance strength.

---

## 8. Framework summary

| Component | Implemented? | Evidence | Limitation |
|---|---|---|---|
| PD calibration | Yes | NB03 §3 | Summary statistic, not fitted |
| LGD calibration | Yes | NB03 §4 | Deterministic, function of PD |
| EAD calculation | Yes | NB03 §5 | `ORG_UPB` base; AP-03 band breach |
| Stage classification | Yes | NB03 §3 | SICR-by-construction; C6 default×5 |
| ECL per stage | Yes | NB03 §6 | Single-period |
| Probability-weighted ECL | Yes | NB04 §4 | Scenario multipliers not calibrated |
| Macro conditioning | No | — | Multipliers are narrative, not computational |
| Transition matrices | No | — | Single-period snapshot, not projection |
| Front-loading / cliff effects | No | — | Not modelled |
| Capital adequacy | No | — | Coverage diagnostic only |

### Framework sign-off

| Role | Name | Date | Signature |
|---|---|---|---|
| Model Development owner | `[ANALYST: name, role]` | `[ANALYST: date]` | `[ANALYST: signature]` |
| Validation Opinion author | `[ANALYST: name, role]` | `[ANALYST: date]` | `[ANALYST: signature]` |

> **Note on the placeholders.** The `[ANALYST: ...]` fields are the analyst's contribution, not omissions. The framework produces the evidence; the analyst produces the determination and the signature.

---

## Appendix — "Stage 2 by construction" callout in NB03

The current NB03 output contains the caveat, but it is buried in the Phase 3 output between the stage table and the LGD section. A reader who skims will miss it. **Promote it to a Jupyter Markdown cell immediately after the Stage distribution print, before the LGD section begins.**

The suggested Markdown cell content:

> ### ⚠️ Stage 2 is SICR-by-construction — not observed credit deterioration
>
> **The Stage 2 fraction (9.9% in this run) is the top decile of non-Stage-3 loans by `pd_estimate`. It is a construction, not a measurement.**
>
> The dataset contains origination characteristics only. It does not contain current credit characteristics. A true IFRS 9 SICR assessment cannot be performed on this data.
>
> **What this means for downstream readers:**
>
> - **Do not read "9.9% Stage 2" as "9.9% of the portfolio had a significant increase in credit risk."** It means "the top-decile proxy assigned 9.9% of loans to Stage 2."
> - **Do not compare this 9.9% to a bank's reported Stage 2 fraction** without accounting for the difference between observed SICR and proxy SICR.
> - **Do not use the Stage 2 fraction as evidence of portfolio credit deterioration.** It is a proxy artefact.
>
> **Reference:** Finding F-07; Limitation L2 in `notebook_03_limitations.csv`; Remediation Plan finding **FM-R-07**.

---

*End of document.*
