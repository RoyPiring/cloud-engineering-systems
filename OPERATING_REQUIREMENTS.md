# Operating Requirements

This document defines the **target operating baseline** used to evaluate systems in this repository.

The requirements describe **production-grade expectations** across security, reliability, cost, and repeatability. Individual systems may intentionally implement a subset based on scope, maturity, or purpose; any deviation is expected to be **explicitly documented**.

Operating Requirements define **what good looks like**. How adherence is evaluated is defined in `QUALITY_STANDARDS.md`.

---

## Security Expectations

Security expectations describe the intended operating posture for systems.

### Identity and Access
- IAM policies are expected to grant only the permissions required for intended functionality
- Service-to-service access is expected to follow least-privilege principles
- Privileged access paths are expected to be visible and intentional

### Network Boundaries
- Network boundaries are expected to isolate workloads by trust zone
- Security groups are expected to enforce instance-level access controls
- Network ACLs may be used for additional subnet-level controls where appropriate to scope

### Encryption and Key Management
- Data at rest is expected to be encrypted using KMS or service-managed mechanisms
- Data in transit is expected to use TLS or equivalent protections
- Key usage and rotation expectations are expected to be documented where applicable

### Auditability and Visibility
- Security-relevant actions are expected to be observable
- API activity is expected to be traceable where cloud services are used
- Access logging and retention expectations are expected to be documented

### Secure Defaults
- Default configurations are expected to favor secure behavior
- Public exposure is expected to be explicit rather than implicit
- Unused ports, protocols, and permissions are expected to be closed or removed

---

## Reliability Expectations

Reliability expectations describe how systems are intended to behave under normal and failure conditions.

### Failure Awareness
- Likely failure scenarios are expected to be identified
- Critical execution paths are expected to account for failure behavior
- Degraded operation modes may be defined where appropriate

### Retries and Timeouts
- Retry behavior is expected to use backoff strategies where retries apply
- Timeouts are expected to be explicitly configured
- Circuit-breaking mechanisms may be appropriate for complex or stateful systems

### Idempotency and Determinism
- Operations are expected to tolerate safe retries
- Infrastructure provisioning is expected to be repeatable
- State transitions are expected to be predictable

### Rollback and Recovery
- Rollback procedures are expected to be documented
- Rollback behavior is expected to be considered for critical changes
- Automated rollback may be appropriate where deployment automation exists

### Service Level Awareness
- Long-running or user-facing systems are expected to define service-level intent
- Monitoring is expected to surface indicators relevant to that intent
- Alerting is expected to prioritize meaningful degradation

---

## Cost Expectations

Cost expectations describe how financial impact is considered during system design.

### Resource Sizing
- Resources are expected to be sized according to intended workload behavior
- Auto-scaling may be appropriate where demand varies
- Utilization is expected to be observable

### Spend Awareness
- Primary cost drivers are expected to be identified
- Guardrails or alerts may be appropriate for systems with ongoing cost profiles
- Spending limits are evaluated relative to system purpose

### Cost Transparency
- Cost implications of design decisions are expected to be explained
- Optimization opportunities may be noted where relevant
- Tradeoffs between cost, reliability, and complexity are expected to be acknowledged

---

## Repeatability Expectations

Repeatability expectations describe how systems can be understood, reviewed, and re-executed.

### Documentation
- Business context and system intent are expected to be documented
- Architecture is expected to be described with sufficient clarity
- Implementation steps are expected to be reproducible

### Validation
- Systems are expected to define how behavior is verified
- Expected and observed results are expected to be recorded
- Supporting evidence is expected where verification is performed

### Version Control
- Code and infrastructure are expected to be version controlled
- Changes are expected to be reviewable
- Rollback through version control is expected where applicable

---

## Structural Baseline

Engineering Systems are evaluated against the following structural baseline:

- **Business Context** – Problem statement, requirements, constraints, and scope
- **Architecture** – System design, boundaries, and tradeoffs
- **Implementation** – Step-by-step implementation approach
- **Validation** – Verification procedures, observed results, and notes
- **Executions** – Pattern-specific or procedural walkthroughs

This structure supports consistency, traceability, and independent review.
