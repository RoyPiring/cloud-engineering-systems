# Architecture: VPC Networking Engineering

## Quick Orientation

**Scope:** Secure, scalable AWS VPC networking with subnet segmentation, network-level security controls, private AWS service connectivity, multi-AZ high availability, and optional multi-VPC connectivity patterns.

**Non-Goals:**
- Multi-region or global networking
- Hybrid connectivity (VPN or Direct Connect)
- Advanced routing protocols (BGP, OSPF)
- Custom DNS architectures
- Application-layer security controls
- Large-scale automation platforms

**Key Tradeoffs:**
- **Subnet Design:** Public (internet access, higher exposure) vs. Private (NAT required, more secure) vs. Isolated (no internet, most secure)
- **NAT Strategy:** NAT Gateway (managed, higher cost) vs. NAT Instance (self-managed, lower cost)
- **VPC Endpoints:** Gateway endpoints (free, S3/DynamoDB only) vs. Interface endpoints (cost per hour, all services)
- **Multi-VPC:** VPC Peering (simple, non-transitive) vs. Transit Gateway (scalable, transitive, higher cost)
- **Security:** Security Groups (stateful, instance-level) vs. Network ACLs (stateless, subnet-level)

**Diagram:** See [Architecture Patterns](#architecture-patterns) section below for visual representations.

---

## System Design

This system covers secure, scalable AWS VPC networking architecture, from single-VPC foundations to multi-VPC connectivity patterns, documenting tradeoffs in security, cost, and operational complexity.

## Core Components

### 1. VPC Foundation
- Custom VPC with CIDR planning
- Multi-AZ subnet distribution
- DNS resolution and hostnames
- Resource tagging and organization

### 2. Subnet Segmentation
- Public subnets for internet-facing resources
- Private subnets for application workloads
- Isolated subnets for data-tier resources
- Explicit routing per subnet tier

### 3. Network Security
- Security Groups for stateful, instance-level controls
- Network ACLs for stateless, subnet-level defense-in-depth
- VPC Endpoints for private AWS service access
- Explicit trust boundaries and least-privilege access

### 4. Connectivity Patterns
- Internet Gateway for public internet access
- NAT Gateway for private subnet outbound access
- VPC Peering for multi-VPC connectivity
- Transit Gateway for scalable hub-and-spoke patterns

### 5. Observability
- VPC Flow Logs for traffic analysis
- CloudTrail for network change auditing
- Cost monitoring and anomaly detection

---

## Architecture Patterns

### Pattern 1: Public Subnet Traffic Flow
```
Internet → Internet Gateway → Public Subnet → EC2 Instance → Response → Internet
```

### Pattern 2: Private Subnet Traffic Flow
```
EC2 Instance (Private) → NAT Gateway → Internet Gateway → Internet → Response → NAT → EC2
```

### Pattern 3: Isolated Subnet with VPC Endpoint
```
EC2 Instance (Isolated) → VPC Endpoint → AWS Service (S3/DynamoDB) → Response → EC2
```

### Pattern 4: Multi-VPC Connectivity
```
VPC A → VPC Peering → Route Tables → VPC B → Cross-VPC Communication
```

### Pattern 5: Security-Enforced Communication
```
Source → Security Group (Allow) → Network ACL (Allow) → Route Table → Destination
```

---

## Design Decisions

- **Subnet tiering strategy:** Public, private, and isolated subnets for security segmentation
- **NAT Gateway placement:** Per-AZ deployment for high availability
- **Security enforcement:** Security Groups as primary control, Network ACLs as defense-in-depth
- **VPC Endpoint selection:** Gateway endpoints preferred, interface endpoints used selectively
- **Multi-VPC connectivity:** VPC Peering for small scale, Transit Gateway for hub-and-spoke
- **CIDR planning:** Sized for 10x growth to avoid re-addressing
- **Route table design:** Explicit routing per subnet tier, no shared catch-all tables
- **Observability:** VPC Flow Logs mandatory, CloudTrail for change auditing

---

## Failure Model

**What fails:** Route table misconfiguration, security group errors, NAT Gateway failures, VPC Endpoint misconfigurations, CIDR exhaustion, internet gateway attachment failures

**How it fails:** Route table misconfiguration causes traffic blackholes; security group errors allow unintended access or block legitimate traffic; NAT Gateway failure in single AZ loses outbound internet for private subnets; VPC Endpoint misconfig prevents AWS service access; CIDR exhaustion blocks new resource deployment; internet gateway detachment breaks public subnet connectivity

**Blast Radius:** Route table failure affects only the affected subnet; security group error affects only the specific workload; NAT Gateway failure affects private subnets in that AZ only; VPC Endpoint failure affects only the specific service; CIDR exhaustion affects only new resource deployments; internet gateway failure affects all public subnets

**Recovery:** Route tables validated before deployment; security group changes tested incrementally; NAT Gateways deployed per AZ for redundancy; endpoint health monitored and auto-recovered; CIDR sizing prevents address exhaustion; internet gateway attachment validated in change control

---

## Security Model

**Trust Boundaries:** Internet boundary (untrusted external traffic); VPC boundary (trusted internal traffic); subnet boundary (segmentation by exposure); security group boundary (workload-specific access); VPC endpoint boundary (private AWS service access)

**IAM Model:** Least-privilege IAM roles for network resource management; no cross-account VPC access without explicit peering; security group rules scoped to specific source/destination; VPC endpoint policies restrict service access

**Encryption:** TLS 1.2+ for all internet-facing traffic; VPC endpoints use AWS private network (no internet traversal); no unencrypted data transfer across untrusted networks; CloudTrail logs encrypted at rest

**Audit Trail:** VPC Flow Logs capture all network traffic (30-day retention); CloudTrail records all network-related API changes; security group changes logged and reviewed; route table changes tracked in change control; cost anomalies flag potential security misconfigurations

---

## Cost Model

**Primary Drivers:** NAT Gateway ($0.045/hour + $0.045/GB data processed), Interface VPC Endpoints ($0.01/hour per endpoint), Data transfer across AZs ($0.01/GB), Flow Log ingestion and storage ($0.50/GB logs), Internet Gateway (free, data transfer charges apply)

**Guardrails:** Budget alert at $60/month; NAT Gateway limited to 2 per VPC (one per AZ); interface endpoints limited to required services only; Flow Logs enabled selectively; data transfer monitored for anomalies

**Expected Monthly Range:** $30-50/month for lab environment (2 NAT Gateways, 2-3 interface endpoints, moderate data transfer, selective Flow Logs)

## Constraints

**Policy:** Single cloud provider (AWS only); no multi-cloud networking; no hybrid connectivity (VPN/Direct Connect)

**Org:** Team skill sets limited to AWS managed networking services; no custom routing protocol development

**Cost Ceiling:** Network infrastructure budget <$60/month for lab environment

**Latency:** Inter-AZ data transfer <5ms; VPC endpoint access <10ms; internet gateway egress <50ms

**Data Classification:** Network handles standard application traffic; requires encryption in transit; no special compliance requirements beyond standard AWS security

**Regions:** Single region deployment (us-east-1 for service availability and cost optimization)

## Quality Goals (Detailed)

1. **Security** - How judged: Unauthorized traffic blocked and logged (validated via Flow Logs); zero cross-subnet access without explicit rules; security group violations logged; network ACLs provide defense-in-depth

2. **Reliability** - How judged: No single points of failure (NAT Gateways per AZ); route table redundancy; automatic failover for NAT Gateways; network availability >99.9%

3. **Scalability** - How judged: CIDR blocks sized for 10x growth; subnet addressing supports expansion; routing tables below AWS limits; architecture supports Transit Gateway transition

4. **Cost Efficiency** - How judged: Network costs constrained to <$60/month for lab; Gateway endpoints preferred over interface endpoints; NAT usage optimized through subnet design; cost per GB data transfer tracked

5. **Operational Simplicity** - How judged: Network topology clear and reviewable; troubleshooting time <30 minutes for common issues; Flow Logs provide traffic visibility; route table changes validated before deployment

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |
