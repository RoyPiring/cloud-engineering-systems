# Changelog

All notable changes to this repository will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [2026-01-16]

### Changed

- **Renamed Engineering System: Revenue-Instrumented Application Platform**
  - Renamed system from "AI FinOps Checkout Platform Engineering" to "Revenue-Instrumented Application Platform"
  - Updated all core documentation files:
    - `README.md` - Updated system name, domain, and terminology throughout
    - `business-context.md` - Updated system name and business context descriptions
    - `architecture.md` - Updated system name and scope descriptions
    - `implementation.md` - Updated system name and implementation descriptions
    - `validation.md` - Updated system name and validation descriptions
  - Updated system directory from `ai-finops-checkout-platform-engineering` to `revenue-instrumented-application-platform`
  - Updated all terminology references from "checkout platform" to "revenue-instrumented application platform" for consistency
  - Execution files maintained with original names (01-ai-finops-vercel.md, 02-ai-finops-stripe.md, 03-ai-finops-posthog.md)
  - Updated image references to reflect new system naming

- **Repository Index Updates**
  - Updated `README.md` (root) to reference "Revenue-Instrumented Application Platform" in "More Engineering Systems" section
  - Updated `engineering-systems/README.md` Engineering Systems Index table with new system name and directory path
  - Updated `engineering-systems/README.md` Additional Engineering Systems list with new system name and directory path

### Fixed

- **Repository Quality and Consistency**
  - Removed duplicate `ai-finops-checkout-platform-engineering` directory after successful rename
  - Performed comprehensive quality check across all 12 engineering systems
  - Verified all required sections present in all systems (System Architecture, How to Read This Repository, Boundaries, Execution Path, Evidence Map)
  - Verified all navigation links and references are accurate and functional
  - Confirmed 100% structural consistency across all engineering systems
  - No linter errors detected

## [2026-01-14]

### Added

- **RAG Knowledge Service Delivery Assurance Engineering System**
  - New engineering system demonstrating production-ready RAG service delivery from development through deployment and testing
  - Includes complete documentation: business context, architecture, implementation, and validation
  - Execution path covering:
    - RAG API development with FastAPI, Chroma, and Ollama
    - Docker containerization for portable deployment
    - Kubernetes orchestration with self-healing capabilities
    - CI/CD automation with semantic testing and deterministic validation
  - Evidence-based validation covering API functionality, containerization, orchestration, and CI/CD automation
  - Location: `engineering-systems/rag-knowledge-service-delivery-assurance-engineering/`
  - Documentation links:
    - [README](./engineering-systems/rag-knowledge-service-delivery-assurance-engineering/README.md)
    - [Business Context](./engineering-systems/rag-knowledge-service-delivery-assurance-engineering/business-context.md)
    - [Architecture](./engineering-systems/rag-knowledge-service-delivery-assurance-engineering/architecture.md)
    - [Implementation](./engineering-systems/rag-knowledge-service-delivery-assurance-engineering/implementation.md)
    - [Validation](./engineering-systems/rag-knowledge-service-delivery-assurance-engineering/validation.md)
    - [Executions](./engineering-systems/rag-knowledge-service-delivery-assurance-engineering/executions/)

### Changed

- Updated repository index files to include new RAG Knowledge Service Delivery Assurance Engineering system
  - Added entry to `engineering-systems/README.md` Engineering Systems Index table
  - Added entry to `engineering-systems/README.md` Additional Engineering Systems list
  - Updated `README.md` (root) "More Engineering Systems" section

### Fixed

- Added "Execution Path (Start to Finish)" sections to implementation documentation:
  - `vpc-networking-engineering/implementation.md`
  - `security-and-compliance-engineering/implementation.md`
  - `cicd-automation-engineering/implementation.md`
- Added "Evidence Map to Executions" section to `rag-knowledge-service-delivery-assurance-engineering/validation.md`
- Standardized evidence references to use full paths (`./executions/...`) in validation documentation
- Added execution path link in `rag-knowledge-service-delivery-assurance-engineering/README.md`

---

## Types of Changes

- **Added** - New features, engineering systems, or capabilities
- **Changed** - Changes to existing functionality or documentation structure
- **Deprecated** - Features or systems that will be removed in future releases
- **Removed** - Removed features or systems
- **Fixed** - Bug fixes, documentation corrections, or consistency improvements
- **Security** - Security-related changes or vulnerability fixes
