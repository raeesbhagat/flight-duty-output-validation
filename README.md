# Flight-Duty Extension Screening and Output Validation

Can a rule-based result be traced and independently checked?

This is a public documentation repository for a connected research workstream in Raee Bhagat’s portfolio. It describes methods and decisions from reviewed project materials. It does not contain the original analysis implementation, participant data, or internal research files.

[Portfolio](https://raeeb.dev/) · [Workstream in the project library](https://raeeb.dev/project-library#P14) · [Detailed case study](https://raeeb.dev/projects/validation)

## Research context

Implemented a workflow that evaluates flight records against configured duty-limit rules and produces flagged-record lists and audit workbooks. The code handles time zones, crew-size branches, trip segments, acclimatization assumptions, and cases needing review. A separate validation script recomputes expected fields and compares them with generated outputs. This provides a concrete engineering story involving deterministic business rules, traceable transformations, and verification of saved results.

## What the workflow produces

Flagged-record lists, branch-level audit fields, and source-to-output validation summaries.

## Methods and decisions

- Rule-based classification.
- time-zone conversion.
- boundary conditions.
- source-to-output reconciliation.
- audit trails.
- duplicate-key checks.
- exception reporting.

## Libraries and tools

`R`, `dplyr`, `tidyr`, `lubridate`, `readxl`, `openxlsx`, `knitr`, `R Markdown`, `Excel`.

These tools are associated with the reviewed workstream. This repository is documentation, so it does not install or execute those libraries.

## Analytical structure

**Unit of analysis:** A keyed flight record with crew, time-zone, segment, and required timestamp context.

**Inputs:** Source flight records and configured duty-limit rule inputs, including cases with incomplete or ambiguous fields.

**Output:** Screening classifications, flagged records, audit workbooks, duplicate checks, and reconciliation summaries.

### Normalize and validate inputs

The workflow handles time zones, crew-size branches, multi-segment trips, and acclimatization assumptions. Required keys and timestamps determine whether a record can be evaluated or needs review.

### Make the branch inspectable

Intermediate fields explain how a final classification was reached. A flag without the values and rule branch that produced it is difficult to investigate, especially near a threshold or with incomplete timing information.

### Validate the exported artifact

A separate script recomputes selected expected fields and compares them with saved outputs. This catches discrepancies in the delivered workbook rather than assuming that a script finishing successfully proves correctness.

### Reconcile keys and duplicates

Record identity matters alongside numeric agreement. Reconciliation checks should establish whether the output contains the expected keys and whether duplicate records could change the reported counts.

## Validation and interpretation

- **Boundary values:** Exercise a value just below, exactly at, and just above a configured threshold, and state the inequality used.

- **Missing required inputs:** Send unevaluable cases to review. Missing information should not silently become a pass.

- **Independent computation:** Compare saved outputs with a separately recomputed expectation and retain mismatch fields for investigation.

- **Saved evidence:** Reviewed workbook summaries contain 3,198 checked records and zero mismatches in the checked fields; the portfolio does not rerun the original pipeline.

**Model or calculation:** Source record → normalize → evaluate branch → retain audit fields → independently reconcile

Agreement between an implementation and configured rules is a software-validation result. It does not independently certify the rules or their regulatory applicability.

## Where the methods transfer

Business-rule implementation, boundary handling, exception reporting, and auditability.

## Evidence and boundaries

This summary describes analytical work and its interpretation. It is not a certification, a causal claim, or evidence of a deployed production service.

Saved validation workbooks report 3,198 checked records and zero mismatches in the checked outputs. These are saved summaries, not a pipeline rerun for this portfolio; they do not certify legal or aviation compliance.

The portfolio contains twenty connected workstreams. Several share datasets, preparation logic, research programs, or legacy code. Separate documentation repositories do not imply twenty independent completed studies or exclusive authorship of all underlying research.

## Privacy and reproducibility

- Original datasets, participant identifiers, internal file paths, workbooks, and unpublished source code are not included.
- Public interactive examples on the portfolio use synthetic teaching data and are labeled accordingly.
- There is no install command, runnable research pipeline, or reproducibility claim for this documentation repository.
- No institutional endorsement or ownership of shared research materials is implied.

## Author and contact

Raee Bhagat · [Portfolio](https://raeeb.dev/) · [LinkedIn](https://www.linkedin.com/in/raee-suresh-bhagat-53168890/) · [Email](mailto:raeesbhagat@gmail.com)
