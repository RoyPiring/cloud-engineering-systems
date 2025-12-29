<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Security Monitoring System

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-monitoring)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Reference  
**Audience:** Builder | Designer | Learner  
**Production Use:** Conditional  
**System Dependency:** Optional

**Prerequisites:**
- AWS account with CloudTrail, CloudWatch, and SNS access
- Secrets Manager secret for monitoring
- Email address for SNS subscription
- Understanding of CloudTrail event logging
- Basic knowledge of CloudWatch metrics and alarms
- AWS CLI installed for testing

**Outputs:**
- CloudTrail trail configuration
- CloudWatch metrics and alarms
- SNS topic and subscription
- Security monitoring validation results
- Alert notification test evidence

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-monitoring_reghtjy)

---

## Introducing Today's Project!

### Project overview

This project implements a basic security monitoring capability within an AWS account. It focuses on capturing control plane activity, emitting operational signals, and generating notifications when predefined activity thresholds are exceeded. The system is intended to provide visibility into API usage patterns rather than full threat detection or incident response coverage.

### Tools and concepts

The system is composed of managed AWS services that address discrete responsibilities. AWS Secrets Manager is used as a monitored resource to generate controlled API activity. AWS CloudTrail records API calls across the account and provides the authoritative audit log. Amazon CloudWatch consumes CloudTrail-derived metrics and evaluates them against thresholds. Amazon SNS delivers notifications when those thresholds are breached. The AWS CLI is used to generate repeatable API activity for validation.

### Project reflection

The implementation demonstrates the end-to-end signal flow from API invocation through audit logging, metric evaluation, and notification delivery. Threshold tuning is intentionally simple and highlights the tradeoff between sensitivity and noise in alert-based monitoring systems. The outcome validates functional integration rather than production-grade alert fidelity.

---

## Create a Secret

AWS Secrets Manager is used as a representative sensitive resource whose access can be monitored. It provides centralized storage and controlled retrieval of secrets while emitting auditable API events. The secret exists to generate predictable read activity that can be observed through CloudTrail and evaluated by downstream monitoring components.

A secret named MyProjectSecrets is created to store placeholder credential values associated with an S3 use case. The secret itself is not used by an application and exists solely to produce access events for monitoring validation.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-monitoring_o5p6q7r8)

---

## Set Up CloudTrail

AWS CloudTrail is configured to record management events for the account and deliver them to an S3-backed log store. Its role in this system is to provide an immutable record of API activity that can be analyzed for security and compliance signals.

Management events, data events, and Insights events are enabled to ensure visibility across control plane actions and selected data plane access. This configuration supports broad activity coverage rather than minimal logging.

### Read vs Write Activity

Read API activity represents access to existing resources and metadata. Write API activity represents resource creation, modification, or deletion. Both categories are included because security-relevant behavior can occur in either path, and excluding one would create blind spots in monitoring.

---

## Verifying CloudTrail

Secret access is performed through both the AWS Management Console and the AWS CLI to generate management API calls. This confirms that CloudTrail is capturing events from multiple access paths.

Captured events are reviewed in the CloudTrail console to validate timestamps, principals, and accessed resources. This verification confirms that the audit layer is functioning and that downstream monitoring is operating on complete input data.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-monitoring_s8t9u0v1)

---

## CloudWatch Metrics

Amazon CloudWatch Logs provides centralized ingestion and analysis of log-derived data. .

In this system, it serves as the bridge between raw CloudTrail events and actionable metrics

CloudTrail Event History is suitable for retrospective inspection, while CloudWatch enables near real-time evaluation and alerting. Metrics represent quantified event counts over time and form the basis for automated threshold evaluation.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-monitoring_a9b0c1d2)

---

## CloudWatch Alarm

A CloudWatch alarm is configured to evaluate API activity metrics against a static threshold. Its purpose is to detect abnormal increases in activity volume rather than classify specific malicious actions.

An Amazon SNS topic is used as the notification endpoint for the alarm. It decouples alert generation from alert delivery and allows multiple subscribers to receive the same signal.

Email subscription confirmation is required by SNS to ensure that notifications are delivered only to verified endpoints. This control prevents unintended data disclosure and enforces explicit consent for alert receipt.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-monitoring_fsdghstt)

---

## Troubleshooting Notification Errors

Validation is performed by repeatedly accessing the monitored secret via the AWS CLI to artificially increase API call volume. 

This approach tests the full signal path under controlled conditions.

Initial notification failures are traced to an unconfirmed SNS email subscription. Confirming the subscription resolves delivery issues and restores end-to-end alerting functionality

---

## Success!

System validation confirms that CloudTrail records API activity and that CloudWatch alarms trigger SNS notifications when thresholds are exceeded. This demonstrates functional integration across logging, monitoring, and notification layers.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-monitoring_ageraergearge)

---

## Comparing CloudWatch with CloudTrail Notifications

CloudTrail provides authoritative audit records but does not natively support real-time alerting. CloudWatch enables operational monitoring but can produce excessive noise if thresholds are not tuned to workload baselines.

Effective use requires deliberate filtering and prioritization to avoid alert fatigue while preserving security visibility.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-monitoring_d7e8f9g0)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Boundary Enforcement](./03-boundary-enforcement.md) | [Evidence Collection](./05-evidence-collection.md) |
