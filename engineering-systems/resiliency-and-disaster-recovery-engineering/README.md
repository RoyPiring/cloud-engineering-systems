# Resiliency and Disaster Recovery Engineering
**Domain:** Cloud Resilience & Availability Engineering

## System Architecture
<img width="2752" height="1536" alt="resiliency-and-disaster-recovery-engineering-architecture" src="https://github.com/user-attachments/assets/placeholder" />

## Executive Summary

This repository documents a **comprehensive disaster recovery and resiliency baseline** designed and validated against real-world requirements for multi-region availability, automatic failover, multi-cloud resilience, and operational visibility.

The work demonstrates how to approach disaster recovery as a **system**: framing the problem first, defining constraints, making explicit tradeoffs, executing in phases, and validating outcomes with evidence.

This is not a tutorial repository. It is an architectural and execution record intended for engineers, reviewers, and hiring managers evaluating judgment, rigor, and ownership.

---

## Problem Framing

Applications without disaster recovery capabilities introduce recurring business risks including single-region vulnerability, manual failover processes, no protection against cloud provider failures, and limited visibility into recovery status.

This system addresses the measurable problem of:

- Enabling multi-region availability to survive regional outages (target: application deployed in at least two AWS regions)
- Automating failover to minimize downtime (target: failover within 60 seconds)
- Supporting multi-cloud resilience to reduce dependency on a single provider
- Providing operational visibility for failover events and recovery status

---

## Goals and Success Criteria

The system is evaluated against explicit, testable goals:

- **Availability:** Application remains available during regional outages; failover occurs automatically within 60 seconds; uptime >99.9% across all regions
- **Automation:** Failover occurs without manual intervention; infrastructure changes managed through Infrastructure as Code
- **Operational Visibility:** CloudWatch alarms trigger on failover events; monitoring dashboard shows metrics across regions and clouds
- **Cost Efficiency:** Disaster recovery costs stay under $100/month for lab environment
- **Maintainability:** Infrastructure managed through Pulumi codebase; changes tracked and versioned

These goals are validated through structured testing documented in `validation.md`.

---

## Architecture Overview

**Architecture Style:** Multi-region and multi-cloud disaster recovery with automatic failover and Infrastructure as Code management.

- Multi-region deployment provides regional redundancy through AWS App Runner services
- CloudFront origin groups enable automatic failover between regions
- Multi-cloud deployment extends resilience across AWS and GCP
- Infrastructure as Code manages multi-cloud resources through Pulumi
- Monitoring and alerting provide operational visibility

The design scales from single-region to multi-region to multi-cloud without architectural redesign.

Detailed architecture, tradeoffs, and failure models are documented in `architecture.md`.

---

## Key Engineering Decisions

This system makes the following deliberate decisions:

- **Deployment Model:** Multi-region with AWS App Runner, extended to multi-cloud with GCP Cloud Run
- **Failover Strategy:** CloudFront origin groups for automatic, edge-based failover without application changes
- **Infrastructure Management:** Pulumi for Infrastructure as Code across multiple cloud providers
- **Monitoring Strategy:** CloudWatch and GCP Monitoring with unified dashboard

Each decision includes documented alternatives and rationale in `architecture.md`.

---

## Execution and Validation Model

The system is built incrementally, with validation at each stage:

1. Multi-region foundation with AWS App Runner
2. Automatic failover with CloudFront origin groups
3. Multi-cloud resilience with Pulumi
4. Monitoring and alerting for operational visibility

Execution steps and sequencing are documented in `implementation.md`.

Validation is performed through explicit checks covering multi-region deployment, automatic failover, multi-cloud disaster recovery, and monitoring. Evidence and expected outcomes are documented in `validation.md`.

---

## Repository Structure

This repository is intentionally structured to reflect how real systems are reviewed:

- **Business Context**  
  Problem statement, requirements, constraints  
  → `business-context.md`

- **Architecture**  
  System design, tradeoffs, failure models  
  → `architecture.md`

- **Implementation**  
  Execution phases and build decisions  
  → `implementation.md`

- **Validation**  
  Test results and evidence of correctness  
  → `validation.md`

Each document stays within its scope. Redundancy is minimized by design.

---

## How to Read This Repository

Recommended reading order for reviewers:

1. `README.md` – System orientation
2. `business-context.md` – Why the system exists
3. `architecture.md` – How the system is designed
4. `implementation.md` – How the system was built
5. `validation.md` – Proof the system behaves as intended

---

## Intended Audience

This repository is written for:

- Cloud and platform engineers evaluating disaster recovery approaches
- Site reliability engineers reviewing availability and failover strategies
- Hiring managers assessing senior or principal-level judgment
- Technical reviewers validating execution discipline and evidence

---

## Scope and Non-Goals

**In Scope**
- Multi-region application deployment
- Automatic failover between regions
- Multi-cloud disaster recovery
- Infrastructure-as-code management
- Monitoring and alerting for failover events

**Out of Scope**
- Database replication and failover
- Custom failover logic development
- Advanced disaster recovery testing
- Multi-account organization management
- Hybrid cloud connectivity (VPN or Direct Connect)

These exclusions are deliberate and documented to preserve clarity and focus.

---

## Boundaries

This engineering system operates within the following boundaries:

- **Policy Constraints:** Multi-region deployment within AWS; multi-cloud support for AWS and GCP; infrastructure-as-code required ([constraints](./business-context.md))
- **Organizational Constraints:** Team expertise in AWS App Runner, CloudFront, and Pulumi; integration with existing deployment workflows; budget constraints ([constraints](./business-context.md))
- **Technical Constraints:** Failover must complete within 60 seconds; multi-region deployment in us-east-1 and us-west-2; infrastructure changes managed through Pulumi ([constraints](./architecture.md))
- **Cost Boundaries:** Disaster recovery services budget <$100/month for lab environment; production costs scale with usage ([cost model](./architecture.md))

Complete constraint definitions are documented in `business-context.md` and `architecture.md`.

---

## Summary

This repository represents a complete disaster recovery system lifecycle: from problem framing, through design and execution, to validation.

The emphasis is on **how decisions are made, constrained, and verified**, not on listing tools or services. The result is a defensible, repeatable disaster recovery baseline suitable for real-world cloud environments.

---

## Next Areas of Expansion

- Database replication and failover strategies
- Advanced disaster recovery testing and simulation
- Multi-account organization management
- Cost optimization strategies for disaster recovery
- Advanced monitoring and observability patterns

Each expansion builds on this baseline without architectural rework.

---

## Navigation

| Next |
|------|
| [Business Context](./business-context.md) |
