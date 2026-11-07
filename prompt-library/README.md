# Prompt Library

## Controlled Delegation — Prompt Library

This is the prompt library for the **Controlled Delegation** method. It is the set of prompts used to accelerate AI-assisted risk analysis while preserving judgment, reproducibility, and accountability.

The library is part of a larger portfolio:

- **Book 1** — *Risk Model Analysis: A Practical Guide to Problem Solving* (the theory of analytical judgment)
- **Book 2** — *Controlled Delegation: How Teams Use AI Without Losing Ownership* (the theory of AI-assisted development)
- **The manual** — *Controlled Delegation: An Operations Manual for AI-Assisted Risk Analysis* (the practice)
- **The prompt library** (this repository) — the prompts used to implement the method
- **The template package** — the artifacts produced by the method

---

## What This Library Is

The prompt library is a collection of reusable prompts. Each prompt has been used, tested, and versioned. The library has three purposes:

1. **Reuse.** A prompt written once can be used again. The analyst does not have to rewrite the prompt for each project.
2. **Review.** A prompt in the library has been reviewed. The review is documented. A new analyst can trust the prompt because it has been tested.
3. **Reproducibility.** A prompt in the library is versioned. When the analyst uses the prompt, they record the version. A reviewer can trace the output to the version of the prompt that produced it.

---

## What This Library Is Not

- It is **not a substitute for the method**. The prompts are tools. The method is the discipline. A reader who uses the prompts without the method will produce output without accountability.
- It is **not exhaustive**. Every project will need additional prompts. The library provides the pattern; the analyst provides the additions.
- It is **not static**. As the analyst learns, the prompts will evolve. The version log records the changes.

---

## The Six Shared Prompts

The shared prompts are the building blocks. They are used in every notebook, in both projects.

| Prompt | Purpose |
|---|---|
| **P1 — Context Setting** | Establish the project, the methodology, and the boundaries |
| **P2 — Task Specification** | Specify the task to be performed |
| **P3 — Acceptance Criteria** | Specify what "success" looks like |
| **P4 — Boundary Enforcement** | Reassert the boundaries if the tool has drifted |
| **P5 — Ambiguity Flagging** | Require the tool to surface ambiguity before implementing |
| **P6 — Self-Documentation** | Require the tool to document its own implementation |

Each shared prompt is in the `shared/` folder. Each has a version, a prompt text, acceptance criteria, and notes.

---

## The Project Prompts

The project prompts are specific to each project. They are organized by notebook.

### Fannie Mae

| Notebook | What it covers |
|---|---|
| Notebook 01 | Data loading and cleaning |
| Notebook 02 | EDA and risk factor analysis |
| Notebook 03 | PD/LGD/EAD calibration |
| Notebook 04 | Stress testing and fairness |
| Notebook 05 | Reporting and dashboard |
| Notebook 06 | Power BI data export |

### Lending Club

| Notebook | What it covers |
|---|---|
| Notebook 01 | Data loading and cleaning |
| Notebook 02 | EDA and risk factor analysis |
| Notebook 03 | Feature engineering |
| Notebook 04 | Model training and evaluation |
| Notebook 05 | Fairness and stability |
| Notebook 06 | Reporting and export |

---

## How to Use the Library

### For a New Project

1. **Read the shared prompts.** Understand the six prompt types. They are the building blocks.
2. **Adapt the context prompt (P1).** Change the project name, the framework, the dataset, and the regulatory anchors.
3. **Adapt the task specifications (P2).** Change the notebook structure and the specific tasks.
4. **Keep the boundaries (P4, P5, P6).** They do not change. They are the discipline.

### For the Fannie Mae Project

1. **Use the Fannie Mae prompts.** They are specific to the project.
2. **Follow the methodology document.** The prompts reference specific sections.
3. **Record every interaction.** Use the AI Interaction Record for every prompt.

### For the Lending Club Project

1. **Use the Lending Club prompts.** They are specific to the project.
2. **Follow the leakage exclusion rules.** They are the most important part of the project.
3. **Record every interaction.** Use the AI Interaction Record.

---

## What to Record

When you use a prompt from the library, record the following:

- The prompt ID and version
- The tool and model version
- The timestamp
- The output reference
- The acceptance criteria result
- Any human edits
- The approval

This is the **AI Interaction Record**. It is the evidence that the prompt was used, the output was reviewed, and the change was approved.

---

## References

The prompt library is based on the following sources:

- **The manual** — *Controlled Delegation: An Operations Manual for AI-Assisted Risk Analysis* (2026)
- **Regulatory anchors:** IFRS 9, OSFI E-23, SR 11-7, ECOA, Basel III, NIST AI RMF, ISO/IEC 42001

---

*The method is the discipline. The analyst is the judgment.*
