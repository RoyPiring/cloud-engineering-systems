<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# GitHub to Azure DevOps Pipeline

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-azure-deployment-pipeline)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

---

## Introducing Today's Project!

This project focuses on building a full CI/CD pipeline using Azure DevOps, with clearly separated staging and production environments and support for safe, repeatable deployments. The objective is to automate the path from source code in GitHub to running workloads in Azure, while reducing deployment risk and manual effort.

This work matters because reliable delivery pipelines are a prerequisite for operating production systems. A well-designed pipeline enforces consistency, catches errors early, and gives teams confidence that changes can be deployed frequently without destabilizing the platform.

### Key tools and concepts

The project uses Azure DevOps for pipeline orchestration, GitHub for source control, and Azure Functions as the deployment target. The core concepts include CI/CD pipelines, YAML-based pipeline definitions, self-hosted agents, environment separation, service connections, and deployment gating.

Together, these concepts form a delivery system that is predictable, auditable, and aligned with modern DevOps practices used in production environments.

### Challenges and wins

The primary challenge was rebuilding and integrating prior projects into a single automated pipeline, then configuring a self-hosted agent and service connections correctly. These steps are often underestimated but are critical to enabling secure and reliable automation across environments.

The key win was seeing the entire pipeline execute end to end, deploying first to staging and then to production without manual intervention. This confirmed that the pipeline design was sound and that deployments could be trusted to run consistently.

---

## Configuring the Self-Hosted Agent

The agent runs on a local machine or private compute environment and registers itself with Azure DevOps. When a pipeline is triggered, Azure DevOps assigns jobs to the agent, which executes them locally and reports results back to the service.

This model allows pipelines to interact securely with Azure subscriptions, deploy resources, and run tests in environments that closely resemble production.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-deployment-pipeline_h5j9w4m1)

### How self-hosted agents work

The agent runs on a local machine or private compute environment and registers itself with Azure DevOps. When a pipeline is triggered, Azure DevOps assigns jobs to the agent, which executes them locally and reports results back to the service.

This model allows pipelines to interact securely with Azure subscriptions, deploy resources, and run tests in environments that closely resemble production.

---

## Creating Staging and Production Environments

Two separate Azure Function Apps are created to represent staging and production. Staging is used to validate changes before release, while production serves live traffic.

Each environment has its own configuration and environment variables, ensuring that testing can occur without impacting users. This separation is a core reliability practice in production systems.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-deployment-pipeline_b6k1y9f4)

---

## Building the Multi-Stage Pipeline

A multi-stage pipeline is defined using YAML to describe the full automation flow. The pipeline includes build, test, staging deployment, and production deployment stages, each with explicit dependencies and execution order.

The YAML file serves as a version-controlled blueprint for the delivery process. This ensures the pipeline itself evolves alongside the application code and can be reviewed, tested, and audited like any other artifact.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-deployment-pipeline_w8k4n1v6)

### Understanding the four pipeline stages

The build stage compiles the code and prepares deployable artifacts. The staging deployment stage releases the application to a non-production environment for validation. Integration testing verifies that the application behaves correctly once deployed. The production deployment stage releases validated changes to users.

This staged approach reduces risk by ensuring that only tested and verified artifacts reach production.

### Configuring service connections and environments

Service connections provide the pipeline with controlled access to external systems such as Azure subscriptions and GitHub repositories. Environments group deployments logically and allow additional controls, such as approvals or checks, to be applied.

Together, they enforce security boundaries and operational discipline across the software delivery lifecycle.

---

## Running the CI/CD Pipeline

The pipeline is triggered through code commits or manual execution. Each run executes the defined stages in order, providing real-time feedback on build status, test results, and deployment progress.

This automation replaces manual deployment steps with a repeatable and observable process, reducing human error and speeding up delivery.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-deployment-pipeline_x9k3m7p1)

### Watching the pipeline progress

During execution, the pipeline advances through build, staging deployment, testing, and production deployment. Logs and status indicators make it easy to identify failures early and understand exactly where and why a run failed.

This visibility is essential for diagnosing issues and maintaining confidence in the delivery process.

---

## Verifying Production Deployment

Production deployment is verified by accessing the application endpoint and confirming expected behavior. Health checks returning successful responses indicate that the application is running correctly.

Automated pipelines save time by handling repetitive tasks consistently, allowing engineers to focus on improving the system rather than managing deployments.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-deployment-pipeline_q6y1f9d3)

---

## Adding Code Quality Gates

A code quality stage is added to the pipeline to enforce baseline standards before builds occur. Tools like Flake8 and Black ensure that code meets syntax and formatting requirements before it is allowed to progress.

By intentionally breaking rules during testing, the quality gate demonstrates that the pipeline correctly blocks unsafe changes.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-deployment-pipeline_n7p3k8v2)

### How code quality gates improve the pipeline

Quality gates prevent defective or poorly formatted code from reaching later stages. This shifts error detection earlier in the lifecycle, where fixes are faster and less costly.

Over time, these gates improve overall code quality and reduce production incidents caused by preventable mistakes.

---

## Project Wrap-Up

This project demonstrates how to design and operate a CI/CD pipeline that supports safe, automated delivery across environments. It reinforces the importance of environment separation, automation, and guardrails in modern software development.

The next area of growth is extending these patterns to containerized workloads and Kubernetes-based platforms, where similar principles apply at larger scale.

### Final reflection

---

---
