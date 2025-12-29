<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy a Web App with CodeDeploy

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codedeploy-updated)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Canonical  
**Audience:** Builder | Designer | Learner  
**Production Use:** Yes  
**System Dependency:** Required

**Prerequisites:**
- AWS account with CodeDeploy access
- EC2 instances or deployment targets configured
- Understanding of deployment strategies
- Knowledge of application deployment patterns
- Understanding of rollback procedures
- Basic familiarity with deployment groups

**Outputs:**
- CodeDeploy application and deployment group configuration
- Deployment configuration files (appspec.yml)
- Deployment validation results
- Rollback procedure test evidence
- Automated deployment documentation

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codedeploy-updated_val-27)

---

## Introducing Today's Project!

This project implements an automated application deployment workflow using AWS CodeDeploy to deliver a web application to an Amazon EC2 instance. The system exists to demonstrate how deployment can be standardized, repeatable, and decoupled from manual server access within a CI/CD pipeline.

### Key tools and concepts

The deployment uses AWS CodeDeploy to orchestrate application updates, Amazon EC2 as the runtime environment, GitHub as the source repository, and AWS IAM for controlled service permissions. Together, these components support a basic continuous deployment model where code changes are promoted through automation rather than manual intervention.

### Project reflection

The deployment surfaced configuration and permission dependencies between CodeDeploy, EC2 instance roles, and source access. Resolving these dependencies validated the end-to-end deployment path from source to running application. The result confirms a functioning deployment stage suitable for integration with upstream CI processes.

This project represents the deployment layer of a CI/CD pipeline and is intentionally scoped to single-instance delivery. It assumes prior CI artifact creation and focuses on controlled rollout rather than production-grade availability.

---

## Deployment Environment

An Amazon EC2 instance serves as the deployment target, hosted within a VPC to provide network isolation and controlled access boundaries. This environment defines where application artifacts are installed and executed.

Infrastructure is provisioned using infrastructure-as-code tooling to ensure consistency and repeatability. The same definitions support both deployment and teardown, reducing configuration drift and preventing orphaned resources.

The template provisions EC2 instances, IAM roles, and supporting integrations required by CodeDeploy. These resources establish the minimum control plane needed for automated application delivery and access control.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codedeploy-updated_val-5)

---

## Deployment Scripts

Deployment scripts define host-level actions executed during the CodeDeploy lifecycle. Their purpose is to prepare the instance, configure runtime dependencies, and manage application processes in a predictable manner.

The install_dependencies script installs required services such as Tomcat and Apache and configures Apache to proxy traffic to the application runtime. This establishes the execution environment expected by the deployed application.

The start_server.sh script starts application services, applies runtime configuration, and records execution output. It ensures the application enters a known running state after deployment.

The stop_server.sh script cleanly stops the application server and releases resources. This prepares the instance for version replacement and prevents conflicts during redeployment.

---

## appspec.yml

The appspec.yml file defines how CodeDeploy applies a revision to the target environment. It specifies file mappings, lifecycle hooks, and permission settings that govern deployment behavior.

The build configuration was updated to align artifact structure and deployment expectations. These changes ensure compatibility between build outputs and deployment inputs without altering deployment scope.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codedeploy-updated_val-12)

---

## Setting Up CodeDeploy

A CodeDeploy application acts as a logical container for deployments, while deployment groups define the target environment and deployment behavior. These constructs separate application identity from infrastructure targeting.

IAM permissions grant CodeDeploy the ability to retrieve application revisions, interact with EC2 instances, and emit logs. Assigning these permissions through a service role enforces least privilege while enabling deployment execution.

Resource tagging is used to categorize and identify CI/CD-related components. Tags support operational clarity and simplify resource discovery without affecting deployment behavior.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codedeploy-updated_val-18)

---

## Deployment configurations

Deployment configuration controls how updates are applied to targets. The CodeDeployDefault.AllAtOnce strategy updates all instances simultaneously, which simplifies testing but increases blast radius.

The CodeDeploy agent runs on the EC2 instance and executes lifecycle commands defined in the deployment specification. It serves as the execution endpoint for deployment instructions issued by the CodeDeploy service.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codedeploy-updated_val-20)

---

## Success!

A deployment represents a single rollout of an application revision within a deployment group. The deployment group defines which instances are updated and under what configuration constraints.

The revision location specifies where CodeDeploy retrieves deployment artifacts. In this implementation, revisions are sourced from an Amazon S3 bucket that stores packaged application outputs.

Successful deployment was verified by accessing the application endpoint and confirming expected behavior. This validation confirms that CodeDeploy correctly retrieved, installed, and activated the application revision.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codedeploy-updated_val-27)

---

## Disaster Recovery

A deployment failure was intentionally triggered by introducing an invalid Maven repository configuration. This caused dependency resolution to fail and prevented successful application startup.

CodeDeploy supports automatic rollback when deployments fail health checks. In this case, the system reverted to the previously deployed version, limiting service disruption.

Recovery may also require manual redeployment of a known-good revision. Manual intervention introduces operational risk if not controlled, underscoring the importance of validated artifacts and repeatable deployment processes.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-codedeploy-updated_rollback-validation-upload)

---

---

## Navigation

| Previous |
|----------|
| [Guardrail Enforcement](./08-guardrail-enforcement.md) |
