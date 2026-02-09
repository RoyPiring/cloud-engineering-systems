<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Review GitHub Pull Requests with Gemini

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-cicd-codereview)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-codereview_j8k3p6v1)

---

## Introducing Today's Project!

This project implements an automated pull request code review system using GitHub Actions, Python, and the Gemini API. The goal is to introduce AI as a first-class reviewer in the CI process, capable of identifying security risks, logic errors, and code quality issues before human review or merge.

This matters because modern engineering teams rely on automation to scale safely. Automated reviews reduce reviewer fatigue, catch repeatable classes of mistakes, and enforce consistent standards across all pull requests. By integrating Gemini directly into the pull request workflow, every code change is analyzed at the moment it matters most.

### Key tools and concepts

The solution is built using GitHub Actions for automation, Python for orchestration, and the Gemini API for AI analysis. The core concepts include AI-driven code review, secure secret management, CI-triggered workflows, and structured analysis of code diffs.

Together, these components form a production-style review pipeline similar to those used by large engineering organizations to augment human reviewers rather than replace them.

### Challenges and wins

The most challenging part of the project was integrating the Gemini API reliably within a GitHub Actions workflow. This required careful prompt construction, consistent diff formatting, and defensive error handling to ensure that failed API calls did not break the entire pipeline.

The major win was achieving consistent, actionable feedback from the AI reviewer. The system reliably flagged security issues, explained why they mattered, and provided clear guidance on remediation. Seeing the AI review evolve from blocking unsafe code to approving corrected changes validated the effectiveness of the pipeline.

### Why I did this project

This project was designed to build practical experience with AI-assisted development workflows. Automated code review is becoming a baseline expectation in mature engineering teams, especially for security-sensitive code paths.

By completing this project, the system demonstrates how AI can be safely embedded into CI pipelines to improve quality, reduce risk, and accelerate feedback without introducing operational fragility.

---

## Getting the Gemini API Key

The Gemini API key is required to authenticate requests to the AI model. The key is generated through Google AI Studio and provides controlled access to Gemini’s analysis capabilities.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-codereview_t5v8w1x4)

### Securing the API key

Securing the API key is critical. It is never hardcoded into the repository. Instead, it is stored using GitHub Secrets, ensuring the key is encrypted at rest and only exposed to the workflow at runtime. This mirrors real-world security practices used for production credentials.

### Installing the dependency

The google-genai Python package is installed to enable communication with the Gemini API. This library abstracts request handling, response parsing, and authentication, allowing the review logic to focus on analysis rather than protocol details.

Including this dependency ensures the script can run both locally and inside GitHub Actions without environment drift.

---

## Building the AI Review Script

The review script processes code diffs and submits them to Gemini for analysis. A diff represents the exact changes introduced by a pull request, allowing the AI to focus only on new or modified code rather than the entire codebase.

The script is executable from the command line and accepts diff files as input. It formats a structured prompt instructing Gemini to analyze the changes for security vulnerabilities, bugs, and code quality issues, then returns a clear, actionable review response.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-codereview_v5w9x2y6)

### How the review function works

The review_code function accepts a diff_text parameter containing a standard Git diff. This ensures the AI evaluates only what changed. The prompt instructs Gemini to assess security risks, logic flaws, and maintainability issues, and to explain findings in practical terms.

The returned response text is then used as the review output, which can be surfaced directly in pull request comments or logs.

### The complete script

The script includes the required Gemini client libraries, file handling logic, and argument parsing. A standard if __name__ == "__main__": entry point allows the script to be executed locally with diff files passed via the command line.

This design keeps the script reusable across local testing and CI execution.

---

## Testing the Script Locally

The script is tested locally before CI integration to ensure correct behavior. A sample Git diff is passed into the script, confirming it can read the file, send the prompt to Gemini, and return analysis output without errors.

Local testing reduces CI iteration time and ensures predictable behavior once automated.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-codereview_p3q6r9s2)

### Identifying the security vulnerability

The test diff includes a SQL injection vulnerability, allowing attackers to manipulate database queries through unsanitized input. This class of vulnerability can lead to data breaches, unauthorized access, or full database compromise.

### Gemini's review results

Gemini successfully identified security risks such as SQL injection patterns and hardcoded credentials, along with code quality issues. The feedback included explanations and remediation guidance, indicating the code was not production-ready.

This validated that the AI reviewer can surface meaningful issues early in the development process.

---

## Configuring the GitHub Actions Workflow

The workflow is configured to run on pull request events. It retrieves the diff, injects the Gemini API key from GitHub Secrets, executes the review script, and posts results as part of the CI process.

This ensures every PR receives automated scrutiny without manual intervention.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-codereview_q2r8s5y7)

### Storing the API key as a GitHub Secret

GitHub Secrets provide encrypted storage for sensitive values. The Gemini API key is injected only at runtime, preventing exposure in source control or logs.

This aligns with standard security practices for CI pipelines.

### How the workflow triggers

The workflow automatically triggers on pull request creation and updates. This ensures every code change is reviewed consistently, enforcing quality and security standards before merge.

---

## Running the AI Code Review on a Pull Request

A pull request with intentionally flawed code is used to validate the pipeline. Gemini flags the issues, the code is corrected, and the workflow is re-run.

The updated review confirms the fixes, demonstrating a complete feedback loop from detection to resolution.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-codereview_j8k3p6v1)

### Security issues detected

The AI reviewer analyzes the diff for SQL injection risks, XSS vulnerabilities, weak input validation, hardcoded secrets, and outdated libraries. These issues represent common and high-impact security failures in real-world systems.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-codereview_s1b6f3q8)

### Security issues detected

The AI reviewer analyzes the diff for SQL injection risks, XSS vulnerabilities, weak input validation, hardcoded secrets, and outdated libraries. These issues represent common and high-impact security failures in real-world systems.

### Fixing and re-reviewing the code

The identified issues are resolved by sanitizing inputs, removing hardcoded secrets, and applying best practices. A subsequent AI review confirms the code is compliant and secure.

This final step validates the effectiveness of AI-assisted review as part of a modern CI workflow.

---

## Auto-Labeling PRs by Severity

### Modifying the AI review script

### How labels help triage PRs

---

---
