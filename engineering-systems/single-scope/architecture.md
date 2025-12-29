# Architecture: Single-Scope Engineering

## Quick Orientation

**Scope:** Standalone labs organized by category (Prerequisites, AI/ML Tools, Storage) with self-contained execution guides for specific tools, services, or concepts.

**Non-Goals:**
- Full system implementations (covered in engineering systems)
- Multi-domain integrations (covered in feature systems)
- Advanced enterprise patterns (covered in engineering systems)
- Comprehensive series progression (covered in engineering systems)
- Production-ready deployments (covered in engineering systems)

**Key Tradeoffs:**
- **Lab Design:** Self-contained (independent, some duplication) vs. Series-based (efficient, dependencies)
- **Scope:** Single tool/concept (focused, clear) vs. Multi-concept (comprehensive, complex)
- **Integration:** Standalone (flexible) vs. Integrated (efficient, dependencies)
- **Documentation:** Quick reference (focused) vs. Comprehensive (detailed, longer)

**Architecture Patterns:** See [Architecture Patterns](#architecture-patterns) section below for lab pattern visualizations.

---

## Overview

Single-scope engineering consists of standalone labs organized by category. Each lab is self-contained and focuses on a specific tool, service, or concept without requiring progression through a series.

## Architecture Components

### Lab Organization

Labs are organized into categories:

1. **Prerequisites**
   - AWS account setup
   - Beginner challenges

2. **AI/ML Tools**
   - AI agents (no-code, web UI)
   - LLM integrations
   - Prompt engineering
   - AWS AI services

3. **Storage**
   - S3 static website hosting
   - Multi-cloud storage patterns

## Component Relationships

```
Single-Scope Engineering
├── Prerequisites
│   ├── AWS Account Setup
│   └── AWS Beginners Challenge
├── AI/ML Tools
│   ├── AI Agent Implementations
│   ├── LLM Integrations
│   ├── Prompt Engineering
│   └── AWS AI Services
└── Storage
    ├── S3 Hosting
    └── Multi-Cloud Patterns
```

## Architecture Patterns

### Pattern 1: Standalone Lab Execution
```
Lab → Self-Contained Setup → Execution → Validation → Cleanup
(No dependencies on other labs)
```

### Pattern 2: Prerequisite Integration
```
Engineering System → Prerequisite Lab → Setup Complete → System Execution
```

### Pattern 3: Quick Reference Pattern
```
Documentation → Lab Reference → Tool/Pattern Lookup → Implementation
```

### Pattern 4: Category-Based Organization
```
Category (Prerequisites/AI/Storage) → Lab → Tool/Service/Concept
```

## Integration Patterns

### Standalone Execution
- Each lab can be completed independently
- No dependencies between labs
- Self-contained documentation

### Prerequisite Integration
- Labs can be used as prerequisites for engineering systems
- Referenced from domain READMEs
- Integrated into domain execution paths

### Quick Reference
- Labs serve as quick guides
- Referenced from other documentation
- Used for specific tool or pattern lookup

## Design Principles

1. **Single Focus:** Each lab addresses one tool, service, or concept
2. **Self-Contained:** All information needed in the lab itself
3. **Clear Scope:** Explicit boundaries and non-goals
4. **Quick Completion:** Designed for focused, time-boxed execution
5. **Reusability:** Can be referenced and integrated elsewhere

## Technology Stack

- **AWS Services:** Account setup, S3, AI services
- **AI Tools:** Agents, LLMs, prompt engineering
- **Storage:** S3, multi-cloud patterns
- **Documentation:** Markdown, execution guides

## Scalability

- New labs can be added without affecting existing labs
- Categories can be expanded as needed
- Integration points remain consistent

---

## Failure Model

**What fails:** Lab setup failures, resource provisioning errors, configuration mistakes, service unavailability, cost overruns, cleanup failures

**How it fails:** Setup scripts fail due to missing prerequisites; CloudFormation stack creation fails; configuration errors prevent execution; AWS service outages; usage exceeds free tier; resources not cleaned up

**Blast Radius:** Setup failure affects only that lab; resource failure affects that lab's execution; configuration error affects that lab only; service outage affects all labs using that service; cost overrun affects budget; cleanup failure leaves orphaned resources

**Recovery:** Setup scripts provide clear error messages; CloudFormation rollback on failure; configuration validation before execution; service status checks; cost monitoring and alerts; cleanup scripts documented

## Security Model

**Trust Boundaries:** Lab boundary (isolated execution); AWS account boundary (standard security); no cross-lab trust; educational use only

**IAM Model:** Least-privilege IAM roles per lab; no shared credentials; lab-specific permissions; cleanup removes all IAM resources

**Encryption:** Standard AWS encryption (TLS in transit, KMS at rest); no special encryption requirements; educational data only

**Audit Trail:** CloudTrail logs all lab resource creation; lab execution logs; cost tracking per lab; cleanup verification

## Cost Model

**Primary Drivers:** Varies by lab type (S3 hosting <$1/month, EC2 instances $5-10/month, AI services $5-15/month, databases $5-10/month)

**Guardrails:** Budget alert at $45/month total; individual lab cost <$15/month; free-tier usage maximized; cleanup scripts remove all resources

**Expected Monthly Range:** $5-15/month per active lab; total single-scope infrastructure <$50/month with multiple labs running simultaneously

## Constraints

**Policy:** Each lab must be self-contained; no dependencies on other single-scope labs; focus on single tool/service/concept

**Org:** Time constraints for quick completion (<2 hours per lab); resource constraints (cost-effective implementations)

**Cost Ceiling:** Individual lab budget <$15/month; total single-scope infrastructure <$50/month

**Latency:** Lab setup must complete in <30 minutes; execution time varies by lab type; no real-time requirements

**Data Classification:** Labs handle standard application data; no special compliance requirements; educational use only

**Regions:** Single region deployment (us-east-1 preferred); some labs may be region-agnostic

## Quality Goals (Detailed)

1. **Independence** - How judged: Labs complete successfully without dependencies on other labs (tested via isolated execution); prerequisites clearly documented; zero cross-lab dependencies; completion time <1 hour per lab

2. **Clarity** - How judged: Lab scope clearly defined in first paragraph; objectives measurable; steps unambiguous; expected outcomes documented; troubleshooting guidance provided

3. **Cost Efficiency** - How judged: Each lab costs <$10/month to run; resource cleanup documented; cost optimization tips provided; free-tier usage maximized where possible

4. **Reusability** - How judged: Labs integrate into larger systems without modification; patterns reusable across domains; documentation supports reference use; code/configs portable

5. **Accessibility** - How judged: Beginner-friendly labs have clear explanations; advanced labs have prerequisites listed; completion time matches skill level; error messages actionable

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |

