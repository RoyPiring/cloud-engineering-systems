# Feature Systems

This directory contains **curated presentations of selected Engineering Systems**, designed to provide a focused review surface for scope, constraints, and validated outcomes.

Feature Systems do not introduce new behavior or requirements. They summarize and route reviewers to their authoritative implementations.

---

## Purpose

Feature Systems exist to support **efficient system review** by presenting a concise view of complete Engineering Systems.

They relate as follows:

- **Engineering Systems** (`/engineering-systems/`)  
  Authoritative, end-to-end system implementations organized by engineering domain (for example networking, security, CI/CD). Each Engineering System includes full documentation, execution paths, and validation evidence and serves as the source of truth.

- **Feature Systems** (this directory)  
  Curated views of selected Engineering Systems. Each Feature System maps **1:1** to an Engineering System and emphasizes system scope, architectural constraints, execution outcomes, and validation evidence. All definitive documentation lives in the corresponding Engineering System.

---

## Featured Systems

See **[FEATURE_SYSTEMS.md](../FEATURE_SYSTEMS.md)** for the complete index of all Feature Systems and their linked evidence.

---

## Template

The `_feature-project-template/` directory defines the standard structure for Feature Systems.

Each Feature System is expected to include:

- **README.md** – System overview and navigation
- **business-context.md** – Problem statement, requirements, constraints, and non-goals
- **architecture.md** – System design and cross-domain integration
- **implementation.md** – Step-by-step implementation approach
- **validation.md** – Verification procedures, observed results, and known failure conditions
- **tradeoffs.md** – Architectural decisions and tradeoffs made during system design

This structure ensures consistency, traceability, and faithful representation of the underlying Engineering System.

---

## Navigation

- **[Root README](../README.md)** – Primary entry point and curated Feature Systems
- **[FEATURE_SYSTEMS.md](../FEATURE_SYSTEMS.md)** – Complete Feature System index and evidence links
- **[Engineering Systems](../engineering-systems/README.md)** – Authoritative system implementations
