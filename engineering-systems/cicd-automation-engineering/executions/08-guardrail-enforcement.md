<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a CI/CD Pipeline with AWS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codepipeline-updated)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Canonical  
**Audience:** Builder | Designer | Learner  
**Production Use:** Yes  
**System Dependency:** Required

**Prerequisites:**
- AWS account with CodePipeline access
- Source, build, and deployment stages configured
- Understanding of pipeline orchestration
- Knowledge of approval gates and policy enforcement
- Understanding of security scanning integration
- Basic familiarity with pipeline stages and actions

**Outputs:**
- CodePipeline pipeline configuration
- Policy gate configurations
- Security scanning integration
- Pipeline execution validation results
- Guardrail enforcement test evidence

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codepipeline-updated_fbdetger)

---

## Introducing Today's Project!

This project implements an end-to-end CI/CD pipeline that automates application build and deployment using AWS managed services. The system exists to standardize promotion from source control to runtime, reduce manual intervention, and provide deterministic rollback when failures occur.

The implementation composes previously established components into a single pipeline that orchestrates source ingestion, build execution, and deployment. The outcome is a continuously executable release mechanism with traceability across stages and versions.

### Key tools and concepts

The pipeline uses Amazon S3 and Amazon EC2 for artifacts and runtime, AWS IAM for scoped access, GitHub for source control, CodePipeline for orchestration, CodeBuild for build execution, CodeDeploy for deployment, and CloudFormation for infrastructure definition.

These services collectively enforce separation of concerns between orchestration, execution, and deployment while enabling automated, repeatable releases.

### Project reflection

The primary challenge was integrating multiple AWS services with consistent permissions and event flow. Resolving these integrations validated service boundaries and reduced failure modes caused by misaligned roles or triggers.

Successful execution demonstrated that the pipeline can deploy changes reliably and recover from errors through rollback.

---

## Starting a CI/CD Pipeline

AWS CodePipeline acts as the orchestration layer that models, visualizes, and executes the release workflow. It coordinates actions across services while maintaining execution state and history.

The pipeline was configured to execute automatically on changes rather than manual release gates.

A managed service role was created to centralize permissions required for pipeline execution, reducing configuration errors and simplifying access management.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codepipeline-updated_gdnhtm)

---

## CI/CD Stages

The pipeline is composed of Source, Build, and Deploy stages. Each stage encapsulates a discrete responsibility and exposes status and logs for inspection.

The Source stage monitors GitHub for changes and emits versioned artifacts. The Build stage uses CodeBuild to compile, test, and package code in an isolated environment. The Deploy stage uses CodeDeploy to apply validated artifacts to EC2 targets using defined deployment strategies.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codepipeline-updated_fbdetger)

---

## Source Stage

The source configuration specifies the default branch to monitor, establishing the canonical trigger for pipeline execution. Without an explicit branch, downstream stages would lack a stable input.

Webhook integration enables event-driven execution on commits and pull requests. This removes manual triggers and ensures changes are validated and deployed consistently.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codepipeline-updated_sergt)

---

## Build Stage

The build stage executes in CodeBuild using an AWS-managed container image and a build specification file. Input is the versioned source artifact produced by the Source stage.

This stage is responsible for compiling code, running tests, and producing deployable artifacts that are immutable and traceable to a specific commit.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codepipeline-updated_j1k2l3m4)

---

## Deploy Stage

The deployment stage uses CodeDeploy to roll out artifacts to EC2 instances. Deployment configuration defines how updates are applied and how failures are detected.

This stage focuses on controlled application of changes rather than build concerns, minimizing downtime and isolating deployment-specific failure modes.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codepipeline-updated_m4n5o6p7)

---

## Success!

Pipeline behavior was validated by introducing incremental code changes and observing automated execution across all stages.

Commit metadata propagated through the pipeline, providing traceability from source to deployment.

Successful deployment was confirmed by verifying application changes on the running service, ensuring that pipeline outputs matched expected runtime behavior.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codepipeline-updated_e1f2g3h4)

---

## Testing the Pipeline

Rollback behavior was tested by initiating a deployment failure and observing automatic reversion to a known-good version.

During rollback, source and build stages are bypassed because they are not relevant to deployment recovery.

Verification confirmed that the application returned to a stable state after rollback. This behavior demonstrates the pipeline’s ability to limit blast radius and preserve service availability during failures.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codepipeline-updated_sdfgsdfgdf)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Idempotent Provisioning](./07-idempotent-provisioning.md) | [Rollback Procedure](./09-rollback-procedure.md) |
