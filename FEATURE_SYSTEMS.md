# Feature Systems

This document indexes the **curated Feature Systems** in this repository and routes directly to their **authoritative implementations and validation evidence**.

Feature Systems surface **high-signal, end-to-end engineering systems** that demonstrate architectural judgment, execution depth, and verified outcomes. Each Feature System maps **1:1 to an Engineering System**, which remains the source of truth.

---

## Featured Systems (Built / Validated / Evidence)

### 1. [Secure VPC Networking Baseline](./feature-systems/fs-secure-vpc-networking-baseline/README.md)

**Built:** Secure, isolated network infrastructure using VPC design, subnet segmentation, routing boundaries, and security controls.  
**Evidence:**  
[Validation](./engineering-systems/vpc-networking-engineering/validation.md) ·
[Implementation](./engineering-systems/vpc-networking-engineering/implementation.md) ·
[Execution Path](./engineering-systems/vpc-networking-engineering/implementation.md#execution-path-start-to-finish)

---

### 2. [Security & Compliance Guardrails](./feature-systems/fs-security-compliance-guardrails/README.md)

**Built:** IAM least-privilege enforcement, secrets management, encryption boundaries, monitoring, and threat detection controls.  
**Evidence:**  
[Validation](./engineering-systems/security-and-compliance-engineering/validation.md) ·
[Implementation](./engineering-systems/security-and-compliance-engineering/implementation.md) ·
[Execution Path](./engineering-systems/security-and-compliance-engineering/implementation.md#execution-path-start-to-finish)

---

### 3. [IaC CI/CD Policy Gates](./feature-systems/fs-iac-cicd-policy-gates/README.md)

**Built:** Infrastructure-as-code delivery pipelines with policy enforcement, automated validation, and rollback mechanisms.  
**Evidence:**  
[Validation](./engineering-systems/cicd-automation-engineering/validation.md) ·
[Implementation](./engineering-systems/cicd-automation-engineering/implementation.md) ·
[Execution Path](./engineering-systems/cicd-automation-engineering/implementation.md#execution-path-start-to-finish)

---

## Additional Engineering Systems

This repository also contains **complete, validated Engineering Systems** beyond the curated Feature Systems above.  
These systems expand domain coverage and can be reviewed independently with full documentation and validation.

See the **[Engineering Systems README](./engineering-systems/README.md)** for the complete system index, scope, and evidence.
