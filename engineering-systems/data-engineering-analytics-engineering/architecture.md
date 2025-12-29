# Architecture: Data Engineering Analytics Engineering

## Quick Orientation

**Scope:** Data engineering workflows using Model Context Protocol (MCP) for database interaction, including ETL/ELT pipelines, query optimization, indexing strategies, and production monitoring patterns.

**Non-Goals:**
- Advanced data warehousing solutions
- Real-time streaming analytics beyond basic patterns
- Custom data processing frameworks
- Multi-region data replication

**Key Tradeoffs:**
- **Database:** Containerized (flexible, lower cost) vs. Managed (production-ready, higher cost)
- **Pipeline Pattern:** ETL (transform before load) vs. ELT (load then transform) vs. Streaming (real-time)
- **Processing:** Batch (simpler, predictable) vs. Streaming (real-time, more complex)
- **Optimization:** Indexing (faster queries, storage cost) vs. Query tuning (no storage cost, development time)

**Diagram:** See [Architecture Patterns](#architecture-patterns) section below for visual representations.

---

## System Design

This system covers data engineering workflows using Model Context Protocol (MCP) for database interaction, analysis, and optimization.

## Core Components

### 1. Database Infrastructure
- Containerized databases for development
- Managed databases for production
- Database selection and configuration
- Connection management

### 2. Data Pipelines
- ETL (Extract, Transform, Load) patterns
- ELT (Extract, Load, Transform) patterns
- Streaming data processing
- Batch processing workflows

### 3. Query Optimization
- Indexing strategies
- Query performance tuning
- Execution plan analysis
- Cost optimization

### 4. MCP Integration
- Model Context Protocol setup
- Database interaction via MCP
- Analysis and optimization workflows
- AI-assisted data engineering

### 5. Production Patterns
- Monitoring and observability
- Error handling and retry logic
- Scalability patterns
- Cost optimization

## Architecture Patterns

### Pattern 1: ETL Pipeline
```
Source Data → Extract → Transform → Load → Target Database
```

### Pattern 2: ELT Pipeline
```
Source Data → Extract → Load → Transform (In-Database) → Analytics
```

### Pattern 3: MCP-Assisted Data Engineering
```
Developer → MCP Client → PostgreSQL MCP → Database Operations → Results
```

### Pattern 4: Batch Processing Workflow
```
Data Source → Batch Job → Processing → Validation → Storage → Analytics
```

## Design Decisions

- Database selection (containerized vs. managed)
- Data pipeline patterns (ETL vs. ELT vs. streaming)
- Query optimization strategies
- Production reliability patterns

---

## Failure Model

**What fails:** Pipeline execution failures, query timeouts, data quality validation failures, storage capacity limits, database connection failures, transformation errors

**How it fails:** Pipeline steps fail due to data format issues; queries exceed timeout limits; validation rules reject data; storage fills causing write failures; database connections exhausted; transformation logic errors

**Blast Radius:** Pipeline failure affects downstream consumers; query timeout affects that operation; validation failure affects that data batch; storage failure affects all writes; connection failure affects all database operations; transformation error affects that pipeline stage

**Recovery:** Pipeline retries with exponential backoff; query optimization reduces timeouts; validation provides detailed error reports; storage auto-scaling; connection pooling with retries; transformation error handling and logging

## Security Model

**Trust Boundaries:** Data source boundary (external systems); pipeline boundary (internal processing); database boundary (trusted storage); consumer boundary (downstream applications)

**IAM Model:** Least-privilege IAM roles for pipeline execution; database access scoped to required tables; no cross-environment access; MCP access limited to development databases

**Encryption:** TLS for all database connections; encryption at rest for data storage; no sensitive data in logs; secrets in Secrets Manager; data masking for sensitive fields

**Audit Trail:** CloudWatch Logs for all pipeline executions (30-day retention); query execution logs; data quality validation results; database access logs; CloudTrail for all AWS API calls; data lineage tracking

## Cost Model

**Primary Drivers:** Database compute (containerized = ~$15/month), data processing compute ($0.10/hour = ~$10/month), storage ($0.023/GB = ~$8/month), CloudWatch Logs ($0.50/GB = ~$5/month)

**Guardrails:** Budget alert at $45/month; database instances limited to 2 containers; processing compute limited to 100 hours/month; storage limited to 50GB; log retention limited to 30 days

**Expected Monthly Range:** $30-40/month for lab environment with standard usage (moderate data volume, standard processing frequency, containerized databases, standard logging)

## Constraints

**Policy:** Single region deployment; containerized databases for development; no advanced data warehousing

**Org:** MCP-based database interaction; team expertise in SQL and basic ETL; no custom processing frameworks

**Cost Ceiling:** Data engineering infrastructure budget <$50/month for lab environment

**Latency:** Query execution must complete in <200ms p95; pipeline execution <30 minutes for standard batch; real-time processing <5 seconds

**Data Classification:** Handles application data; requires data quality validation; no special compliance beyond standard practices

**Regions:** Single region deployment (us-east-1 for service availability)

## Quality Goals (Detailed)

1. **Query Performance** - How judged: Query execution time <100ms p95 for optimized queries (measured via query plans); index utilization >90%; query optimization reduces execution time by 60%; parallel processing improves throughput by 3x

2. **Pipeline Reliability** - How judged: Pipeline success rate >99.9% (measured via execution logs); error handling tested; data quality validation passes; retry logic handles transient failures; zero data loss in failures

3. **Data Quality** - How judged: Data validation rules pass >99% of records; schema validation enforced; data completeness >95%; duplicate detection functional; data lineage tracked

4. **Cost Efficiency** - How judged: Data processing costs <$25/month; storage costs <$15/month; total data infrastructure <$40/month; cost per GB processed <$0.01

5. **Scalability** - How judged: Pipelines handle 10x data volume without redesign; query performance maintained with 10x data growth; storage scales automatically; processing scales horizontally

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |

