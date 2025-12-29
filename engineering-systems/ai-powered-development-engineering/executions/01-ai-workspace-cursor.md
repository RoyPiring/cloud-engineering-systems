<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Mini Spotify with Cursor

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-workspace-cursor)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Test a Mini Spotify with Cursor

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-cursor_s2q3upload)

---

## Introducing Today's Project!

This project evaluates the use of an AI-assisted editor to inspect an existing web application, modify its behavior, and introduce a new feature with minimal manual scaffolding. The scope focuses on understanding how AI tooling integrates into a standard local development workflow rather than on building a production-grade music service.

### Key tools and concepts

Cursor is used as an AI-assisted IDE to query and modify the codebase. Git and GitHub are used for source control and change tracking. The project exercises code comprehension, feature scaffolding, and documentation generation within an existing repository.

### Personal reflection

The intent is to assess whether AI-assisted coding can accelerate comprehension and small feature development without bypassing developer judgment. The project serves as a controlled environment to evaluate limits, friction points, and areas where human review remains necessary.

The work was completed within a short, fixed time window. The primary constraint was integrating AI-generated changes into an unfamiliar codebase while maintaining functional correctness. Success criteria were limited to local execution and observable behavior changes.

---

## Environment Setup

### Setting up my development environment

The environment consists of a local development workstation running Cursor, a cloned application repository, and a configured Cursor account. This establishes a standard local workflow where AI assistance operates alongside conventional tooling without altering the runtime environment.

### How Cursor differs from other AI coding tools

---

## Chatting with Cursor

### Exploring the codebase with Cursor

The application is inspected using AI-assisted queries to identify structure, dependencies, and runtime behavior. Dependencies are installed and the application is executed locally to confirm a working baseline before any modifications are introduced.

### The NextSound web app

The application is a client-side music web app that supports playlist creation and browsing. Any references to personalization or AI-driven recommendations are conceptual within the project context and are not validated against an external recommendation system.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-cursor_s2q3upload)

---

## Creating a Brand New Feature

A client-side playlist queue is introduced to control playback order within the application. The feature manages sequencing during a single user session and operates entirely within the existing frontend architecture. No backend services, persistence layer, or multi-user coordination are introduced.

### Designing the Queue feature

The queue is designed to provide deterministic control over track order while minimizing architectural impact. The UI exposes song metadata and supports add, reorder, and remove actions with immediate visual feedback. State changes are handled locally and integrated with existing playback controls. Persistence and cross-session continuity are explicitly excluded to avoid expanding scope beyond the current application boundaries.

### Troubleshooting with Cursor

AI-generated changes are reviewed and selectively modified to resolve state synchronization and UI update issues. Attention is given to preventing inconsistent queue behavior during rapid user interaction. Validation is performed through local execution and manual interaction to confirm functional correctness within the defined scope.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-cursor_s4q5upload)

---

## Automating with Commands

Commands are used to reduce manual overhead for repetitive, low-risk tasks within the development workflow. In this project, commands are applied to standardize documentation output and enforce consistent structure without altering application behavior. Their use is limited to developer productivity and does not affect runtime execution.

### What are Cursor commands?

Cursor commands are predefined AI-assisted actions executed within the editor. The /update-docs command is used to generate or update README files based on repository context. The command operates on existing files and metadata and does not introduce new system dependencies.

Commands automate discrete actions such as documentation generation and file updates. They are used where outcomes are deterministic and easily reviewable. All generated output is inspected before being committed to source control to ensure accuracy and alignment with project constraints.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-cursor_s4q1upload)

---

## Enforcing Standards with Rules

### What are Cursor rules?

Rules constrain AI behavior to enforce consistency across changes. In this project, rules are applied to maintain a consistent color palette and to control how chat interactions are initiated within the editor.

### Choosing rule application strategies

Rules configured as always-applied are used for deterministic updates such as formatting or metadata changes. Manually applied rules are reserved for changes that require human judgment, such as debugging or UI decisions.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-cursor_s4q1_5upload)

---

## Manage AI Context

### Controlling Cursor's context

AI context is controlled by defining which files and directories are visible to the editor during interactions. This constrains the information surface area available to the AI, reduces irrelevant references, and improves the determinism of suggested changes. Context management is treated as a configuration concern, not a runtime behavior.

### Performance and security benefits

Restricting context reduces unnecessary file scanning and limits cognitive noise in AI responses, resulting in more targeted suggestions. From a security and governance perspective, controlling visibility helps prevent unintended exposure of sensitive files and narrows what the AI can reference during code analysis. These controls affect editor behavior only and do not replace application-level security mechanisms.

### Comparing .cursorignore and .cursorindexingignore

The .cursorignore file removes specified paths entirely from AI visibility, preventing both indexing and reference. The .cursorindexingignore file excludes paths from the search index while keeping them visible in the repository and accessible for direct inspection. This separation allows precise control over AI context without modifying repository layout or build behavior.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-workspace-cursor_s6q4upload)

---

---

## Navigation

| Next |
|------|
| [AI Workspace Claude Code](./02-ai-workspace-claude-code.md) |
