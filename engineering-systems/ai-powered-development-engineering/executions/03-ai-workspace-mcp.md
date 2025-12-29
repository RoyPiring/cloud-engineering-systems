<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Database With Cursor and Supabase MCP

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-workspace-mcp)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-mcp_s5s3q3)

---

## Introducing this project!

This project implements a basic interaction datastore for NextSound, a platform feature that records user likes on tracks. The system integrates a hosted PostgreSQL database with an AI-assisted development environment to persist and update like counts. The objective is to demonstrate a minimal interaction model that supports stateful user actions without embedding database logic directly in application code.

### Key tools and concepts

The system uses Cursor connected to a Supabase-managed database through an MCP interface to perform schema creation and data updates. MCP serves as the control plane that allows the editor to issue structured database operations. Environment variables are used to scope credentials and endpoints. The design centers on reducing manual query writing while maintaining explicit control over schema and data integrity.

### Project completion time

The implementation was completed in approximately 90 minutes. Most effort was spent validating MCP connectivity and confirming that database mutations issued through the editor were correctly reflected in Supabase. The outcome is a working baseline that can be extended with additional interaction tables without reworking the connection model.

---

## Setting up Cursor and MCPs

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-mcp_s1q4img)

### Why MCPs?

MCP provides a mechanism for AI-assisted tools to access external systems with context and constraint awareness. In this project, MCP acts as the boundary between the editor and the database, allowing controlled read and write operations without exposing raw credentials in prompts.

Cursor was connected to the Supabase project and verified by observing live table creation and data population. The MCP connection enables Cursor to issue deterministic database operations, such as incrementing like counters, while Supabase enforces schema and access rules.

---

## Building with Cursor

### How Cursor set up the database

Cursor issued tool-based commands through MCP to create the initial database structure. This included provisioning a Supabase project and defining a table used to persist track like data. All schema changes were executed against the live database rather than simulated locally.

### Understanding .env files

The .env file stores Supabase connection details, including the project URL and API key, and is consumed by Cursor during MCP operations. This isolates secrets from source files and limits accidental disclosure. Proper use of environment variables ensures the database can be accessed securely while maintaining least-privilege principles.

### Implementing the likes feature

The likes feature persists user interactions by writing to a dedicated table rather than storing state in application memory. Cursor was used to define the table schema, including identifiers for tracks and users and a field for like counts.

This structure supports idempotent updates and avoids duplicate records per user-track pair.

---

## Testing the Likes Feature

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-mcp_s4q4img)

### How likes connect to the database

When a user clicks the heart icon, the application triggers a database update that increments the like count for the associated track. This operation results in an update to the corresponding row in the Supabase table, confirming that frontend actions are correctly mapped to persistent state changes.

### Data in the track_likes table

The track_likes table stores track identifiers, user identifiers, and the associated like count. Each row represents a user interaction with a track. Database connectivity was validated by confirming that records appeared and updated in Supabase following user actions.

The current focus is limited to incrementing like counts. The schema is intentionally narrow to validate interaction flow before expansion. Future extensions would require additional tables and relationships to capture comments, shares, and listening history, enabling analytics and recommendation logic without overloading the initial design.

---

## Querying with Natural Language

### MCP tools used

Cursor used the Supabase MCP to create and populate the track_likes table. Sample data was inserted to confirm read and write paths. This demonstrated that natural language instructions issued in the editor were translated into concrete database operations through MCP.

### Natural language vs SQL

---

## Updating Votes with Cursor

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-mcp_s5s3q3)

### How Cursor updated the votes

Cursor was used to issue update operations that incremented like counts in the track_likes table. Correct behavior was verified by observing consistent count increases in Supabase after each user interaction.

### Verifying the update

Natural language-driven updates reduce the need for repetitive query authoring while still producing explicit database mutations. This approach is suited for routine updates, low-complexity data entry, and rapid iteration scenarios where schema and access boundaries are already defined.

---

## Secret Mission: User Authentication

### What we're building

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-mcp_z1x0c9v8)

### user_profiles vs user_track_likes

The user_profiles table stores user-level attributes, while the user_track_likes table records interactions between users and tracks. Separating profile data from interaction data avoids coupling identity management with engagement metrics.

### Linking users to tracks

Track and user identifiers are used as foreign keys to associate users with their liked tracks. This relationship enables downstream features such as displaying liked tracks and generating personalized recommendations without duplicating user data.

---

## Querying User Data

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-mcp_f9d8s7a6)

### Benefits of natural language querying

User data introduces additional security considerations, particularly when storing identifiers such as email addresses. Strong encryption and regulatory compliance are required. Supabase service limits, including monthly active user caps and resource quotas, must be considered when designing query patterns and growth expectations.

### Other questions to explore

What are the current like counts for each track?
How many users have liked a specific track?
Which tracks has a given user liked?
What is the average number of likes per track?
Can the like count for a specific user-track pair be updated deterministically?

---

---

## Navigation

| Previous |
|----------|
| [AI Workspace Claude Code](./02-ai-workspace-claude-code.md) |
