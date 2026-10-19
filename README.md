# Model Analysis Package

**AI-assisted model development and validation, with governance and reproducibility as first-class artifacts.**

This repository is a demonstration of how to package the evidence that a model is (or is not) fit for its stated purpose. It contains two projects, five governance documents, and a shared prompt library. Each project was developed with AI assistance under a fixed prompt protocol; the analyst owns every decision and every interpretation.

## What's in here

- **Two projects**, each with their own frozen deliverables, notebooks, and outputs:
  - **Fannie Mae IFRS 9** — a methodology demonstration of IFRS 9 Expected Credit Loss (ECL) on public mortgage data. Verdict: analyst-authored validation opinion.
  - **Lending Club Credit Risk** — an independent validation of a collections prioritization model on public consumer data. Verdict: machine-authored by Notebook 03 (`authored_by: "NB03"`), inherited by Notebook 04.
- **Five governance documents**, each with a per-project instance:
  1. Model Risk Remediation Plan
  2. Model Risk Validation Report
  3. IFRS 9 Stress Testing Framework (Fannie Mae only)
  4. AI Interaction Record
  5. Reproducibility Record

## Start here

If you have **five minutes**: read [`docs/01-map-cover.md`](docs/01-map-cover.md) — the cover explains what this package is and what it does not claim to be.

If you have **fifteen minutes**: read the cover, then the two Validation Reports:
- [`docs/03-validation-report/fannie-mae-PR004.md`](docs/03-validation-report/fannie-mae-PR004.md)
- [`docs/03-validation-report/lending-club-CR001.md`](docs/03-validation-report/lending-club-CR001.md)

These state the verdict for each project and the specific evidence that supports it.

If you have **an hour**: read the whole `docs/` folder in numeric order (01 → 06), then read one project's `notebooks/` folder end to end.

## What makes this package defensible

Three things, and a reviewer should see all three:

1. **Verdict and evidence are kept separate.** The notebooks produce evidence; the Validation Report states the verdict. In Lending Club, the verdict is machine-authored (NB03) and inherited without recomputation (NB04). In Fannie Mae, it's analyst-authored. Neither project conflates the two.

2. **Every finding is traceable.** Each finding in the Remediation Plan maps to a finding ID in the project's Findings Register, which maps to a specific notebook phase or artifact. There is no finding without an owner, a deadline, and a verification method.

3. **Reproducibility is evidenced, not asserted.** The Reproducibility Record for each project lists the version registry, freeze log, run log, manifest, and environment. The `verify.yml` CI workflow re-runs the check on every push (see [`.github/workflows/verify.yml`](.github/workflows/verify.yml)).

## What this package does NOT claim

- **Not a production model.** Both projects are methodology demonstrations on public proxy data. Neither is validated against a real institution's portfolio.
- **Not IFRS 9 compliant.** IFRS 9 compliance is an institution-specific determination, not a claim a demonstration project can make. The Fannie Mae Validation Report names the specific scope and limitations.
- **Not fair-lending compliant.** The Fannie Mae dataset lacks protected-class attributes; the Lending Club dataset uses a geographic proxy. Both are documented as limitations, not resolved.
- **Not independently validated in the SR 11-7 sense.** Neither project is a second-line validation. Lending Club's Notebook 03 is an independent validation *of the model*; it is not itself independently validated by a third party.

The honesty of the "does not claim" section is what makes the "does claim" sections credible.

## Repository structure

See [`STRUCTURE.md`](STRUCTURE.md) for the directory layout and the role of each folder.

## How to verify

Every artifact in this repository is hashed and listed in [`version-registry.csv`](version-registry.csv). To verify a project's reproducibility:

```bash
python scripts/verify_chain.py --project fannie-mae
python scripts/verify_chain.py --project lending-club
