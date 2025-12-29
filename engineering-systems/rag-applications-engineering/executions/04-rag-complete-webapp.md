# Building a RAG Chatbot with a Web Interface

**Project Name:** ai-rag-webapp  
**Author:** Roy Piring Jr

---

## Introducing Today’s Project!

This project implements a web application that provides interactive access to a retrieval-augmented generation (RAG) chatbot. The system exists to expose Bedrock-backed retrieval and inference through a browser-based interface rather than a terminal or direct API client.

The implementation integrates a web framework with Amazon Bedrock and IAM-scoped credentials to enable user-driven queries against one or more knowledge bases. The result is a functional web surface that mediates access to grounded model responses.

---

## Tools and concepts

The system uses Amazon Bedrock for inference, Amazon S3 for knowledge base storage, and AWS IAM for access control. FastAPI provides the application layer for routing and request handling.

These components establish clear boundaries between identity, retrieval, inference, and presentation, reducing coupling between the web layer and Bedrock services.

---

## Project reflection

The primary challenge was troubleshooting API endpoints and resolving missing or incorrect AWS environment variables. Correct configuration enabled stable authentication and consistent request handling.

Successful execution confirmed that the web interface can reliably invoke the same RAG pipeline used in non-UI contexts.

---

## Chatbot setup

A Bedrock Knowledge Base was created to provide structured access to reference data. This enables consistent retrieval behavior and constrains chatbot responses to indexed content.

The knowledge base improves response accuracy and reduces ambiguity by ensuring answers are derived from approved source material.

---

## Setting Up the API

The API layer installs and configures required runtime dependencies to support HTTP request handling and multipart form processing.

A virtual environment isolates dependencies to ensure repeatable behavior and avoid version conflicts. This isolation maintains consistency across local development and execution contexts.

---

## Breaking down the API

The API acts as the control plane between the web interface and the RAG backend. It handles request validation, routing, and translation of user input into Bedrock-compatible calls.

Sensitive configuration values are supplied through environment variables rather than source code. This limits credential exposure and simplifies rotation.

The API uses the AWS SDK to interact with Bedrock programmatically, enabling automated request handling.

Two primary routes define the supported interaction patterns and serve as stable entry points for the web application.

---

## Testing the API

Accessing the root endpoint returned the expected welcome response, confirming that routing and application initialization completed successfully.

This validation establishes baseline API availability before invoking Bedrock-backed functionality.

---

## Troubleshooting the API

Errors on secondary endpoints were traced to missing or misconfigured AWS environment variables. These variables are required for authentication and regional routing.

Setting the required credentials and region variables resolved request failures and enabled secure access to Bedrock resources.

---

## Running the Web App

The API provides the backend communication layer, while the web application presents a real-time interface for user interaction.

The web application supports switching between multiple knowledge bases. Identical queries routed to different bases produced context-specific responses, confirming correct retrieval behavior.

---

## Breaking down the Web App

User input submitted through the web interface is forwarded to the API layer. The API invokes Bedrock through the AWS SDK, processes the response, and returns structured output.

The web layer renders responses without embedding Bedrock logic directly, maintaining a clean separation between presentation and inference.

---

## Customizing the Frontend

Frontend customization modifies presentation without changing API behavior. Requests continue to target the same endpoints and retrieval logic.

Interface changes focused on layout, navigation clarity, and user guidance while preserving functional correctness and backend compatibility.

---

## Navigation

| Previous |
|----------|
| [RAG API Integration](./03-rag-api-integration.md) |
