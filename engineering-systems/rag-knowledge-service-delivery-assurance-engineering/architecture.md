# Architecture: RAG Knowledge Service Delivery Assurance Engineering

## Quick Orientation

**Scope:** Production-ready RAG service delivery from API development through containerization, orchestration, and CI/CD automation, ensuring accurate, context-aware responses with operational reliability.

**Non-Goals:**
- Production-scale Kubernetes clusters
- Production-grade language models
- Advanced orchestration features
- Multi-region deployment
- Advanced monitoring and observability

**Key Tradeoffs:**
- **Development vs. Production:** Local development with TinyLLama vs. Production models (local for validation)
- **Containerization:** Docker for portability vs. Direct deployment (Docker for consistency)
- **Orchestration:** Kubernetes for reliability vs. Manual management (Kubernetes for self-healing)
- **Testing:** Semantic testing vs. Unit testing (semantic for behavior validation)
- **Determinism:** Mock LLM mode vs. Live LLM (mock for CI reliability)

**Diagram:** See [Architecture Patterns](#architecture-patterns) section below for visual representations.

---

## System Design

This system covers RAG service delivery assurance from API development through containerization, orchestration, and automated quality validation.

## Core Components

### 1. Application Layer
- FastAPI REST API framework
- Uvicorn ASGI server
- Python application logic and orchestration

### 2. Retrieval Layer
- Chroma vector database
- Vector embeddings for semantic search
- Knowledge base document storage

### 3. Generation Layer
- Ollama local language model platform
- TinyLLama lightweight model for development
- Mock LLM mode for deterministic testing

### 4. Infrastructure Layer
- Docker containerization
- Docker Hub container registry
- Kubernetes orchestration
- Minikube local cluster
- kubectl cluster management

### 5. Automation Layer
- GitHub Actions CI/CD
- Git version control
- Semantic testing framework

## Architecture Patterns

### Pattern 1: RAG Query Processing
```
User Query → FastAPI → Chroma Vector Search → Context Retrieval → Ollama LLM → Response
```

### Pattern 2: Containerization Flow
```
Local API → Dockerfile → Docker Image → Container Registry → Containerized Service
```

### Pattern 3: Kubernetes Deployment
```
Docker Image → Kubernetes Deployment → Pods → Kubernetes Service → NodePort → External Access
```

### Pattern 4: CI/CD Pipeline
```
Code Push → GitHub Actions → Semantic Tests → Mock LLM Mode → Validation → Pass/Fail
```

## Design Decisions

- **API Framework:** FastAPI for modern Python API development
- **Vector Database:** Chroma for local development and validation
- **Language Model:** Ollama with TinyLLama for local execution
- **Containerization:** Docker for portability and consistency
- **Orchestration:** Kubernetes for reliability and self-healing
- **CI/CD:** GitHub Actions for automated quality validation
- **Testing:** Semantic tests with mock LLM mode for determinism

---

## Failure Model

**What fails:** API endpoint failures, container build failures, pod failures, retrieval misses, generation timeouts, test failures

**How it fails:** API returns errors; Docker build fails; pods crash or become unavailable; retrieval returns no results; LLM generation times out; CI tests fail

**Blast Radius:** API failure affects that request; container failure affects deployment; pod failure affects that instance; retrieval miss affects that query; generation timeout affects that response; test failure blocks deployment

**Recovery:** API error handling with proper responses; Docker build retries; Kubernetes self-healing replaces failed pods; retrieval fallback handling; generation timeout handling; CI failure reporting with actionable feedback

## Security Model

**Trust Boundaries:** User boundary (untrusted queries); API boundary (local development); container boundary (isolated runtime); cluster boundary (Minikube local)

**Access Control:** Local development environment; container isolation; Kubernetes namespace isolation; Git repository access control

**Encryption:** TLS for API communications; container image security; secrets management in development

**Audit Trail:** Git commit history; CI/CD workflow logs; Kubernetes event logs; API request logging

## Cost Model

**Primary Drivers:** Local development environment (no cloud costs); Docker Hub registry (free tier); GitHub Actions (free tier for public repos); Minikube local cluster (no cloud costs)

**Guardrails:** Local development only; no production cloud resources; free-tier services where possible

**Expected Cost:** $0/month for local development and validation environment

## Constraints

**Policy:** Local development environment; Minikube for validation; no production cloud deployment

**Org:** Development-to-deployment pipeline; CI/CD automation; quality validation focus

**Technical:** Python, Ollama, Docker, Minikube required; local language model for development; mock LLM mode for CI

**Data Classification:** Knowledge base documents; no special compliance requirements; local development data

**Regions:** Local development environment; no multi-region considerations

## Quality Goals (Detailed)

1. **Response Accuracy** - How judged: API returns context-aware answers based on knowledge base retrieval; query responses reference authoritative source content; dynamic content addition updates knowledge base successfully

2. **Containerization** - How judged: Docker image builds successfully; containerized service runs identically to local version; image distributable via container registry

3. **Orchestration** - How judged: Kubernetes deployment maintains desired replica count; Service provides stable network endpoint; self-healing replaces failed pods automatically; external access validated through NodePort

4. **Quality Assurance** - How judged: CI pipeline executes semantic tests automatically; mock LLM mode enables deterministic test results; data quality regressions detected and reported; multi-document changes validated without service disruption

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |
