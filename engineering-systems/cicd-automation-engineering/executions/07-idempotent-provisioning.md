<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Create S3 Buckets with Terraform

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-terraform1)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Canonical  
**Audience:** Builder | Designer | Learner  
**Production Use:** Yes  
**System Dependency:** Required

**Prerequisites:**
- Terraform installed and configured
- AWS account with appropriate permissions
- Understanding of Infrastructure as Code principles
- Knowledge of Terraform syntax and concepts
- Understanding of state management
- Basic familiarity with idempotent operations

**Outputs:**
- Terraform configuration files
- Infrastructure state files
- Idempotent provisioning validation results
- Infrastructure deployment evidence
- Terraform pattern examples

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-terraform1_9i0j1k2l)

---

## Introducing Today's Project!

This project defines an Amazon S3 bucket using Terraform to demonstrate infrastructure provisioning through declarative configuration rather than manual console actions. The system establishes a repeatable method for creating and managing S3 resources with consistent configuration.

The scope includes installing Terraform, configuring AWS credentials for provider authentication, defining S3 resources in Terraform configuration files, and applying those definitions to AWS. The intent is to show how object storage can be lifecycle-managed and version-controlled through code.

### Tools and concepts

The project uses Terraform as the control plane and Amazon S3 as the managed service. It focuses on Infrastructure as Code concepts, Terraform configuration structure, and basic S3 bucket management without assuming production ownership or scale.

### Project reflection

The implementation was completed within a short execution window and focused on validating the Terraform workflow rather than optimizing for scale or multi-environment deployment. Challenges primarily involved local AWS CLI configuration and understanding Terraform state behavior.

The outcome demonstrates that S3 resources can be created and updated deterministically through Terraform, reducing manual configuration drift. The project validates basic state handling and resource reconciliation rather than advanced backend or team workflows.

---

## Introducing Terraform

Terraform is used as an Infrastructure as Code tool to define cloud resources declaratively. It enables infrastructure changes to be planned, reviewed, and applied in a controlled manner rather than executed imperatively.

The tool manages infrastructure state externally and reconciles declared configuration with actual cloud resources. This supports repeatability, version control, and predictable changes across environments.

Terraform configuration files describe desired infrastructure state, including resources and attributes. In this project, the primary configuration file defines the S3 bucket and associated settings that Terraform enforces.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-terraform1_9i0j1k2l)

---

## Configuration files

Terraform configuration files declare resources, attributes, and relationships in a provider-agnostic syntax. The main configuration file serves as the authoritative definition for the S3 bucket and related properties.

The configuration enables infrastructure changes to be tracked as code, reducing manual errors and enabling consistent recreation of resources. It is designed for repeatability rather than ad hoc execution.

### My main.tf configuration has three blocks

The main configuration file contains multiple logical blocks that together define provider behavior and resource state. These blocks collectively describe what infrastructure exists and how Terraform manages it.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-terraform1_ljvh9876)

---

## Customizing my S3 Bucket

The S3 bucket configuration includes additional settings beyond basic creation, such as tagging and optional lifecycle-related attributes. These configurations support organization, cost attribution, and future policy extension.

Tags are applied at the resource level to support identification and cost allocation. Validation is performed by inspecting bucket properties through the AWS Console or AWS CLI to confirm that metadata is correctly applied.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-terraform1_ffe757cd3)

---

## Terraform commands

The Terraform workflow begins with initializing the working directory to download required providers and prepare local state handling. This step ensures Terraform can interact with AWS using the defined provider configuration.

A planning step is used to calculate proposed changes before execution. This allows inspection of resource creation or modification without applying changes to the AWS account.

These commands establish a controlled workflow that separates initialization, review, and execution. They are foundational to predictable infrastructure management rather than deployment automation.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-terraform1_3g4h5i6j)

---

## AWS CLI and Access Keys

AWS provider configuration requires an explicit region and valid credentials. Missing region configuration results in provider initialization errors during Terraform execution.

The AWS CLI is used to configure credentials locally and to perform basic validation outside of Terraform. It serves as a supporting tool rather than the primary provisioning mechanism.

This setup assumes a single-user local environment and does not implement credential rotation, role assumption, or centralized identity controls.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-terraform1_7j8k9l0m)

---

## Lanching the S3 Bucket

Applying the Terraform configuration creates or updates the S3 bucket according to the declared state. Terraform reconciles the desired configuration with existing resources in the AWS account.

The execution sequence follows initialization, planning, and application to reduce risk and surface errors early. This ordering enforces deliberate change management even for simple resource creation.

The workflow demonstrates controlled infrastructure changes but does not include safeguards such as remote state locking or approval gates.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-terraform1_1q2w3e4r)

---

## Uploading an S3 Object

Additional Terraform resource definitions extend the S3 bucket configuration to include features such as versioning, encryption, or lifecycle behavior when explicitly defined. These settings improve durability and management characteristics.

Applying configuration changes updates the existing bucket without recreating it when possible. Terraform determines the minimum required changes based on state comparison.

Validation consists of confirming bucket properties through AWS-native tools. The project verifies configuration presence rather than performance, security posture, or production readiness.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-terraform1_9o0p1a2s)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Package Management CodeArtifact](./06-package-management-codeartifact.md) | [Guardrail Enforcement](./08-guardrail-enforcement.md) |
