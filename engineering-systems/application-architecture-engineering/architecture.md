# Architecture: Application Architecture Engineering

## Quick Orientation

**Scope:** Full-stack cloud-native application architecture from serverless functions to containerized workloads, including three-tier applications, integration patterns, and deployment automation.

**Non-Goals:**
- Multi-cloud application deployments
- Advanced deployment strategies beyond basic patterns
- Custom orchestration tooling development
- Performance testing automation frameworks

**Key Tradeoffs:**
- **Compute Model:** Serverless (event-driven, pay-per-use) vs. Containers (long-running, more control)
- **Architecture:** Microservices (scalable, complex) vs. Monolithic (simpler, less scalable)
- **API Design:** RESTful (standard) vs. GraphQL (flexible queries) vs. gRPC (high performance)
- **Scaling:** Auto-scaling (elastic) vs. Manual scaling (predictable costs)

**Diagram:** See [Architecture Patterns](#architecture-patterns) section below for visual representations.

---

## System Design

This system covers full-stack cloud-native application architecture, from serverless functions to containerized workloads, documenting tradeoffs in service selection and integration patterns.

## Core Components

### 1. Serverless Architecture
- AWS Lambda for compute
- API Gateway for API management
- Event-driven patterns
- Pay-per-use pricing model

### 2. Container Architecture
- Amazon ECS for container orchestration
- Amazon EKS for Kubernetes workloads
- Container registry (ECR)
- Auto-scaling and load balancing

### 3. Three-Tier Application
- Presentation layer (web frontend)
- Application layer (API and business logic)
- Data layer (databases and storage)

### 4. Integration Patterns
- RESTful APIs
- Service-to-service communication
- Event-driven architectures
- Message queues and event buses

## Architecture Patterns

### Pattern 1: Serverless Architecture
```
Client → API Gateway → Lambda → DynamoDB → Response
```

### Pattern 2: Three-Tier Application
```
Client → CloudFront → S3 (Presentation) → API Gateway → Lambda (Logic) → DynamoDB (Data)
```

### Pattern 3: Container-Based Architecture
```
Client → Load Balancer → ECS/EKS → Application Containers → Database
```

### Pattern 4: Hybrid Serverless + Container
```
Event → Lambda (Orchestration) → ECS Task (Processing) → S3/DynamoDB (Storage)
```

## Design Decisions

- Compute model selection criteria
- API design and versioning strategies
- Data access patterns
- Scaling and performance optimization

---

## Failure Model

**What fails:** Lambda function timeouts, container node failures, API Gateway throttling, database connection exhaustion, service dependency failures

**How it fails:** Lambda exceeds 15-minute timeout; container nodes crash due to memory issues; API Gateway rate limits exceeded; database connection pool exhausted; downstream service returns errors

**Blast Radius:** Lambda failure affects only that function's invocations; container node failure affects pods on that node (auto-replaced); API Gateway failure affects all API traffic; database failure affects all application tiers; service dependency failure cascades to dependent services

**Recovery:** Lambda automatic retries with exponential backoff; container auto-scaling replaces failed nodes; API Gateway circuit breakers prevent cascade; database connection pooling with retries; service dependency timeouts and fallbacks

## Security Model

**Trust Boundaries:** Internet boundary (untrusted clients); API Gateway boundary (authenticated requests); VPC boundary (internal services); database boundary (application access only)

**IAM Model:** Least-privilege IAM roles for each service; Lambda execution roles limited to required permissions; container task roles scoped to service needs; no cross-service over-privilege

**Encryption:** TLS 1.2+ for all API traffic; KMS encryption for data at rest; secrets in Secrets Manager; no credentials in code or environment variables

**Audit Trail:** CloudWatch Logs for all application logs (30-day retention); API Gateway access logs; Lambda execution logs; CloudTrail for all AWS API calls; application metrics in CloudWatch

## Cost Model

**Primary Drivers:** Lambda ($0.20 per 1M requests + compute time), EC2/ECS ($0.10-0.50/hour per instance), API Gateway ($3.50 per 1M requests), RDS/Aurora ($0.10-0.50/hour per instance), CloudWatch ($0.50/GB logs + $0.30/metric)

**Guardrails:** Budget alert at $140/month; Lambda concurrency limited to 1000; container instances limited to 2-4 nodes; API Gateway throttling at 10K requests/second; database instance size limited to db.t3.medium

**Expected Monthly Range:** $80-120/month for lab environment with moderate traffic (100K Lambda invocations, 2-4 container nodes, standard database instance, moderate API usage)

## Constraints

**Policy:** Single cloud provider (AWS only); no multi-cloud deployments

**Org:** Team skill sets limited to managed services; no custom orchestration development

**Cost Ceiling:** Application infrastructure budget <$150/month for lab environment

**Latency:** API response time must be <300ms p95; database queries <100ms p95; cold starts <2s

**Data Classification:** Application handles standard application data; requires encryption in transit; no special compliance requirements

**Regions:** Single region deployment (us-east-1 for service availability)

## Quality Goals (Detailed)

1. **Scalability** - How judged: Applications auto-scale based on load (tested with load generators); serverless functions scale to 1000+ concurrent invocations; container clusters scale nodes based on CPU/memory metrics; response times remain <200ms under 10x load

2. **Reliability** - How judged: Application availability >99.9% (measured via health checks); zero-downtime deployments validated; automatic failover tested; error rates <0.1% under normal load

3. **Cost Efficiency** - How judged: Serverless costs align with actual usage (pay-per-invocation); container costs optimized through right-sizing; total compute costs <$100/month for lab; cost per request <$0.001

4. **Performance** - How judged: API response times <200ms p95; cold start times <1s for Lambda; container startup <30s; database query times <50ms p95

5. **Operational Simplicity** - How judged: Deployment time <15 minutes; rollback time <5 minutes; monitoring dashboards provide clear health signals; troubleshooting time <30 minutes for common issues

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |

