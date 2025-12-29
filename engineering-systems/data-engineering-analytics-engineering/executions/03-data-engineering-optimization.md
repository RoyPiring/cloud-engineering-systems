<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Data Engineering with Jupyter MCP

**Project Link:** [View Project](http://learn.nextwork.org/projects/mcp-data-engineer3)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer3_jup9j0k1l)

---

## Introducing Today's Project!

This project establishes an interactive analysis workflow using Jupyter notebooks connected to a PostgreSQL database through MCP. The system enables SQL-backed analysis from Python, basic visualization, and the promotion of exploratory queries into a dbt-managed transformation suitable for reuse and testing.

### Key tools and concepts

The implementation uses Jupyter for interactive execution, PostgreSQL as the data source, Matplotlib for basic visualization, Cursor as the MCP client, and dbt for managed transformations. The core concepts are database connectivity from Python, notebook-based analysis, visualization for inspection, and transitioning validated logic into a tested data model.

### Challenges and wins

The primary constraint was aligning dbt outputs with notebook-based queries so the same dataset could be validated and reused across tools. The work focused on ensuring dbt models executed correctly, tests passed, and results were queryable from the notebook without manual data duplication.

### Why I did this project

The project demonstrates a standard analytics flow where exploratory work in notebooks feeds into structured transformations. It validates how ad hoc analysis can be constrained, tested, and prepared for repeatable use through dbt without treating notebooks as a production system.

---

## Connecting Cursor to Jupyter

This section configures Cursor with an MCP server to communicate with Jupyter. The integration allows the notebook environment to issue database queries, render results, and remain synchronized with the local development tooling used to manage models and code.

PostgreSQL serves as the authoritative data store queried by the notebook. The connection enables analysis to operate on persisted datasets rather than static files, ensuring queries reflect the current database state and schema.

### Why Jupyter needs PostgreSQL

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer3_jup3d4e5f)

### Configuring the Jupyter MCP

The MCP configuration is added to Cursor and validated by restarting the client and confirming connectivity. This step ensures the notebook can execute database-backed operations and receive results without direct credential handling in the notebook itself.

---

## Building My First Notebook

The notebook is structured as an executable document that combines narrative context, dependency setup, and database queries. Its purpose is to provide a reproducible analysis surface rather than a long-lived service.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer3_jup6g7h8i)

### Three cells that tell a story

The notebook is intentionally minimal. One cell defines context, one prepares required libraries, and one executes a PostgreSQL query. This structure keeps the analysis readable while ensuring all execution dependencies are explicit and repeatable.

---

## Launching Jupyter Lab

Jupyter Lab is used to run queries, inspect results, and render visual output. The environment supports iterative analysis while remaining isolated from production pipelines.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer3_jup9j0k1l)

### Running my notebook

Visualization cells are added through Cursor and executed via Jupyter. The resulting bar chart summarizes customer acquisition by month, providing a quick inspection of temporal trends without asserting production-grade analytics or forecasting.

---

## Creating Data Visualizations

Query logic is promoted into a dbt model to formalize the transformation. The model is tested, materialized, and then queried back into Jupyter. This separates exploratory analysis from managed data transformations while keeping both connected.

### Verifying my work

The dbt project is validated using standard CLI commands to confirm dependencies, connectivity, model execution, and tests. Verification is performed directly against PostgreSQL to ensure the model behaves as expected outside the notebook.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/mcp-data-engineer3_jup1l2m3n)

### Notebook vs Production

The notebook functions as an exploratory and inspection tool optimized for rapid iteration. The dbt model represents a reusable, testable transformation intended for integration into data pipelines. The boundary between the two prevents notebooks from being treated as production infrastructure.

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Data Engineering Advanced](./02-data-engineering-advanced.md) | [Data Engineering Production](./04-data-engineering-production.md) |
