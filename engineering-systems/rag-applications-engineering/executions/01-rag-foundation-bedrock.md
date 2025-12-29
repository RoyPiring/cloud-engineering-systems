# Set Up a RAG Chatbot in Bedrock

**Project Name:** ai-rag-bedrock  
**Author:** Roy Piring Jr

---

## Introducing Today’s Project!

This project implements a retrieval-augmented generation (RAG) chatbot using Amazon Bedrock. The system exists to ground model responses in external data by combining managed foundation models with a searchable knowledge base.

The implementation demonstrates knowledge base creation, document ingestion, and response generation using Bedrock-managed services. The result is a bounded chatbot whose answers are constrained by indexed source material rather than unconstrained model output.

---

## Tools and concepts

The system uses Amazon Bedrock for model orchestration, Amazon S3 for document storage, and Amazon OpenSearch Serverless as the vector store. Core concepts include RAG architecture, vector embeddings, semantic similarity search, data chunking, and knowledge base synchronization.

These components explicitly separate storage, retrieval, and inference responsibilities to reduce coupling and clarify system behavior.

---

## Project reflection

The primary challenge was validating knowledge base synchronization behavior. Correct configuration ensured that newly added or updated documents were reflected in retrieval results.

Testing confirmed that grounding materially improves relevance while constraining responses to indexed content.

---

## Understanding Amazon Bedrock

Amazon Bedrock provides managed access to foundation models and native support for RAG workflows. In this system, Bedrock coordinates retrieval from the knowledge base and response generation from the selected model.

The knowledge base uses Amazon S3 as the authoritative data source. S3 provides durable, low-cost storage and integrates directly with Bedrock ingestion workflows.

Training documents were uploaded to an S3 bucket in the same region as the knowledge base to minimize latency and simplify access patterns.

---

## My Knowledge Base Setup

The knowledge base uses a vector store to persist embeddings and support semantic search. When a query is issued, OpenSearch Serverless performs similarity matching to return the most relevant text chunks.

Embeddings encode semantic meaning into numerical vectors to enable efficient retrieval. Titan Text Embeddings v2 was selected to balance cost, latency, and retrieval quality for text-centric workloads.

Chunking splits source documents into fixed-size segments to improve recall and relevance. Chunks are capped at 500 characters to balance context density and retrieval precision.

---

## AI Models

Foundation models provide language understanding and response generation. Without them, the system would be limited to static retrieval results.

Model access was explicitly requested through the AWS console due to quota controls and cost considerations. This establishes governance over model usage and spend.

---

## Syncing the Knowledge Base

Synchronization ensures the knowledge base reflects the current state of the source data. It updates embeddings and maintains consistency between S3 content and the vector store.

The sync process includes ingestion of S3 objects, chunking and embedding of text, and storage of vectors in OpenSearch Serverless. Each phase is required to ensure accurate retrieval during inference.

---

## Testing My Chatbot

Initial testing used minimal input to validate the end-to-end flow, including retrieval and model invocation. A specific Bedrock model was selected for response generation.

Irrelevant responses to out-of-scope queries confirmed that the chatbot is constrained by the indexed knowledge base. This behavior validates that RAG limits model output to provided context.

Model selection was adjusted to compare response characteristics while keeping retrieval behavior constant.

---

## Upgrading My Chatbot

The number of source chunks returned during retrieval was increased to broaden context coverage. This improves answer completeness at the cost of additional retrieval overhead.

A custom generation prompt was added to constrain tone and response structure. Prompt tuning clarified expected output without altering retrieval mechanics.

Together, these adjustments improved relevance and consistency while preserving the bounded nature of the system.

---

## Navigation

| Next |
|------|
| [RAG CloudShell Implementation](./02-rag-cloudshell-implementation.md) |
