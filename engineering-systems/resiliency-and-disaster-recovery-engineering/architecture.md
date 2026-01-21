# Architecture: Resiliency and Disaster Recovery Engineering

## Quick Orientation

**Scope:** Multi-region application deployment, automatic failover with CloudFront origin groups, multi-cloud disaster recovery with Pulumi, and centralized monitoring across regions and clouds.

**Non-Goals:**
- Database replication and failover
- Custom failover logic development
- Advanced disaster recovery testing
- Multi-account organization management
- Hybrid cloud connectivity

**Key Tradeoffs:**
- **Deployment Model:** Multi-region (AWS only, simpler) vs. Multi-cloud (AWS + GCP, higher resilience, more complexity)
- **Failover Strategy:** CloudFront origin groups (automatic, edge-based) vs. Application-level routing (custom logic, higher complexity)
- **Infrastructure Management:** Manual configuration (faster setup, less repeatable) vs. Infrastructure as Code (consistent, version-controlled)
- **Monitoring:** Single-region monitoring (simpler) vs. Multi-cloud monitoring (unified view, more complex)

**Architecture Patterns:** See [Architecture Patterns](#architecture-patterns) section below for disaster recovery pattern visualizations.

---

## System Design

The resiliency and disaster recovery architecture provides multi-region and multi-cloud redundancy with automatic failover, infrastructure-as-code management, and operational visibility.

## Core Components

### 1. Multi-Region Deployment
- AWS App Runner services in multiple regions
- Independent regional deployments
- Region-aware application responses
- GitHub-based automated deployments

### 2. Automatic Failover
- CloudFront distribution with origin groups
- Health check monitoring
- Automatic failover and failback
- Edge-based traffic routing

### 3. Multi-Cloud Resilience
- AWS App Runner services
- GCP Cloud Run service
- Cross-cloud failover capability
- Unified infrastructure management

### 4. Infrastructure as Code
- Pulumi for infrastructure management
- TypeScript for declarative definitions
- Multi-cloud resource control
- Version-controlled infrastructure changes

### 5. Monitoring and Alerting
- CloudWatch alarms for failover events
- Multi-cloud monitoring dashboard
- SNS notifications for incidents
- Centralized observability

## Architecture Patterns

### Pattern 1: Multi-Region Deployment
```
GitHub → App Runner (us-east-1) → Application
     ↓
App Runner (us-west-2) → Application
```

### Pattern 2: CloudFront Origin Group Failover
```
User → CloudFront → Primary Origin (us-east-1)
                ↓ (on failure)
            Secondary Origin (us-west-2)
```

### Pattern 3: Multi-Cloud Disaster Recovery
```
CloudFront → Primary: AWS App Runner (us-east-1)
         ↓ (on failure)
    Secondary: GCP Cloud Run
```

### Pattern 4: Infrastructure as Code Management
```
Pulumi Code → AWS Resources (App Runner, CloudFront)
          ↓
    GCP Resources (Cloud Run)
```

### Pattern 5: Monitoring and Alerting
```
CloudWatch Metrics → CloudWatch Alarms → SNS → Operators
GCP Monitoring Metrics → Unified Dashboard
```

## Design Decisions

- Multi-region deployment strategy (AWS App Runner for consistency)
- Failover mechanism (CloudFront origin groups for automatic failover)
- Multi-cloud approach (Pulumi for Infrastructure as Code across providers)
- Monitoring strategy (CloudWatch and GCP Monitoring with unified dashboard)

---

## Failure Model

**What fails:** Regional outages, cloud provider failures, application service failures, CloudFront misconfiguration, health check failures, Pulumi state corruption

**How it fails:** Regional outage takes down single-region deployment; cloud provider failure affects all services in that cloud; application service failure triggers health check failure; CloudFront misconfiguration prevents failover; health check failure triggers unnecessary failover; Pulumi state corruption prevents infrastructure updates

**Blast Radius:** Regional failure affects only that region (multi-region protects); cloud provider failure affects only that cloud (multi-cloud protects); application service failure affects only that service; CloudFront failure affects all traffic routing; health check failure causes unnecessary failover; Pulumi state issues prevent infrastructure changes

**Recovery:** Multi-region deployment provides automatic failover; multi-cloud deployment provides cross-cloud failover; CloudFront health checks detect failures and route traffic; Pulumi state backups enable recovery; monitoring alerts operators to investigate root causes

---

## Security Model

**Trust Boundaries:** Regional boundary (isolated AWS regions); cloud provider boundary (AWS vs. GCP); edge boundary (CloudFront distribution); application boundary (App Runner/Cloud Run services)

**IAM Model:** Least-privilege IAM roles for infrastructure management; Pulumi credentials scoped to required resources; no cross-cloud access without explicit configuration

**Encryption:** TLS 1.2+ for all application traffic; HTTPS enforced for all endpoints; no unencrypted data transfer

**Audit Trail:** Pulumi state tracks all infrastructure changes; CloudWatch logs capture application behavior; CloudTrail records AWS API calls; GCP audit logs record Cloud Run changes

---

## Cost Model

**Primary Drivers:** App Runner ($0.007/vCPU-hour + $0.0008/GB-hour), CloudFront ($0.085/GB data transfer), Cloud Run ($0.00002400/vCPU-second + $0.00000250/GB-second), Pulumi (free for open source, paid for team features), CloudWatch ($0.50/metric + $0.50/alarm)

**Guardrails:** Budget alert at $100/month; App Runner services limited to 2 regions; CloudFront data transfer monitored; Cloud Run usage optimized; Pulumi state stored in free tier

**Expected Monthly Range:** $60-90/month for lab environment (2 App Runner services, CloudFront distribution, 1 Cloud Run service, moderate traffic, monitoring)

## Constraints

**Policy:** Multi-region deployment within AWS; multi-cloud support for AWS and GCP; infrastructure-as-code required

**Org:** Team expertise in AWS App Runner, CloudFront, Pulumi, and GCP Cloud Run; limited budget for disaster recovery services

**Cost Ceiling:** Disaster recovery services budget <$100/month for lab environment

**Latency:** Failover must complete within 60 seconds; CloudFront edge routing <50ms; cross-cloud failover <5 seconds

**Data Classification:** Application handles standard web traffic; requires high availability; no special compliance requirements

**Regions:** Multi-region deployment in us-east-1 and us-west-2; GCP deployment in us-central1 or us-east1

## Quality Goals (Detailed)

1. **Availability** - How judged: Application remains available during regional outages; failover occurs automatically within 60 seconds; multi-cloud failover validated; uptime >99.9% across all regions

2. **Automation** - How judged: Failover occurs without manual intervention; infrastructure changes managed through Pulumi; deployments automated through GitHub integration

3. **Operational Visibility** - How judged: CloudWatch alarms trigger on failover events; monitoring dashboard shows metrics across regions and clouds; alerting provides actionable intelligence

4. **Cost Efficiency** - How judged: Disaster recovery costs stay under $100/month for lab environment; App Runner usage optimized; CloudFront data transfer monitored; Cloud Run costs controlled

5. **Maintainability** - How judged: Infrastructure managed through Pulumi codebase; changes tracked and versioned; multi-cloud resources controlled from single codebase; deployment procedures documented

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |
