<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Your First GitHub Actions AI workflow

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-cicd-github)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-github_d2f6s4y1)

---

## Introducing Today's Project!

This project focuses on building a CI pipeline using GitHub Actions to automate Python testing with pytest. The goal is to establish a reliable feedback loop where code changes are automatically validated before they are merged or released.

This matters because CI is the foundation of modern software delivery. Automating tests reduces human error, shortens feedback cycles, and ensures that broken code is caught early, long before it reaches production systems.

### Key tools and concepts

This project uses GitHub Actions for automation, Python for application logic, and pytest for testing. Together, they form a minimal but production-relevant CI setup.

The key concepts include CI/CD workflows, automated testing, and build artifact management, all of which are foundational to modern software delivery.

### Challenges and wins

The project took approximately one hour to complete. The most challenging part was understanding the GitHub Actions workflow structure and environment setup, which required some trial and error.

Once the workflow model was clear, the remaining steps flowed naturally and reinforced how automation simplifies development.

### Why I did this project

This project was completed to learn how to build and operate a CI pipeline using GitHub Actions for automated Python testing. It establishes a strong baseline for more advanced workflows.

A logical next step is integrating AI-powered code review, security scanning, or deployment automation to extend CI into a full CI/CD system.

---

## Setting Up the Python Environment

This step establishes a clean and isolated Python development environment. By forking and cloning the repository, creating a virtual environment, and installing dependencies, the project ensures that development and testing occur in a controlled context.

This isolation is important because it prevents dependency conflicts and guarantees that tests run consistently across different machines and environments, including CI runners.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-github_m5v9b3x7)

### Activating the virtual environment

The virtual environment is activated so the project uses its own Python interpreter and dependency set. The visible environment indicator confirms that commands are executed within this isolated context.

This mirrors production and CI behavior, where environments are intentionally separated to ensure reproducibility and reliability.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-github_p2w8n4r6)

### Exploring the project structure

The project is organized to clearly separate application logic, tests, and automation configuration. Core application code lives in the main module, tests are placed under a dedicated directory, and GitHub Actions workflows are stored in the .github directory.

This structure improves readability, maintainability, and automation readiness, reflecting conventions used in professional Python projects.

---

## Writing and Testing a Python Function

This step introduces basic application logic alongside automated tests. Writing tests at the same time as code ensures behavior is explicitly defined and verifiable.

Tests act as a safety net. They catch regressions early, document expected behavior, and provide confidence that changes do not unintentionally break existing functionality.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-github_q8j4m1h6)

### Creating the multiply function

The multiply function extends the application logic and reinforces the value of type hints. Type annotations clarify how functions should be used and improve maintainability as the codebase grows.

This practice reduces ambiguity and helps prevent subtle bugs during future changes.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-github_a6s2v5t8)

### Running and verifying tests

Tests are executed locally using pytest to confirm that all functionality behaves as expected. Passing results indicate the code, dependencies, and test environment are aligned.

Running tests locally before pushing changes reduces CI noise and speeds up iteration.

---

## Building a CI Pipeline with GitHub Actions

This step introduces automation using GitHub Actions. The pipeline is configured to run tests automatically on every push, ensuring immediate feedback on code changes.

CI improves reliability by enforcing a consistent validation process that does not depend on individual developer habits.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-github_g1k5n9r3)

### Configuring the workflow

The workflow checks out the repository, sets up Python, installs dependencies, and runs pytest. These steps mirror the local development workflow in a clean, automated environment.

This ensures that validation is consistent and repeatable for every change.

### Testing the pipeline

An intentional test failure is introduced to confirm that the pipeline detects errors correctly. The failed run demonstrates that the CI system is actively enforcing quality gates.

Fixing the test and observing the pipeline pass validates the fast feedback loop that CI provides.

---

## Packaging Code with CI Artifacts

This step extends the pipeline to generate build artifacts. Packaging the application allows tested outputs to be stored and reused without rebuilding.

Artifacts are critical in real pipelines because they decouple build and deployment stages and preserve exactly what was tested.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-github_n3m7k1w9)

### Adding build and upload steps

The pipeline packages the application into a distributable artifact and uploads it to GitHub Actions. This makes the build output available for download and downstream use.

This pattern improves traceability and repeatability across environments.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-cicd-github_s6p9c4v1)

### Downloading the packaged artifact

The packaged artifact is downloaded from the workflow run, confirming that the pipeline successfully produces and stores build outputs.

This completes the CI loop by proving that validated code can be packaged and distributed automatically.

---

---
