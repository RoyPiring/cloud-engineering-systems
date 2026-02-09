# Engineering Systems

This directory contains **authoritative, end-to-end Engineering Systems**, organized by domain.

Each Engineering System is a **complete, validated cloud system** and serves as the **source of truth** for any related Feature Systems. Systems are independently reviewable and document the full lifecycle: context, design, implementation, and validation.

## Repository Structure

- **Feature Systems**  
  Curated entry points surfaced in the root README for focused review.

- **Engineering Systems** *(this directory)*  
  Full system implementations with authoritative documentation and validation.

- **Executions**  
  Pattern-level, procedural walkthroughs supporting system implementation.

- **Single-Scope Engineering**  
  Isolated labs, prerequisites, and narrowly scoped capabilities.

---

## Engineering Systems Index

| System | What It Proves | Start Here | Execution | Evidence |
|------|---------------|-----------|----------|----------|
| [VPC Networking Engineering](./vpc-networking-engineering/README.md) | Secure network baselines and segmentation | [implementation.md](./vpc-networking-engineering/implementation.md) | [executions/](./vpc-networking-engineering/executions/) | [validation.md](./vpc-networking-engineering/validation.md) |
| [Security and Compliance Engineering](./security-and-compliance-engineering/README.md) | Access controls, secrets, threat detection | [implementation.md](./security-and-compliance-engineering/implementation.md) | [executions/](./security-and-compliance-engineering/executions/) | [validation.md](./security-and-compliance-engineering/validation.md) |
| [CI/CD Automation Engineering](./cicd-automation-engineering/README.md) | Automated delivery, policy gates, rollback | [implementation.md](./cicd-automation-engineering/implementation.md) | [executions/](./cicd-automation-engineering/executions/) | [validation.md](./cicd-automation-engineering/validation.md) |
| [Application Architecture Engineering](./application-architecture-engineering/README.md) | Cloud-native application design | [implementation.md](./application-architecture-engineering/implementation.md) | [executions/](./application-architecture-engineering/executions/) | [validation.md](./application-architecture-engineering/validation.md) |
| [Database Services Engineering](./database-services-engineering/README.md) | Data-layer architecture and optimization | [implementation.md](./database-services-engineering/implementation.md) | [executions/](./database-services-engineering/executions/) | [validation.md](./database-services-engineering/validation.md) |
| [Conversational AI Engineering](./conversational-ai-engineering/README.md) | Conversational AI system design | [implementation.md](./conversational-ai-engineering/implementation.md) | [executions/](./conversational-ai-engineering/executions/) | [validation.md](./conversational-ai-engineering/validation.md) |
| [RAG Applications Engineering](./rag-applications-engineering/README.md) | Knowledge-grounded AI systems | [implementation.md](./rag-applications-engineering/implementation.md) | [executions/](./rag-applications-engineering/executions/) | [validation.md](./rag-applications-engineering/validation.md) |
| [RAG Knowledge Service Delivery Assurance Engineering](./rag-knowledge-service-delivery-assurance-engineering/README.md) | Production-ready RAG service delivery from development through deployment and testing | [implementation.md](./rag-knowledge-service-delivery-assurance-engineering/implementation.md) | [executions/](./rag-knowledge-service-delivery-assurance-engineering/executions/) | [validation.md](./rag-knowledge-service-delivery-assurance-engineering/validation.md) |
| [Data Engineering Analytics Engineering](./data-engineering-analytics-engineering/README.md) | Data pipelines and analytics workflows | [implementation.md](./data-engineering-analytics-engineering/implementation.md) | [executions/](./data-engineering-analytics-engineering/executions/) | [validation.md](./data-engineering-analytics-engineering/validation.md) |
| [Event-Driven Serverless Platform Engineering](./event-driven-serverless-platform-engineering/README.md) | Event-driven serverless platform with automatic scaling, AI integration, and deployment automation | [implementation.md](./event-driven-serverless-platform-engineering/implementation.md) | [executions/](./event-driven-serverless-platform-engineering/executions/) | [validation.md](./event-driven-serverless-platform-engineering/validation.md) |
| [AI-Enabled Cloud Security Automation Engineering](./ai-enabled-cloud-security-automation-engineering/README.md) | AI-powered security automation with code scanning, storage assessment, and automated remediation | [implementation.md](./ai-enabled-cloud-security-automation-engineering/implementation.md) | [executions/](./ai-enabled-cloud-security-automation-engineering/executions/) | [validation.md](./ai-enabled-cloud-security-automation-engineering/validation.md) |
| [AI-Powered Development Engineering](./ai-powered-development-engineering/README.md) | Developer productivity systems | [implementation.md](./ai-powered-development-engineering/implementation.md) | [executions/](./ai-powered-development-engineering/executions/) | [validation.md](./ai-powered-development-engineering/validation.md) |
| [AI CICD E2E GitHub Actions Gemini](./ai-cicd-e2e-github-actions-gemini/README.md) | AI-augmented CI with GitHub Actions and Gemini: baseline CI, PR code review, coverage-gated test generation | [implementation.md](./ai-cicd-e2e-github-actions-gemini/implementation.md) | [executions/](./ai-cicd-e2e-github-actions-gemini/executions/) | [validation.md](./ai-cicd-e2e-github-actions-gemini/validation.md) |
| [Resiliency and Disaster Recovery Engineering](./resiliency-and-disaster-recovery-engineering/README.md) | Multi-region and multi-cloud disaster recovery with automatic failover | [implementation.md](./resiliency-and-disaster-recovery-engineering/implementation.md) | [executions/](./resiliency-and-disaster-recovery-engineering/executions/) | [validation.md](./resiliency-and-disaster-recovery-engineering/validation.md) |
| [Revenue-Instrumented Application Platform Engineering](./revenue-instrumented-application-platform-engineering/README.md) | Secure payment processing, privacy-compliant analytics, and rapid deployment | [implementation.md](./revenue-instrumented-application-platform-engineering/implementation.md) | [executions/](./revenue-instrumented-application-platform-engineering/executions/) | [validation.md](./revenue-instrumented-application-platform-engineering/validation.md) |
| [Single-Scope Engineering](./single-scope/README.md) | Isolated labs and prerequisites | [README.md](./single-scope/README.md) | [executions/](./single-scope/executions/) | [validation.md](./single-scope/validation.md) |

---

## Feature Systems (Curated Entry Points)

The following Engineering Systems are surfaced as **Feature Systems** in the root README.  
They are selected to enable efficient review of systems with broad scope and architectural depth.

- **[VPC Networking Engineering](./vpc-networking-engineering/README.md)** – Network isolation, routing, security boundaries  
- **[Security and Compliance Engineering](./security-and-compliance-engineering/README.md)** – Identity, secrets, monitoring, threat detection  
- **[CI/CD Automation Engineering](./cicd-automation-engineering/README.md)** – IaC pipelines with policy enforcement  

Feature Systems are **presentational views only**. Each maps 1:1 to an Engineering System and always points back here for authoritative detail.

---

## Additional Engineering Systems

The following systems expand domain coverage and demonstrate additional **complete, validated implementations**.  
Each is a peer Engineering System and can be reviewed independently.

- [AI CICD E2E GitHub Actions Gemini](./ai-cicd-e2e-github-actions-gemini/README.md)  
- [AI-Enabled Cloud Security Automation Engineering](./ai-enabled-cloud-security-automation-engineering/README.md)  
- [Application Architecture Engineering](./application-architecture-engineering/README.md)  
- [Database Services Engineering](./database-services-engineering/README.md)  
- [Conversational AI Engineering](./conversational-ai-engineering/README.md)  
- [RAG Applications Engineering](./rag-applications-engineering/README.md)  
- [RAG Knowledge Service Delivery Assurance Engineering](./rag-knowledge-service-delivery-assurance-engineering/README.md)  
- [Data Engineering Analytics Engineering](./data-engineering-analytics-engineering/README.md)  
- [Event-Driven Serverless Platform Engineering](./event-driven-serverless-platform-engineering/README.md)  
- [AI-Powered Development Engineering](./ai-powered-development-engineering/README.md)  
- [Resiliency and Disaster Recovery Engineering](./resiliency-and-disaster-recovery-engineering/README.md)  
- [Revenue-Instrumented Application Platform Engineering](./revenue-instrumented-application-platform-engineering/README.md)  

---

## System Structure (Consistent Across All Systems)

Every Engineering System follows the same structure:

- **README.md** – System overview and navigation  
- **business-context.md** – Problem, requirements, constraints, non-goals  
- **architecture.md** – Design, boundaries, tradeoffs  
- **implementation.md** – Step-by-step implementation  
- **validation.md** – Verification, observed results, failure conditions  
- **executions/** – Ordered, pattern-specific walkthroughs  

---

## Systems vs Executions

**Engineering Systems**
- Define the complete end-to-end solution
- Capture scope, architectural decisions, outcomes, and validation evidence

**Executions**
- Focused, procedural guides for specific techniques or patterns
- Numbered and sequential
- Support the system without redefining architectural intent

This separation ensures architectural intent remains stable while procedural learning evolves independently.

---

## Where to Start

- **Overview & Context** → `README.md`, `business-context.md`  
- **Design & Decisions** → `architecture.md`  
- **Build & Validate** → `implementation.md`, `validation.md`  

---

## Navigation

Primary links:  
[Root README](../README.md) |
[Feature Systems Index](../FEATURE_SYSTEMS.md) |
[Engineering Systems Index](./README.md) |
[Operating Requirements](../OPERATING_REQUIREMENTS.md) |
[Quality Standards](../QUALITY_STANDARDS.md)
