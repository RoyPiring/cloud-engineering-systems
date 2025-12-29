<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Data Engineering with DBT MCP

**Project Link:** [View Project](http://learn.nextwork.org/projects/mcp-data-engineer2)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer2_dbt1l2m3n)

---

## Introducing Today's Project!

This project implements a reproducible data transformation workflow that converts raw PostgreSQL data into analytics-ready tables using dbt executed through Cursor with MCP integration. The system exists to formalize transformation logic, enforce consistency, and support downstream analysis through versioned, testable models rather than ad hoc SQL.

### Key tools and concepts

The primary tools in use are dbt for transformation and testing, PostgreSQL as the source system, and Cursor with MCP for assisted development. The implementation relies on SQL constructs such as common table expressions, aggregate functions, and window functions to structure transformations in a maintainable and auditable way.

### Challenges and wins

The main constraint encountered was enforcing data quality rules through dbt tests, specifically value constraints on categorical fields. Resolving test failures validated that transformation logic and source data assumptions were aligned. The resulting dbt-generated documentation provides a system-level view of models and dependencies rather than relying on tribal knowledge.

### Why I did this project

The purpose of this project was to practice structured data transformation using dbt against a relational source and to establish a baseline pattern for analytics pipelines that can later be scheduled and orchestrated by external workflow systems.

---

## Setting Up DBT

This phase establishes dbt as the transformation layer on top of an existing PostgreSQL source. The setup ensures that dbt can consistently connect to the database, manage models as code, and execute transformations in a repeatable manner. Cursor MCP is introduced to assist with authoring and inspecting transformations within the project context.

### Verifying PostgreSQL

PostgreSQL is verified as an operational dependency by confirming the container runtime state and successful connection attempts. The database provides a customer-centric table that serves as the authoritative raw dataset for all downstream dbt models.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer2_dbt2c3d4e)

### Initializing DBT

The dbt project initialization creates the required directory structure and configuration files that define how dbt connects to PostgreSQL. Connection parameters are explicitly configured so that transformations execute against the intended database and schema without manual intervention.

---

## Connecting DBT MCP

DBT MCP is configured within Cursor to bind the dbt project context to the editor environment. This integration ensures that transformations, tests, and documentation are authored against the active project state and executed consistently with the initialized dbt configuration.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer2_dbt6g7h8i)

---

## Building My First DBT Model

### What is a DBT model?

A dbt model is defined to transform raw customer data into a more analytics-friendly representation. The model encapsulates transformation logic in SQL files that can be versioned, tested, and reused across environments, reducing reliance on manual query execution.

### My model uses:

The model uses common table expressions to structure intermediate logic, aggregate functions to derive customer-level metrics, and window functions to analyze relationships across rows. These constructs are chosen to keep transformations readable while supporting non-trivial analytical queries.

### Running the transformation

The transformation is executed using dbt run, producing a materialized result set from the source data. The output validates that the model processes the full dataset and produces summary metrics suitable for analytical consumption rather than operational querying.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer2_dbt1l2m3n)

---

## Testing Data Quality

Data quality tests are added to enforce basic integrity and domain constraints at the model level. These tests act as guardrails to detect invalid or unexpected data states before transformed data is consumed downstream.

### Adding tests to schema.yml

Tests are defined in schema.yml to ensure required fields are populated, identifiers are unique, and categorical values conform to an explicitly defined set. This formalizes assumptions about the data rather than leaving them implicit in queries.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer2_dbt5o6p7q)

### Fixing the failing test

The accepted_values test fails when source data does not conform to the defined domain for customer segmentation. The issue is resolved by aligning the underlying data with the declared constraints, after which all dbt tests pass. This confirms that model expectations and source data are consistent.

---

## Auto-Generated, Interactive Docs

DBT documentation is used as a system reference for understanding model structure, dependencies, and assumptions. The documentation exists to reduce onboarding time and provide visibility into transformation logic and lineage without requiring direct inspection of SQL files.

### How I created my DBT documentation

Documentation is generated using dbt docs generate, producing static artifacts that reflect the current state of models, tests, and metadata.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer2_dbt9t0u1v)

### Exploring my DBT documentation site

The generated documentation site presents model schemas, descriptions, and lineage graphs derived directly from the dbt project. This view supports system-level understanding of how data flows through transformations and where quality checks are applied, enabling easier maintenance and review.

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Data Engineering Foundation](./01-data-engineering-foundation.md) | [Data Engineering Optimization](./03-data-engineering-optimization.md) |
