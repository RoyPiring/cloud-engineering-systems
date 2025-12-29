# Quality Standards

This document defines **how quality is evaluated and verified** for implementations in this repository.

It specifies the **evidence, validation, and review expectations** used to determine whether a system is complete, reviewable, and credible. Architectural intent and operating expectations are defined separately in `OPERATING_REQUIREMENTS.md`.

---

## Scope

These standards apply in the following order of review:

1. **Feature Systems**  
   Curated system views used as primary entry points for review. Feature Systems summarize scope, outcomes, and evidence and route reviewers to their authoritative implementations.

2. **Engineering Systems**  
   Complete, end-to-end system implementations that serve as the source of truth for architecture, implementation, and validation.

3. **Executions and Supporting Artifacts**  
   Pattern-level walkthroughs, procedural guides, and artifacts that support implementation and verification.

Quality is assessed at each level, with clear traceability required between them. Evaluation favors **clarity and honesty over completeness**.

---

## How Quality Is Verified

Quality is evaluated using the mechanisms below.

### 1. System-Level Validation

Each Engineering System includes a `validation.md` file documenting:

- Validation checks relevant to stated scope
- Expected results and observed outcomes
- Assumptions, environment constraints, or limitations
- Supporting evidence where verification occurred

`validation.md` is the **primary quality artifact**.

### 2. Execution Traceability

Systems demonstrate traceability through:

- Ordered execution guides
- Step-by-step implementation documentation
- Explicit links between execution steps and validation checks

Traceability is used to assess completeness and reproducibility.

### 3. Evidence Artifacts

Where verification is performed, evidence may include:

- Logs
- Command output
- Sanitized screenshots
- Metrics or counters
- Test results

Evidence must directly support a validation check. Excess or unrelated artifacts are discouraged.

---

## Quality Dimensions

Quality is evaluated across these dimensions. They describe **how reviewers assess implementations**, not how systems must be designed.

### Correctness
- Validation aligns with documented requirements
- Observed results accurately reflect behavior
- Failure conditions are represented honestly

### Completeness
- Core scope is implemented and validated
- Required documentation is present
- Known gaps or intentional omissions are stated

### Traceability
- Feature Systems map cleanly to Engineering Systems
- Implementation steps map to validation checks
- Claims are supported by concrete references

### Clarity
- Documentation is readable and structured
- Terminology is consistent
- Navigation paths are explicit

### Reproducibility
- Steps can be followed without missing context
- Assumptions and prerequisites are documented
- Validation can be repeated in a comparable environment

---

## Documentation Quality Expectations

Documentation is evaluated for:

- Clear system intent and problem framing
- Explicit scope and non-goals
- Accurate architectural descriptions
- Implementation steps matching deployed behavior
- Validation written in a factual, audit-style format

Narrative explanation may aid understanding. Validation sections remain objective and outcome-focused.

---

## Review Readiness Criteria

An implementation is **review-ready** when:

- A complete execution path exists
- Validation checks are documented
- Expected and observed results are recorded
- Evidence supports verification where applicable
- Assumptions, limitations, or deviations are stated
- Links resolve correctly and point to sources of truth

Review readiness requires **verifiable representation**, not perfection.

---

## Feature Systems Evaluation

Feature Systems are evaluated on:

- Accurate scope representation
- Correct linkage to Engineering Systems
- Faithful summary of outcomes and evidence
- Absence of duplicated, exaggerated, or conflicting claims

Feature Systems must not introduce behavior or guarantees unsupported by their Engineering System.

---

## Quality Checklist (Reviewer Use)

Before considering a system complete:

- [ ] Scope is clearly defined and represented accurately
- [ ] Implementation aligns with documented intent
- [ ] Validation checks are relevant and non-trivial
- [ ] Expected and observed results are recorded
- [ ] Evidence supports validation claims where applicable
- [ ] Execution path is clear and reproducible
- [ ] Assumptions and limitations are documented
- [ ] Feature System summaries align with Engineering Systems

---

## Relationship to Operating Requirements

`OPERATING_REQUIREMENTS.md` defines **target operating expectations** for systems.

This document defines **how quality and completeness are evaluated** against documented behavior and evidence.

Both documents are complementary and should be used together during review.
