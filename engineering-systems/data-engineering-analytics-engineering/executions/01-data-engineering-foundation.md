<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Data Engineering with Postgres & Docker MCP

**Project Link:** [View Project](http://learn.nextwork.org/projects/mcp-data-engineer1)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer1_er-diagram-screenshot)

---

## Introducing Today's Project!

This project provisions a PostgreSQL database inside a Docker container and exposes it for local interaction through MCP-enabled tooling. The system supports loading a non-trivial dataset of over 40,000 rows, executing analytical queries, visualizing schema relationships, and applying targeted performance optimizations. PostgreSQL provides transactional consistency and SQL compliance. Docker isolates the database runtime to ensure repeatable behavior across environments.

### Key tools and concepts

Docker Desktop is used to run and manage containers locally. PostgreSQL serves as the relational database engine. uv initializes and manages the Python project used to interact with the database. Cursor with MCP provides database inspection and query execution. Core concepts include container isolation, database access control, query performance analysis, and basic Python project structure for database interaction.

### Challenges and wins

The primary constraint was aligning local tooling versions to ensure Docker, uv, and MCP integration worked without conflicts. The most material outcome was validating that query performance issues could be identified and corrected through indexing, with measurable changes in execution plans.

### Why I did this project

This project exists to demonstrate a controlled, reproducible approach to standing up a relational database in a containerized environment and validating its behavior under realistic data volume. It focuses on understanding schema design, access boundaries, and the impact of query structure on performance.

---

## Setting Up Docker and UV

The environment establishes Docker Desktop as the container runtime and uv as the Python package manager. Docker ensures the PostgreSQL instance runs consistently regardless of host configuration. uv provides a minimal, deterministic Python project setup to support database interaction scripts.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer1_8h9i0j1k)

### What's Docker and why containers?

Containers encapsulate the database and its dependencies to remove host-level variability. This approach simplifies teardown and rebuild, supports repeatable testing, and mirrors how databases are commonly deployed in controlled non-production environments.

### Verifying installations

Docker and uv installations are validated by confirming expected version output and successful startup. This step ensures the container runtime and Python tooling are functional before provisioning database resources.

---

## Connecting MCP Servers

MCP servers are installed and configured to allow the editor to communicate with Docker and PostgreSQL. The Python project is initialized with uv to provide a structured entry point for database interaction. Cursor is restarted to apply MCP configuration changes.

### Python project setup

The uv init command creates a minimal Python project scaffold. The generated files define project metadata, dependency management boundaries, version control exclusions, and a single entry point for executing database-related code.

### Installing Docker MCP

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer1_mcp-config-screenshot)

---

## Building My Database

A PostgreSQL container is created using Docker through MCP integration. Database users are configured using PostgreSQL MCP tooling. The system is prepared to accept schema definitions and demo data for validation and analysis.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer1_postgres-container-screenshot)

### Database security

An application-scoped database user is created with restricted privileges. Administrative access remains limited to the default superuser. This separation enforces least privilege by constraining application access to only required operations, reducing blast radius in the event of credential compromise.

### Loading demo data

Demo data is introduced by copying and executing a SQL file inside the container. The file defines schema objects and inserts sample records to simulate a realistic workload for querying and performance analysis.

### Verifying and visualizing the database

Database state is validated by inspecting schemas and sample data through Cursor. An entity relationship diagram is generated to confirm table structures and foreign key relationships, including links between product and order data.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer1_er-diagram-screenshot)

---

## Performance Audit

A performance audit is conducted to identify inefficient queries and access patterns. The goal is to surface bottlenecks that would degrade response time or increase resource consumption under load.

### Audit findings

Query execution plans are analyzed using EXPLAIN ANALYZE. Results indicate full table scans on frequently filtered columns. Recommendations focus on indexing and query refinement to align access paths with expected usage patterns.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer1_performance-screenshot)

### Performance gains

An index is added to a commonly filtered column. Subsequent execution plans show a shift from sequential scans to index scans, reducing query execution time and improving overall query efficiency.

---

---

## Navigation

| Next |
|------|
| [Data Engineering Advanced](./02-data-engineering-advanced.md) |
