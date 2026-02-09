<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Increase Test Coverage with AI

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-cicd-testgen)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-testgen_v6n8d4w1)

---

## Introducing Today's Project!

This project implements an AI-assisted CI/CD workflow that automatically generates Python unit tests using GitHub Actions and the Gemini API. The objective is to increase test coverage without relying on manual test writing, while still enforcing quality and efficiency controls.

This matters because test coverage directly impacts software reliability. By automating test generation inside CI, the project reduces human effort, shortens feedback loops, and ensures that new code paths are validated before they reach production.

### Key tools and concepts

This project uses Python as the primary language, GitHub Actions for automation, Gemini API for AI-driven test generation, pytest for test execution, and the AST module for static code analysis.

The core concepts include CI/CD pipelines, automated test generation, workflow orchestration with GitHub Actions, coverage-based quality gates, and Abstract Syntax Tree analysis to safely understand source code structure.

### Challenges and wins

The project took approximately 75 minutes to complete. The most challenging part was implementing a coverage gate that conditionally triggers AI test generation only when coverage would drop below an acceptable threshold.

The key win was achieving a pipeline that intelligently balances cost and quality. Tests are generated only when needed, preventing unnecessary AI usage while still protecting code quality.

### Why I did this project

This project was built to gain hands-on experience with AI-augmented testing workflows inside CI/CD pipelines. Automated test generation is becoming increasingly relevant as codebases scale and manual testing becomes a bottleneck.

The work demonstrates how AI can be applied surgically and responsibly in engineering workflows rather than indiscriminately.

---

## Building the Code Parser with AST

In this step, a Python script is created to analyze source code using the Abstract Syntax Tree module. The script parses Python files and identifies function definitions that require test coverage.

This step is critical because it allows the system to understand code structure without executing it, ensuring safe and deterministic extraction of function metadata.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-testgen_j4w9c6m2)

### How the AST module parses Python code

The AST module converts Python source code into a tree representation. Each function is represented as a node containing its name, parameters, and body.

By traversing this tree, the script extracts only the relevant function signatures, avoiding noise and enabling precise AI prompts for test generation.

---

## Completing the Test Generation Script

The test generation script operates in three phases. First, it parses the code using AST to identify functions. Next, it sends structured function signatures to the Gemini API. Finally, it writes the generated tests into a designated test file.

This approach ensures that AI output is deterministic, scoped, and directly usable within the existing test suite.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-testgen_h2k6y9d4)

---

## Creating the GitHub Actions Workflow

A GitHub Actions workflow is created to automate test generation during pull requests. The workflow triggers on PR events, runs the AST analysis, invokes Gemini for test generation, and commits the generated tests back to the pull request.

This automation ensures that new code is always evaluated for coverage impact before merge.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-testgen_w9p5d3k6)

### Preventing infinite workflow loops

Because the workflow commits code back into the pull request, safeguards are required to prevent infinite execution loops. The workflow uses a [skip ci] commit message to prevent retriggering itself.

This design mirrors production-grade automation patterns where bots modify code safely without destabilizing CI systems.

---

## Verifying the Test Generation Bot

The workflow is validated by opening a pull request and observing the automated test generation process. The pipeline executes, generates tests, commits them, and updates the pull request.

This confirms that the full automation chain operates correctly end-to-end.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-testgen_v6n8d4w1)

### Confirming the bot works

The generated commit includes a new test file containing unit tests created by Gemini. These tests are integrated directly into the repository and executed as part of the standard CI run.

This verifies that AI-generated tests are not isolated artifacts but first-class citizens in the codebase.

---

## Adding Coverage-Gated Test Generation

A coverage gate is added to measure code coverage using pytest-cov. The workflow evaluates whether new changes would reduce overall coverage below 80%.

Test generation only runs when the coverage threshold would be violated, conserving resources while enforcing quality standards.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-testgen_c9m3p7t1)

### How the coverage script decides

The coverage script executes tests with coverage enabled and evaluates the resulting percentage. If coverage remains at or above 80%, the script exits successfully and skips test generation.

If coverage drops below the threshold, the script fails intentionally, triggering the AI test generation step.

---

## Testing the Coverage Gate

The coverage gate is validated by introducing new code paths without tests. The workflow detects the coverage drop and automatically generates tests to restore coverage above the threshold.

This confirms that the pipeline dynamically responds to risk rather than applying static rules.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-testgen_j5q9s3u7)

---

---
