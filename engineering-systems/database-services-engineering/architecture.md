# Architecture: Database Services Engineering

## Quick Orientation

**Scope:** Data layer architecture and optimization with managed database services, including NoSQL (DynamoDB) and relational (Aurora) database selection, data modeling, query optimization, and application integration.

**Non-Goals:**
- Multi-region database replication beyond basic patterns
- Advanced data warehousing solutions
- Custom database tooling development
- Complex data migration automation

**Key Tradeoffs:**
- **Database Type:** NoSQL (high-scale, low-latency) vs. Relational (complex queries, transactions)
- **Capacity Model:** Provisioned (predictable) vs. On-demand (elastic, pay-per-use)
- **Availability:** Single-AZ (lower cost) vs. Multi-AZ (high availability, higher cost)
- **Scaling:** Vertical (larger instance) vs. Horizontal (read replicas, sharding)

**Diagram:** See [Architecture Patterns](#architecture-patterns) section below for visual representations.

---

## System Design

This system covers managed database services on AWS, from NoSQL to relational databases, demonstrating data layer architecture and performance optimization.

## Core Components

### 1. NoSQL Databases
- Amazon DynamoDB for key-value and document storage
- Partition key design for scalability
- On-demand vs. provisioned capacity
- Global tables for multi-region replication

### 2. Relational Databases
- Amazon Aurora for MySQL/PostgreSQL compatibility
- Multi-AZ deployment for high availability
- Read replicas for read scaling
- Serverless v2 for auto-scaling

### 3. Data Modeling
- Partition key and sort key design
- Access pattern optimization
- Indexing strategies
- Query optimization

### 4. Integration Patterns
- Application-to-database connectivity
- Connection pooling
- Transaction management
- Data migration patterns

## Architecture Patterns

### Pattern 1: NoSQL Data Access
```
Application → DynamoDB API → Partition Key Lookup → Item Retrieval → Response
```

### Pattern 2: Relational Database Access
```
Application → Aurora Connection → SQL Query → Transaction → Result Set → Response
```

### Pattern 3: Hybrid Database Architecture
```
Application → DynamoDB (Hot Data) → Aurora (Analytics) → Aggregated Results
```

### Pattern 4: Read Replica Scaling
```
Application → Aurora Primary (Writes) → Read Replicas (Reads) → Load Distribution
```

## Design Decisions

- Database type selection criteria
- Data modeling and access patterns
- Scaling strategies (provisioned vs. on-demand)
- High availability and replication patterns

---

## Failure Model

**What fails:** Database instance failures, connection pool exhaustion, query timeouts, storage capacity limits, read replica lag, backup failures

**How it fails:** Primary instance crashes triggering failover; connection pool maxed out causing connection errors; complex queries exceed timeout limits; storage fills causing write failures; read replica lag exceeds acceptable threshold; backup jobs fail silently

**Blast Radius:** Primary instance failure affects all write operations until failover; connection exhaustion affects all application instances; query timeout affects that specific operation; storage failure affects all write operations; read replica failure affects read scaling; backup failure affects recovery capability

**Recovery:** Automatic multi-AZ failover within 60 seconds; connection pool auto-scaling and retries; query optimization and timeout tuning; storage monitoring and auto-scaling; read replica monitoring and replacement; backup verification and alerting

## Security Model

**Trust Boundaries:** Application boundary (trusted applications only); database boundary (no direct internet access); VPC boundary (network isolation); IAM boundary (role-based access)

**IAM Model:** Database-specific IAM roles for applications; least-privilege database user accounts; no shared credentials; role-based authentication for Aurora; IAM authentication for DynamoDB

**Encryption:** KMS encryption for data at rest (Aurora and DynamoDB); TLS for all database connections; encryption in transit mandatory; key rotation every 365 days; no unencrypted backups

**Audit Trail:** CloudTrail logs all database API calls; Aurora audit logs enabled; DynamoDB CloudWatch metrics; database connection logs; query performance insights stored; backup and restore events logged

## Cost Model

**Primary Drivers:** DynamoDB on-demand ($1.25 per million write units + $0.25 per million read units = ~$30/month for moderate usage), Aurora ($0.10-0.50/hour per instance + storage $0.10/GB = ~$50/month), backup storage ($0.095/GB = ~$5/month), data transfer ($0.01/GB = ~$2/month)

**Guardrails:** Budget alert at $90/month; DynamoDB on-demand mode (no provisioned capacity); Aurora instance limited to db.t3.medium; storage limited to 100GB; backup retention limited to 7 days

**Expected Monthly Range:** $60-85/month for lab environment with standard usage (moderate DynamoDB throughput, 1 Aurora primary + 1 read replica, standard storage, minimal data transfer)

## Constraints

**Policy:** Single region deployment; no cross-region replication beyond basic patterns

**Org:** Managed services only; no custom database development; team expertise in standard SQL/NoSQL

**Cost Ceiling:** Database infrastructure budget <$100/month for lab environment

**Latency:** Query response time must be <100ms p95; connection establishment <500ms; failover time <60 seconds

**Data Classification:** Handles application data; requires encryption at rest and in transit; no special compliance requirements beyond standard encryption

**Regions:** Single region deployment (us-east-1 for service availability and cost)

## Quality Goals (Detailed)

1. **Performance** - How judged: Query latency <10ms p95 for indexed queries; DynamoDB single-digit millisecond latency; Aurora query times <50ms p95; read replica lag <100ms; connection pool utilization >80%

2. **Availability** - How judged: Database uptime >99.99% (measured via health checks); automatic failover completes in <60 seconds; backup and restore tested; zero data loss in failover scenarios

3. **Scalability** - How judged: DynamoDB handles 10x throughput increase without throttling; Aurora read replicas scale to 15 instances; database supports 10x data growth; connection scaling tested to 1000+ connections

4. **Cost Efficiency** - How judged: DynamoDB on-demand costs align with actual usage; Aurora instance costs optimized through right-sizing; storage costs <$20/month; total database costs <$80/month for lab

5. **Data Integrity** - How judged: Transaction consistency validated; referential integrity enforced; backup verification successful; point-in-time recovery tested within 5-minute RPO

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |

