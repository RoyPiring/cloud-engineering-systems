# Architecture: AI CICD E2E GitHub Actions Gemini

## Quick Orientation

**Scope:** End-to-end AI-augmented CI/CD using GitHub Actions and the Gemini API: automated Python testing, PR code review, and coverage-gated AI test generation, with all design traceable to execution records.

**Non-Goals:**
- Replacing human review
- Production deployment or release automation beyond artifacts
- AI providers or tools other than those used in the executions

**Key Tradeoffs:**
- **AI review vs. human:** Gemini augments review; humans remain responsible for final approval
- **Test generation vs. cost:** Coverage gate triggers AI test generation only when coverage would drop (e.g., below 80%)
- **Bot commits vs. loops:** Workflow commits generated tests with [skip ci] to prevent infinite workflow runs

**Diagram:** See [Architecture Patterns](#architecture-patterns) below.

---

## System Design

The system covers four execution areas: (1) baseline CI with pytest and artifacts, (2) PR-triggered AI code review with Gemini, (3) PR-triggered AI test generation with coverage gate, and (4) stale-code-related automation as documented in the fourth execution file.

## Core Components

### 1. Source and Runtime
- GitHub repository (fork/clone, branch, push, pull requests)
- Python virtual environment for isolation and reproducibility
- Python application and test code; pytest for execution

### 2. CI Automation
- GitHub Actions workflows (push and pull_request triggers)
- Checkout, Python setup, dependency install, pytest run
- Build artifact creation and upload/download via Actions artifacts

### 3. AI Code Review
- Review script (Python) that accepts a diff, formats a prompt, and calls the Gemini API
- google-genai (or equivalent) for Gemini API access
- GitHub Secrets for Gemini API key; key injected only at workflow runtime
- Workflow runs on PR events; retrieves diff, runs script, surfaces review (e.g., in logs or comments)

### 4. AI Test Generation
- AST-based parser to extract function metadata from Python source
- Test generation script: parse → prompt Gemini with function context → write generated tests to a test file
- Workflow runs on PR; runs coverage; if coverage would drop below threshold, runs test generation and commits tests with [skip ci]
- pytest-cov (or equivalent) for coverage measurement and gate logic

### 5. Security and Secrets
- GitHub Secrets for API key storage and injection
- No API key in source control or logs

## Architecture Patterns

### Pattern 1: Baseline CI (Push)
```
Push → GitHub Actions → Checkout → Set up Python → Install deps → pytest → Build artifact → Upload artifact
```

### Pattern 2: AI Code Review (Pull Request)
```
PR open/update → Workflow → Get diff → Inject API key from Secrets → Run review script → Gemini API → Review output (e.g., comment/log)
```

### Pattern 3: AI Test Generation (Pull Request)
```
PR → Workflow → Run tests with coverage → Coverage above threshold? → Skip generation
                                      → Coverage below threshold? → AST parse → Gemini generate tests → Write test file → Commit with [skip ci]
```

### Pattern 4: Stale Code Handling
- Refer to `./executions/04-ai-cicd-stalecode.md` for scope and behavior as implemented.

## Design Decisions

- **Automation platform:** GitHub Actions for triggers, environment, and artifact storage (per executions)
- **Language and tests:** Python and pytest for application and test execution
- **AI provider:** Gemini API for review and test generation (per executions)
- **Secrets:** GitHub Secrets only; no credentials in repo
- **Coverage gate:** Threshold (e.g., 80%) so test generation runs only when coverage would drop
- **Loop prevention:** [skip ci] (or equivalent) on bot commits to avoid re-triggering workflows

---

## Failure Model

**What fails:** Workflow failures, pytest failures, Gemini API errors, coverage script failures, review script errors

**How it fails:** Workflow step fails; tests fail; API timeout or error; coverage below threshold triggers generation or fails gate; script crashes on bad input

**Blast radius:** Failed step blocks subsequent steps in that job; failed tests block merge if required; API failure can leave PR without AI review until retry or fix

**Recovery:** Fix tests or code and re-push/re-run; fix workflow or script and re-run; retry workflow for transient API failures; review script should handle errors defensively so one failure does not hide others

## Security Model

**Trust boundaries:** Repository (trusted code); GitHub Secrets (encrypted at rest, exposed only to workflow at runtime); Gemini API (external service)

**Access control:** Repository and workflow permissions; API key only in Secrets; no key in logs or artifacts

**Secrets:** Gemini API key stored in GitHub Secrets; injected as environment variable or input to the workflow

**Audit:** Git history; GitHub Actions run logs (with secrets redacted); execution and validation docs

## Cost Model

**Primary drivers:** GitHub Actions minutes; Gemini API usage (review per PR, test generation when coverage gate fires)

**Guardrails:** Coverage gate limits test generation to when coverage would drop; no unbounded AI calls

## Constraints

**Policy:** No credentials in repo; automation limited to what is in execution records

**Technical:** GitHub Actions, Python, pytest, Gemini API, AST, pytest-cov as used in executions

**Traceability:** Architecture does not assert behavior not present in execution files

## Quality Goals (Detailed)

1. **Baseline CI** - How judged: Workflow runs on push; Python environment and pytest execute consistently; pipeline detects test failures and passes after fixes; build artifacts are produced and downloadable from the workflow run

2. **AI Code Review** - How judged: PR-triggered workflow retrieves diff, calls Gemini, and surfaces review; API key in GitHub Secrets only; security issues (e.g., SQL injection, hardcoded secrets) detected and remediated; re-review confirms compliance

3. **AI Test Generation** - How judged: AST-based parser identifies functions; Gemini generates tests; tests committed with [skip ci]; coverage gate (e.g., 80%) triggers generation only when coverage would drop; generated tests run in same CI pipeline

4. **Traceability** - How judged: Implementation and validation reference only execution files; no untraceable claims; evidence map in validation.md links checks to executions

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |
