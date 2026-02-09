# Security & Compliance Guardrails

Identity, secrets, encryption, and threat detection implemented as a production-oriented security baseline.  
This system prevents unauthorized access through least-privilege controls, protects sensitive data using encryption boundaries, and validates security posture through automated detection and audit evidence.

**Evidence:** [Full Validation Report](../../engineering-systems/security-and-compliance-engineering/validation.md)

---

## Engineering Judgment Highlights

Key architectural decisions and tradeoffs made during system design:

- **IAM roles over IAM users**  
  Selected to eliminate long-lived credentials and enforce temporary access, accepting role-assumption complexity for improved security posture.

- **Customer-managed KMS keys over AWS-managed keys**  
  Chosen to retain control over key policies, rotation schedules, and audit visibility, trading increased operational overhead for compliance and governance requirements.

- **Secrets Manager over Parameter Store**  
  Selected to enable automated secret rotation and tighter lifecycle management, accepting higher per-secret cost for reduced operational risk.

- **GuardDuty over third-party threat detection tools**  
  Chosen to leverage native AWS log sources and managed detection, trading advanced customization for lower maintenance complexity.

- **Defense-in-depth security controls over single-point enforcement**  
  Implemented across identity, data, and monitoring layers, accepting additional configuration complexity to reduce blast radius.

- **Explicit deny with least-privilege IAM policies**  
  Selected to minimize attack surface and improve auditability, trading policy verbosity for clearer access boundaries.

- **CloudTrail, CloudWatch, and GuardDuty over custom security tooling**  
  Chosen to achieve managed monitoring with minimal operational overhead, trading deep customization for reliability and speed of implementation.

---

## Capabilities Demonstrated

This system implements and validates the following capabilities:

- IAM least-privilege access control using scoped roles and policies
- Secure secret storage and automated rotation with AWS Secrets Manager
- Encryption of data at rest using KMS-managed keys
- Encryption of data in transit using TLS/SSL
- Automated threat detection and alerting via GuardDuty
- Centralized security logging and audit trails
- Evidence-backed compliance validation

---

## Scope and Constraints

### In Scope
- IAM least-privilege access controls
- Secrets management and rotation
- KMS-based encryption boundaries
- Managed threat detection
- Compliance validation and evidence collection

### Constraints and Non-Goals
- Single AWS account scope
- No organization-level or multi-account controls
- No advanced threat hunting or forensics
- No SIEM integration
- No custom security tooling development
- No penetration testing or red-team exercises

---

## What Was Validated

The following behaviors were explicitly verified:

1. IAM access restricted to authorized actions only  
2. Unauthorized access attempts denied with expected error behavior  
3. Data encrypted at rest using KMS or service-managed encryption  
4. Encryption in transit enforced using TLS/SSL  
5. Secrets stored securely and excluded from source code  
6. Secret rotation enabled and validated  
7. GuardDuty detects simulated threat conditions  
8. Security-relevant actions logged via CloudTrail and CloudWatch  
9. Compliance checks pass defined criteria  
10. Audit trails enable full action traceability  

Validation details and supporting evidence are documented in:  
[validation.md](../../engineering-systems/security-and-compliance-engineering/validation.md#validation-summary)

---

## Execution Path

Follow the ordered execution path for a complete system walkthrough:

1. IAM Least Privilege  
2. Secrets Management  
3. Encryption Boundary Enforcement  
4. Compliance Checklist Validation  
5. Evidence Collection  

Full execution guide:  
[Execution Path – Start to Finish](../../engineering-systems/security-and-compliance-engineering/implementation.md#execution-path-start-to-finish)

---

## Source of Truth

Authoritative documentation and implementation details live in:  
[engineering-systems/security-and-compliance-engineering/](../../engineering-systems/security-and-compliance-engineering/)

Feature Systems summarize outcomes and evidence but do not redefine system behavior.

---

## Repository Navigation

- [Root README](../../README.md) – Repository overview
- [Feature Systems Index](../../FEATURE_SYSTEMS.md) – All Feature Systems
- [Engineering Systems Index](../../engineering-systems/README.md) – All Engineering Systems
- [Operating Requirements](../../OPERATING_REQUIREMENTS.md) – Target operating expectations
- [Quality Standards](../../QUALITY_STANDARDS.md) – Quality and review criteria
