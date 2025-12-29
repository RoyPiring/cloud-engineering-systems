# How I Built an API for My RAG Chatbot

**Project Name:** ai-rag-api  
**Author:** Roy Piring Jr

---

## Introducing Today’s Project!

This project implements a retrieval-augmented generation (RAG) chatbot backed by Amazon Bedrock and exposed through a custom API. The system exists to demonstrate how external knowledge can be retrieved from object storage and combined with foundation model inference to produce grounded responses.

The implementation focuses on configuring Amazon Bedrock, integrating a managed knowledge source, and exposing model access through a lightweight API layer. The result is a callable interface that cleanly separates retrieval, inference, and client access concerns.

---

## Tools and concepts

The system uses Amazon Bedrock for foundation model inference and Amazon S3 as the authoritative storage layer for knowledge documents. A Python-based API layer built with FastAPI exposes the chatbot functionality.

Supporting tooling includes the AWS CLI and SDKs for service configuration and access, along with vector indexing libraries to enable similarity-based retrieval. These components form a basic RAG architecture where storage, retrieval, inference, and API access are explicitly decoupled.

---

## Project reflection

The primary integration challenge was configuring environment variables and credentials required for Amazon Bedrock access. Resolving these issues validated secure communication between the API runtime and the managed model service.

The resulting system confirms that chatbot responses can be grounded in a custom knowledge base rather than relying exclusively on general-purpose model output.

---

## Setting Up The Knowledge Base

Amazon S3 serves as the source of truth for documents that populate the chatbot knowledge base. These documents include domain-specific reference material such as FAQs, product documentation, and internal notes.

A Bedrock knowledge base is configured to index these documents and make them available for retrieval during inference. This constrains responses to provided content and reduces ungrounded generation.

Distinct models are used for embedding generation and text generation. Configuration ensures compatibility between embedding outputs and retrieval queries to maintain consistent and accurate retrieval behavior.

---

## Running Bedrock Commands

Initial Bedrock CLI commands failed due to missing configuration values required for authentication and model invocation, including region and model identifiers.

After supplying the required parameters, command execution returned valid responses. This confirmed successful connectivity between the local environment and the Bedrock service.

---

## Creating an API

The API layer is implemented in Python using FastAPI to provide a structured interface for chatbot queries. This layer decouples client access from direct interaction with Bedrock services.

The API integrates with Bedrock through the AWS SDK and retrieval libraries, enabling user queries to flow through the RAG pipeline before inference.

The application entry point defines routing and request handling logic. Dependencies are pinned to ensure reproducible runtime behavior, and sensitive configuration values are externalized rather than embedded in source code.

---

## Installing Packages

The API runtime executes as a continuously running service, enabling immediate availability of endpoints during development and testing.

Dependency installation ensures the environment supports vector retrieval, model invocation, and HTTP request handling without requiring manual restarts during iteration.

---

## Testing the API

The root endpoint was accessed successfully, confirming that the FastAPI application initialized correctly and was reachable by clients.

This step establishes baseline service availability before invoking model-backed endpoints.

---

## The Query Endpoint

The query endpoint accepts user input and routes it through the retrieval and inference pipeline to generate responses grounded in the knowledge base.

Environment variables supply credentials, region configuration, and model identifiers required for Bedrock access. Initial misconfiguration of these values caused request failures.

After correcting the environment configuration, the endpoint returned valid responses, confirming correct integration between the API layer and Bedrock services.

---

## Extending the API

The API was extended to include authentication controls, improved error handling, and additional endpoints. These changes introduce clearer separation between secured and unsecured access paths.

Two distinct endpoints were implemented: one that performs RAG-based queries against the knowledge base, and another that invokes the model directly without retrieval context. This separation clarifies system behavior and limits unintended knowledge exposure.

Configuration errors related to missing environment variables initially prevented successful execution. Once resolved, endpoint validation confirmed stable operation and correct behavior.

---

## Navigation

| Previous | Next |
|----------|------|
| [RAG CloudShell Implementation](./02-rag-cloudshell-implementation.md) | [RAG Complete Webapp](./04-rag-complete-webapp.md) |
