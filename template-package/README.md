# Template Package

## Controlled Delegation — Template Package

This is the template package for the **Controlled Delegation** method. It is the set of artifacts produced by the method — the documents that make an analysis defensible.

The template package is part of a larger portfolio:

- **Book 1** — *Risk Model Analysis: A Practical Guide to Problem Solving* (the theory of analytical judgment)
- **Book 2** — *Controlled Delegation: How Teams Use AI Without Losing Ownership* (the theory of AI-assisted development)
- **The manual** — *Controlled Delegation: An Operations Manual for AI-Assisted Risk Analysis* (the practice)
- **The prompt library** — the prompts used to implement the method
- **The template package** (this repository) — the artifacts produced by the method

---

## What This Package Is

The template package is a collection of reusable templates. Each template is a document that the analyst fills in. The templates are the artifacts of the method, in a form that the analyst can adapt to a new project.

The package has three purposes:

1. **Reuse.** A template written once can be used again. The analyst does not have to rewrite the template for each project.
2. **Review.** A template in the package has been reviewed. The review is documented. A new analyst can trust the template because it has been tested.
3. **Reproducibility.** A template in the package is versioned. When the analyst fills in the template, they record the version. A reviewer can trace the artifact to the version of the template that produced it.

---

## What This Package Is Not

- It is **not a substitute for the method**. The templates are tools. The method is the discipline.
- It is **not exhaustive**. Every project will need additional templates. The package provides the pattern; the analyst provides the additions.
- It is **not static**. As the analyst learns, the templates will evolve. The version log records the changes.

---

## The Seventeen Artifacts

The package has seventeen artifacts, organized in six layers.

### Layer 1 — Foundation

| # | Artifact | Purpose |
|---|---|---|
| A01 | Problem Definition Record | Why the model exists |
| A02 | Analytical Specification | What is being analyzed |

### Layer 2 — Methodology

| # | Artifact | Purpose |
|---|---|---|
| A03 | Data Specification | What data is used |
| A04 | Feature Decision Log | What is derived from the data |
| A05 | Methodology Document | How the analysis is implemented |
| A06 | Risk and Validation Plan | How the analysis is validated |
| A07 | Decision Criteria Register | What thresholds determine pass/fail |

### Layer 3 — Execution

| # | Artifact | Purpose |
|---|---|---|
| A08 | Analysis Code | The executable artifact |
| A09 | Edit Log | What the analyst changed |
| A10 | Reproducibility Record | How to reproduce the analysis |

### Layer 4 — Evidence

| # | Artifact | Purpose |
|---|---|---|
| A11 | Results | What the analysis produced |
| A12 | Audit Trail | The chronological record |

### Layer 5 — Judgment

| # | Artifact | Purpose |
|---|---|---|
| A13 | Interpretation Record | What the results mean |
| A14 | Findings | The factual statements |
| A15 | Challenge Record | What could invalidate the findings |
| A16 | Remediation Plan | What will be done |

### Layer 6 — Governance

| # | Artifact | Purpose |
|---|---|---|
| A17 | Approval Record | Who signed off |

---

## The Supporting Templates

In addition to the seventeen artifacts, the package has four supporting templates.

| # | Template | Purpose |
|---|---|---|
| T1 | AI Interaction Record | One-page form with seven fields |
| T2 | Prompt Library Entry | Versioned prompt with acceptance criteria |
| T3 | Pipeline Manifest | Hashes and metadata for every output |
| T4 | Compliance Report | Report with placeholders for analyst claims |

---

## The Template Format

Each template has six parts.

1. **Purpose.** A one-paragraph description of what the template is for.
2. **When to use.** A list of situations where the template applies.
3. **How to fill it in.** A step-by-step guide.
4. **The template.** The document itself, with placeholders.
5. **Worked example.** A filled-in example, drawn from the Fannie Mae or Lending Club project.
6. **Common mistakes.** A list of mistakes the analyst should avoid.

---

## How to Use the Package

### For a New Project

1. **Start with the foundation.** Fill in the Problem Definition Record (A01) and the Analytical Specification (A02).
2. **Move to the methodology.** Fill in the Data Specification (A03), the Feature Decision Log (A04), the Methodology Document (A05), the Risk and Validation Plan (A06), and the Decision Criteria Register (A07).
3. **Freeze the design artifacts.** Once the seven design artifacts are complete, freeze them. They become the contract for the analysis.
4. **Execute the analysis.** Produce the Analysis Code (A08), the Edit Log (A09), and the Reproducibility Record (A10).
5. **Collect the evidence.** Produce the Results (A11) and the Audit Trail (A12).
6. **Make the judgment.** Produce the Interpretation Record (A13), the Findings (A14), the Challenge Record (A15), and the Remediation Plan (A16).
7. **Obtain approval.** Produce the Approval Record (A17).

### For the Fannie Mae Project

1. **Use the Fannie Mae examples.** They are in the `examples/fannie_mae/` folder.
2. **Follow the methodology.** The templates reference specific sections.
3. **Record every decision.** The templates are the record.

### For the Lending Club Project

1. **Use the Lending Club examples.** They are in the `examples/lending_club/` folder.
2. **Follow the leakage exclusion rules.** They are the most important part of the project.
3. **Record every decision.** The templates are the record.

---

## The Worked Examples

The package has two worked examples:

- **Fannie Mae** — the mortgage version. Shows the templates filled in for a mortgage portfolio.
- **Lending Club** — the consumer lending version. Shows the templates filled in for a consumer lending portfolio.

The two examples show how the same templates adapt to different domains. The Fannie Mae example is the reference. The Lending Club example is the transferability demonstration.

---

## What to Record

When you fill in a template, record the following:

- The template ID and version
- The date
- The author
- The freeze timestamp (if applicable)
- The sign-off

The template is the artifact. The metadata is the evidence that the artifact was produced deliberately.

---

## References

The template package is based on the following sources:

- **The manual** — *Controlled Delegation: An Operations Manual for AI-Assisted Risk Analysis* (2026)
- **Regulatory anchors:** IFRS 9, OSFI E-23, SR 11-7, ECOA, Basel III, NIST AI RMF, ISO/IEC 42001

---
*The templates are the evidence. The analyst is the judgment.*
