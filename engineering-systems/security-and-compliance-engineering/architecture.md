# Architecture: Security and Compliance Engineering

## Quick Orientation

**Scope:** IAM least-privilege policies, secrets management (Secrets Manager), encryption boundaries (KMS), threat detection (GuardDuty), compliance checklist validation, and security event logging.

**Non-Goals:**
- Multi-account organization management (single account focus)
- Advanced threat hunting and forensics
- Custom security tooling development
- Compliance automation beyond basic validation
- SIEM integration or penetration testing

**Key Tradeoffs:**
- **Access Model:** IAM roles (preferred) vs. users (minimize) vs. federated identity (enterprise integration)
- **Encryption Strategy:** CMK (full control, rotation, audit) vs. AWS-managed keys (simpler, less control)
- **Secrets Storage:** Secrets Manager (automatic rotation, higher cost) vs. Parameter Store (lower cost, manual rotation)
- **Threat Detection:** Native GuardDuty (integrated) vs. third-party solutions (more features, higher cost)

**Architecture Patterns:** See [Architecture Patterns](#architecture-patterns) section below for security pattern visualizations.

---

## System Design

The security and compliance architecture provides defense-in-depth security controls including identity management, encryption, secrets management, threat detection, and compliance validation.

## Core Components

### 1. Identity and Access Management (IAM)
- Users, groups, roles, and policies
- Least-privilege access principles
- Cross-account access patterns
- Federated identity (if required)

### 2. Key Management Service (KMS)
- Customer-managed keys (CMK)
- AWS-managed keys
- Key rotation policies
- Encryption integration

### 3. Secrets Management
- Secrets Manager
- Parameter Store
- Automatic secret rotation
- Application integration

### 4. Threat Detection
- GuardDuty
- Security findings and alerts
- Integration with security workflows

### 5. Security Monitoring
- CloudWatch security metrics
- CloudTrail audit logging
- Security event detection
- Incident response procedures

## Architecture Patterns

### Pattern 1: Least-Privilege IAM Access
```
Application → IAM Role → Policy (Explicit Allow) → AWS Service
                                    ↓
                            Explicit Deny (Production)
```

### Pattern 2: Secrets Management with Rotation
```
Application → Secrets Manager → Encrypted Secret
                    ↓
            Lambda Rotation Function
                    ↓
            Updated Secret (Automatic)
```

### Pattern 3: Encryption Boundary with KMS
```
Data Source → KMS CMK → Encrypted Data → Storage
                ↓
        Key Policy (Access Control)
```

### Pattern 4: Defense-in-Depth Security Layers
```
Identity (IAM) → Network (VPC/SG) → Data (Encryption) → Application (Controls) → Monitoring (GuardDuty/CloudTrail)
```

### Pattern 5: Threat Detection Flow
```
CloudTrail Events → GuardDuty Analysis → Security Findings → CloudWatch Alarms → Incident Response
```

## Security Architecture

### Defense-in-Depth Layers

1. **Identity Layer:** IAM policies and roles
2. **Network Layer:** Security groups, NACLs, VPC endpoints
3. **Data Layer:** Encryption at rest and in transit
4. **Application Layer:** Application-level security controls
5. **Monitoring Layer:** Threat detection and security monitoring

## Integration Points

- **All AWS Services:** IAM integration
- **Applications:** Secrets Manager, KMS integration
- **Networking:** VPC security groups, NACLs
- **Monitoring:** CloudWatch, CloudTrail, GuardDuty

---

## Failure Model

**What fails:** IAM policy misconfiguration, secret rotation failure, KMS key access denial, GuardDuty detector misconfiguration, CloudTrail log delivery interruption

**How it fails:** Policy syntax errors cause access denials; secret rotation lambda fails silently; KMS key policy changes lock out applications; GuardDuty disabled loses threat visibility; CloudTrail S3 delivery fails silently

**Blast Radius:** IAM failures affect single service or user; secret rotation failure affects applications using that secret; KMS key failure affects all encrypted resources using that key; GuardDuty failure loses threat detection for entire account; CloudTrail failure loses audit trail for compliance

**Recovery:** IAM Policy Simulator validates before deployment; secret rotation has manual override; KMS key policies support emergency access grants; GuardDuty re-enablement restores detection; CloudTrail S3 delivery has CloudWatch alarms

## Security Model

**Trust Boundaries:** AWS account boundary (external untrusted); IAM role boundary (service-to-service trust); VPC boundary (network isolation); KMS key boundary (encryption domain)

**IAM Model:** Role-based access with least-privilege policies; explicit deny statements for production resources; temporary credentials via STS; no long-lived access keys

**Encryption:** Customer-managed KMS keys for data at rest; TLS 1.2+ for data in transit; envelope encryption for high-volume operations; key rotation every 365 days

**Audit Trail:** CloudTrail logs all API calls with 90-day retention; Secrets Manager logs all secret access; KMS CloudTrail integration logs all key usage; GuardDuty findings stored in S3 with 1-year retention

## Cost Model

**Primary Drivers:** Secrets Manager ($0.40/secret/month + $0.05/10K API calls), GuardDuty ($4.00/VPC/month + $1.00/GB analyzed), KMS ($1.00/CMK/month + $0.03/10K requests), CloudTrail ($2.00/100K events)

**Guardrails:** Budget alert at $40/month; Secrets Manager limited to 10 secrets; GuardDuty data sources limited to VPC Flow Logs and CloudTrail; KMS keys limited to 5 CMKs

**Expected Monthly Range:** $25-45/month for lab environment with standard usage patterns (5 secrets, 1 VPC, 2 KMS keys, moderate API call volume)

## Constraints

**Policy:** Single AWS account focus (no multi-account organization management)

**Org:** No SIEM integration or custom security tooling development

**Cost Ceiling:** Security services budget <$50/month for lab environment

**Latency:** Secret retrieval must complete within 200ms; KMS operations within 100ms

**Data Classification:** Handles PII and sensitive credentials; requires encryption at rest and in transit

**Regions:** Single region deployment (us-east-1 or us-west-2)

## Quality Goals (Detailed)

1. **Security Posture** - How judged: IAM Policy Simulator shows zero over-privileged access; Secrets Manager audit logs show no hardcoded credentials; GuardDuty findings correlate with simulated attacks within 5 minutes

2. **Compliance Adherence** - How judged: All compliance checklist items pass validation; CloudTrail logs show 100% API call coverage; encryption status verified on all data stores

3. **Operational Simplicity** - How judged: Secrets rotate automatically without manual intervention; IAM policies are self-documenting through explicit deny statements; security alerts require <10 minutes to investigate

4. **Cost Efficiency** - How judged: Secrets Manager costs stay under $10/month for standard rotation; GuardDuty costs align with data source volume; KMS key usage optimized to avoid unnecessary key creation

5. **Performance Impact** - How judged: Secret retrieval adds <100ms latency to application startup; KMS encryption/decryption adds <50ms to database operations; GuardDuty analysis does not impact application performance

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |

