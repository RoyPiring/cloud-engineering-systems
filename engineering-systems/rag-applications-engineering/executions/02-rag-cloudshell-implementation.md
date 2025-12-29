# Interacting With My RAG Chatbot in the Terminal

**Project Name:** ai-rag-cloudshell  
**Author:** Roy Piring Jr

---

## Introducing Today’s Project!

This project implements a command-line interface for interacting with a retrieval-augmented generation (RAG) chatbot using Amazon Bedrock. The system exists to validate that knowledge-base-backed inference can be invoked directly from a terminal without relying on a web or API layer.

The implementation demonstrates three core concerns: storing reference data in Amazon S3, configuring a Bedrock Knowledge Base for retrieval, and selecting Bedrock foundation models for response generation. The result is a scriptable and repeatable workflow for grounded model interaction via the AWS CLI.

---

## Tools and concepts

The system uses Amazon S3 for document storage, Amazon Bedrock for retrieval and inference, and the AWS CLI executed within CloudShell. Core concepts include IAM-scoped access, CloudShell execution context, Bedrock Knowledge Bases, and explicit model selection for controlled inference.

These components enable direct, low-friction interaction with the RAG pipeline while maintaining separation between data storage, retrieval, and response generation.

---

## Project reflection

The primary challenge was identifying and supplying required identifiers for region, model, and knowledge base configuration. Correctly providing these values resolved command failures and enabled successful retrieval and response generation.

The resulting workflow confirms that terminal-based interactions can retrieve grounded responses with the same constraints enforced by console-driven Bedrock usage.

This project focuses on automation-friendly access paths for AI systems rather than interactive user interfaces.

---

## Setting Up The Knowledge Base

Amazon S3 serves as the authoritative data store for documents referenced by the knowledge base. Stored content includes material related to Amazon S3, Amazon Bedrock, and AWS IAM.

A Bedrock Knowledge Base is configured to index this data and enable semantic retrieval. This ensures that terminal queries return responses grounded in the indexed S3 content.

Multiple models are configured to support retrieval and response generation. The knowledge base is synchronized to ensure embeddings reflect the current state of stored documents.

---

## Running CLI Commands in CloudShell

CloudShell provides a managed Linux environment with the AWS CLI preconfigured for the active account. This environment serves as the execution context for all terminal-based interactions.

Initial Bedrock CLI commands failed due to missing required parameters, including region, model ID, and knowledge base ID. These identifiers are mandatory for scoped Bedrock operations.

The AWS CLI provides a scriptable interface suitable for automation and repeatable execution, making it appropriate for validating RAG behavior outside of graphical interfaces.

---

## Running Bedrock Commands

Required identifiers were sourced from project configuration and AWS documentation. Once supplied, the Bedrock command executed successfully and returned a sample chatbot interaction.

The response demonstrated retrieval of information from the knowledge base related to Amazon S3, Amazon Bedrock, and AWS IAM, confirming correct end-to-end integration.

The default retrieve-and-generate output includes verbose metadata. Applying the `--query-only` flag constrained output to generated content for improved terminal readability.

---

## Extending Your Knowledge Base

A query related to Bedrock pricing revealed gaps in the indexed data, highlighting that retrieval accuracy is bounded by document coverage and freshness.

Additional documents were uploaded to Amazon S3 and the knowledge base was synchronized. The command-line workflow enabled faster iteration compared to console-based updates.

A subsequent Bedrock command validated the update, confirming that the new content was indexed and retrievable.

---

## Interacting with AI Models Directly

Direct model invocation was performed from CloudShell using Bedrock CLI commands. Required parameters for region, model ID, and knowledge base ID were explicitly supplied.

This interaction confirmed that foundation models can be invoked both with and without retrieval context, depending on command configuration. The result validates controlled access to grounded and ungrounded inference paths directly from the terminal.

---

## Navigation

| Previous | Next |
|----------|------|
| [RAG Foundation Bedrock](./01-rag-foundation-bedrock.md) | [RAG API Integration](./03-rag-api-integration.md) |
