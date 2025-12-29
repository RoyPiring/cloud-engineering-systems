# Architecture: RAG Applications Engineering

## Quick Orientation

**Scope:** Knowledge-grounded AI applications using Amazon Bedrock with document retrieval, including knowledge base setup, embedding model selection, retrieval strategy, and API integration.

**Non-Goals:**
- Custom embedding model training
- Advanced vector database architectures beyond Bedrock
- Multi-modal RAG (images, audio)
- Real-time streaming RAG responses

**Key Tradeoffs:**
- **Knowledge Base:** Bedrock Knowledge Base (managed, simpler) vs. Custom vector database (more control, higher complexity)
- **Embedding Model:** General-purpose (faster) vs. Domain-specific (more accurate)
- **Retrieval:** Top-K retrieval (simpler) vs. Reranking (more accurate, higher cost)
- **API Design:** Synchronous (simpler) vs. Asynchronous (better for long-running)

**Diagram:** See [Architecture Patterns](#architecture-patterns) section below for visual representations.

---

## System Design

This system covers Retrieval-Augmented Generation (RAG) implementations for building knowledge-grounded AI applications using Amazon Bedrock.

## Core Components

### 1. Knowledge Base
- Amazon Bedrock Knowledge Base
- Document storage (S3)
- Vector embeddings
- Semantic search capabilities

### 2. Embedding Model
- Embedding model selection
- Document chunking strategies
- Vector generation and storage
- Embedding optimization

### 3. Retrieval Strategy
- Semantic search configuration
- Retrieval parameter tuning
- Context window management
- Relevance ranking

### 4. Foundation Model Integration
- Amazon Bedrock foundation models
- Prompt engineering with context
- Response generation
- Cost optimization

### 5. Application Integration
- API design and implementation
- Web application integration
- Authentication and authorization
- Monitoring and observability

## Architecture Patterns

### Pattern 1: Bedrock Knowledge Base RAG
```
User Query → Bedrock → Knowledge Base → Vector Search → Context Retrieval → LLM → Response
```

### Pattern 2: Document Ingestion Flow
```
Documents → S3 → Bedrock Knowledge Base → Chunking → Embedding → Vector Store → Index
```

### Pattern 3: RAG Query Processing
```
Query → Embedding Generation → Semantic Search → Top-K Retrieval → Context Assembly → LLM Generation
```

### Pattern 4: API-Integrated RAG
```
Client → API Gateway → Lambda → Bedrock Knowledge Base → LLM → Formatted Response → Client
```

## Design Decisions

- Knowledge base selection (Bedrock vs. custom)
- Embedding model selection and tuning
- Retrieval configuration and optimization
- API design and integration patterns

---

## Failure Model

**What fails:** Knowledge base ingestion failures, embedding generation errors, retrieval misses, foundation model timeouts, context truncation, citation errors

**How it fails:** Document ingestion fails silently; embedding API returns errors; retrieval returns irrelevant documents; model timeout exceeds 30 seconds; context exceeds token limits; citations reference wrong documents

**Blast Radius:** Ingestion failure affects new documents only; embedding failure affects that document; retrieval miss affects that query; model timeout affects that generation; context truncation affects answer quality; citation error affects answer credibility

**Recovery:** Ingestion retries with error logging; embedding generation retries with exponential backoff; retrieval fallback to keyword search; model timeout handling with shorter context; context truncation with summarization; citation validation before response

## Security Model

**Trust Boundaries:** User boundary (untrusted queries); API boundary (authenticated requests); knowledge base boundary (document access control); foundation model boundary (managed service)

**IAM Model:** Least-privilege IAM roles for API access; Bedrock access limited to required models; S3 access scoped to knowledge base bucket; no cross-service over-privilege

**Encryption:** KMS encryption for knowledge base storage; TLS for all API communications; embeddings encrypted at rest; no sensitive data in logs; secrets in Secrets Manager

**Audit Trail:** CloudWatch Logs for all API calls (30-day retention); Bedrock usage logged; knowledge base access logged; S3 access logs; query and response metrics in CloudWatch; citation tracking

## Cost Model

**Primary Drivers:** Bedrock inference ($0.0008-0.008 per 1K input tokens + $0.0024-0.024 per 1K output tokens = ~$25/month), embedding generation ($0.0001 per 1K tokens = ~$5/month), S3 storage ($0.023/GB = ~$8/month), knowledge base processing ($0.10 per 1K characters = ~$5/month)

**Guardrails:** Budget alert at $55/month; Bedrock model selection optimized for cost; embedding generation batched; S3 storage limited to 50GB; knowledge base limited to 10K documents

**Expected Monthly Range:** $35-50/month for lab environment with moderate usage (1K-2K queries, standard document corpus, optimized model selection, standard storage)

## Constraints

**Policy:** Bedrock Knowledge Base only; no custom vector database; managed services preferred

**Org:** Team expertise in Bedrock and embeddings; no custom model training; basic retrieval patterns

**Cost Ceiling:** RAG infrastructure budget <$60/month for lab environment

**Latency:** Response generation must complete in <6 seconds p95; retrieval <1 second; embedding generation <2 seconds

**Data Classification:** Handles knowledge base documents; requires document access controls; no special compliance beyond standard encryption

**Regions:** Single region deployment (us-east-1 for Bedrock service availability)

## Quality Goals (Detailed)

1. **Response Accuracy** - How judged: Response accuracy >85% when relevant context retrieved (validated against ground truth); hallucination rate <15% (measured via citation verification); context relevance >80% (measured via retrieval ranking); answer completeness validated

2. **Retrieval Quality** - How judged: Top-K retrieval finds relevant documents >80% of the time; embedding similarity scores >0.7 for relevant matches; retrieval latency <500ms; knowledge base coverage validated

3. **Cost Efficiency** - How judged: Inference costs <$30/month for moderate usage; embedding generation costs <$10/month; storage costs <$10/month; total RAG infrastructure <$50/month; cost per query <$0.05

4. **Performance** - How judged: End-to-end response time <5 seconds p95 (retrieval + generation); embedding generation <1 second; retrieval <500ms; generation <3 seconds; total latency <5000ms

5. **Scalability** - How judged: Knowledge base handles 10x document growth; retrieval performance maintained with larger corpus; embedding storage scales linearly; concurrent queries supported

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |

