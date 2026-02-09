# Business Context: AI CICD E2E GitHub Actions Gemini

## Executive Summary

This engineering system establishes **end-to-end AI-augmented CI/CD** using GitHub Actions and the Gemini API. It delivers automated testing, AI-driven pull request code review, coverage-gated AI test generation, and related automation so that code changes are validated consistently before merge or release.

The business objective is to **reduce delivery risk and reviewer load** by automating tests, embedding AI review in the PR workflow, and generating tests when coverage would otherwise drop, without introducing untraceable or manual-only steps.

This document defines the problem, requirements, constraints, and success criteria that drive all architectural and implementation decisions in this system.

---

## Business Problem

Manual or tool-siloed CI practices introduce recurring risks:

- Broken code reaching main due to inconsistent or late test feedback
- Security and quality issues slipping through without structured review
- Low test coverage on new code paths when tests are written only manually
- Reviewer fatigue and inconsistent standards across pull requests
- Build and artifact handling that is not repeatable or traceable

These issues increase deployment risk, slow feedback, and make it harder to scale review and testing as the codebase grows.

The business requires an engineering system that is **automated by default**, uses AI in defined, auditable ways, and ties every claim to execution evidence.

---

## Business Objectives

The system is designed to achieve the following objectives:

1. **Establish a Reliable CI Baseline**  
   Run Python tests automatically on every push via GitHub Actions, with consistent environment and artifact packaging.

2. **Introduce AI as a First-Class Reviewer**  
   Use the Gemini API to analyze PR diffs for security risks, logic errors, and code quality before human review or merge.

3. **Increase Test Coverage with AI When Needed**  
   Use coverage gates so AI-generated tests run only when coverage would drop below a threshold, balancing quality and cost.

4. **Enforce Evidence-Based Validation**  
   Ensure all behavior is documented in execution records and validation maps to those executions.

---

## Success Criteria (Measurable)

The system is considered successful when the following conditions are met:

- **CI Pipeline**
  - Workflow runs on push; Python environment and pytest execute consistently
  - Pipeline detects intentional test failures and passes after fixes
  - Build artifacts are produced and downloadable from the workflow run

- **AI Code Review**
  - PR-triggered workflow retrieves diff, calls Gemini, and surfaces review
  - Gemini API key stored in GitHub Secrets; never in source or logs
  - Security issues (e.g., SQL injection, hardcoded secrets) are detected and remediated; re-review confirms compliance

- **AI Test Generation**
  - AST-based parser identifies functions; Gemini generates tests; tests are committed to the PR with [skip ci] to avoid loops
  - Coverage gate (e.g., 80%) triggers test generation only when coverage would drop
  - Generated tests run in the same CI pipeline and are first-class in the repo

- **Traceability**
  - Implementation and validation reference only execution files; no untraceable claims

Validation against these criteria is documented in `validation.md`.

---

## Stakeholders and Value

### Development Teams
- Get fast, consistent test feedback on every push
- Receive automated, structured PR review for security and quality
- Gain coverage recovery via AI-generated tests when thresholds would be violated

### Security and Quality Assurance
- Every PR analyzed by AI for security patterns and code quality
- Review results tied to diffs and remediation steps

### Operations
- CI behavior and artifact production are repeatable and documented
- Secrets handled via GitHub Secrets; no credentials in repo

---

## Functional Requirements

The system must support:

- GitHub Actions workflows for test execution, artifact upload/download, PR-triggered review, and PR-triggered test generation
- Python application and test code with pytest
- Gemini API integration for code review and test generation
- Secure storage and injection of the Gemini API key (GitHub Secrets)
- AST-based parsing of Python source for function extraction used in test generation
- Coverage measurement (e.g., pytest-cov) and a coverage gate that conditionally triggers AI test generation
- Commit of generated tests back into the PR with loop-prevention (e.g., [skip ci])

---

## Non-Functional Requirements

- **Security:** API key in GitHub Secrets only; no hardcoded secrets in code or logs
- **Reliability:** Workflows idempotent where possible; review and test generation failures do not hide pipeline status
- **Traceability:** All claims traceable to execution records
- **Cost-awareness:** Test generation gated by coverage to limit unnecessary AI usage

---

## Constraints

**Technical Constraints**
- GitHub and GitHub Actions as the automation platform
- Python, pytest, and Gemini API as core tooling
- Local or CI execution of scripts (review script, AST parser, test generator, coverage script)

**Organizational Constraints**
- Engineering system scope limited to what is implemented and documented in the execution files
- No steps or validation checks that are not present in or traceable to executions

**Operational Constraints**
- Workflow design must avoid infinite loops when bots commit back to the PR (e.g., [skip ci])

---

## Non-Goals

The following are explicitly out of scope:

- Replacement of human review (AI augments, does not replace)
- Production deployment or release automation beyond build artifacts
- Other AI providers or review tools (scope is Gemini-based as executed)
- Claims or validation not backed by execution evidence

---

## Navigation

| Previous | Next |
|----------|------|
| [README](./README.md) | [Architecture](./architecture.md) |
