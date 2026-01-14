# Validation: RAG Knowledge Service Delivery Assurance Engineering

## Purpose

This document provides **objective validation evidence** that the RAG knowledge service delivery assurance system behaves exactly as designed.

It records:
- What was tested
- What was expected
- What was observed
- Where the evidence exists

No rationale.  
No architecture explanation.  
No implementation detail.

---

## Validation Summary

| Domain | Status | Primary Evidence |
|--------|--------|------------------|
| API Development | PASS | ./executions/01-ai-devops-api.md |
| Containerization | PASS | ./executions/02-ai-devops-docker.md |
| Kubernetes Orchestration | PASS | ./executions/03-ai-devops-kubernetes.md |
| CI/CD Automation | PASS | ./executions/04-ai-devops-githubactions.md |

---

## Validation Scope

Validation covers:

- RAG API development with FastAPI, Chroma, and Ollama
- Docker containerization
- Kubernetes orchestration
- CI/CD automation with semantic testing

---

## API Development

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Python and Ollama setup | Python version confirmed, Ollama installed with TinyLLama model ready | Python was installed and verified locally; Ollama was configured with the tinyllama model | ./executions/01-ai-devops-api.md |
| Virtual environment and dependencies | Virtual environment created and activated, FastAPI, Chroma, Uvicorn, Ollama installed | A virtual environment was created using the standard Python venv module; FastAPI, Chroma, Uvicorn, and Ollama packages were installed | ./executions/01-ai-devops-api.md |
| Knowledge base embeddings | Content converted to vector embeddings, stored in Chroma database | Embeddings were generated using a pre-trained model and stored in a Chroma database; the database stores both the embeddings and their associated text | ./executions/01-ai-devops-api.md |
| Query endpoint response | POST to `/query` with question returns context-aware answer based on knowledge base | A POST request was sent to the /query endpoint with the question "What is Kubernetes?"; the response correctly defined Kubernetes as an open-source system, confirming end-to-end functionality | ./executions/01-ai-devops-api.md |
| Dynamic content addition | POST to `/add` endpoint accepts new content, generates embeddings, stores in Chroma | A new /add POST endpoint was implemented to accept additional content; this endpoint generates embeddings for the new data and stores them in the Chroma database | ./executions/01-ai-devops-api.md |

---

## Containerization

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Docker installation | Docker Desktop installed, `docker run hello-world` executes successfully | Docker was verified by running the docker run hello-world command; this command pulls and executes a simple test container, confirming that Docker is installed and functioning correctly | ./executions/02-ai-devops-docker.md |
| Dockerfile build | Docker image builds successfully, contains application code and dependencies | A Dockerfile was created to define the runtime environment for the RAG API container; the image build was verified using docker images to confirm its presence and metadata | ./executions/02-ai-devops-docker.md |
| Containerized API behavior | Containerized API functions identically to local version, responses match | After containerization, the API was tested and confirmed to function identically to the local version; query responses, performance, and behavior remained consistent | ./executions/02-ai-devops-docker.md |
| Docker Hub push | Image pushed to Docker Hub, can be pulled and run on other systems | The image was pushed to Docker Hub by authenticating with docker login, tagging the local image with the appropriate repository name, and executing docker push | ./executions/02-ai-devops-docker.md |

---

## Kubernetes Orchestration

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Cluster availability | Minikube cluster running, `minikube status` shows running state | The Kubernetes cluster is started using minikube start; cluster health was verified using minikube status, confirming that the cluster was running and ready to accept workloads | ./executions/03-ai-devops-kubernetes.md |
| Image loading | Docker image loaded into Minikube, available for pod creation | After starting Minikube, the Docker image was loaded into the cluster using minikube image load; the node status was verified using kubectl get nodes, which showed the node in a Ready state | ./executions/03-ai-devops-kubernetes.md |
| Deployment creation | Deployment created, pod in Running state, READY 1/1 | The RAG API is deployed using a Kubernetes Deployment; running kubectl get pods showed the RAG API pod in a Running state; the READY value of 1/1 confirmed that the container inside the pod was healthy and ready to serve traffic | ./executions/03-ai-devops-kubernetes.md |
| Service exposure | Service created, provides stable endpoint routing to pods | A Kubernetes Service is created to expose the RAG API; the Service was created using kubectl apply -f service.yaml; its status was verified using kubectl get services, confirming that the Service was active and accessible within the cluster | ./executions/03-ai-devops-kubernetes.md |
| External API access | API accessible through NodePort, returns valid JSON responses | The API was accessed using a curl request targeting the Minikube service IP and NodePort; the response returned a valid JSON payload, confirming that the API was running and reachable through Kubernetes | ./executions/03-ai-devops-kubernetes.md |
| Self-healing behavior | Deleted pod automatically replaced, Service routes traffic to new pod | When the pod was deleted, Kubernetes immediately created a replacement pod to satisfy the Deployment's desired state; the Service automatically routed traffic to the new pod because it selects pods based on labels | ./executions/03-ai-devops-kubernetes.md |

---

## CI/CD Automation

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Git repository initialization | Git initialized, files committed, repository pushed to GitHub | Git was initialized using git init, creating a local repository; files were staged with git add . and committed using git commit -m "Initial commit"; pushing the repository to GitHub makes the code available for automated workflows | ./executions/04-ai-devops-githubactions.md |
| Semantic test execution | Semantic tests validate RAG API behavior from user perspective | Semantic tests validate the overall behavior of the RAG API rather than individual functions; these tests ensure the system retrieves relevant context and produces meaningful responses | ./executions/04-ai-devops-githubactions.md |
| Mock LLM mode determinism | Mock mode returns consistent predefined outputs, eliminates variability | Mock LLM mode is introduced to simulate LLM behavior without external API calls; instead of generating responses dynamically, the system returns consistent, predefined outputs; this eliminates variability and allows semantic tests to be deterministic and repeatable | ./executions/04-ai-devops-githubactions.md |
| GitHub Actions workflow trigger | Workflow runs automatically on code push, executes semantic tests | A GitHub Actions workflow is created to automatically run semantic tests whenever code is pushed to the repository; the workflow file, main.yml, is created and committed to the repository; once pushed, GitHub automatically runs the workflow on every change to the main branch | ./executions/04-ai-devops-githubactions.md |
| Data quality detection | CI pipeline fails when flawed data introduced, detects semantic regressions | The CI workflow is intentionally triggered with flawed data to validate that automated semantic testing correctly detects semantic regressions; the missing keyword was "orchestration"; the semantic test failed because the RAG API returned an irrelevant response due to the flawed data | ./executions/04-ai-devops-githubactions.md |
| Multi-document scaling | CI validates full document set, detects no regressions after structural changes | The project is restructured to support increased complexity and long-term maintainability; CI validated the full document set and detected no regressions, confirming that the RAG API continued to retrieve accurate information after structural changes | ./executions/04-ai-devops-githubactions.md |

---

## Evidence Map to Executions

| Validation Check | Execution File | Section Reference |
|-----------------|----------------|-------------------|
| Python/Ollama Setup | `./executions/01-ai-devops-api.md` | "Setting Up Python and Ollama" |
| Dependencies Installed | `./executions/01-ai-devops-api.md` | "Setting Up a Python Workspace" |
| Embeddings Created | `./executions/01-ai-devops-api.md` | "Setting Up a Knowledge Base" |
| Query Endpoint Working | `./executions/01-ai-devops-api.md` | "Testing the RAG API" |
| Dynamic Content Addition | `./executions/01-ai-devops-api.md` | "Adding Dynamic Content" |
| Docker Verified | `./executions/02-ai-devops-docker.md` | "Installing Docker Desktop" |
| Dockerfile Created | `./executions/02-ai-devops-docker.md` | "Creating the Dockerfile" |
| Containerized API Tested | `./executions/02-ai-devops-docker.md` | "Building and Running the Container" |
| Docker Hub Push | `./executions/02-ai-devops-docker.md` | "Pushing to Docker Hub" |
| Cluster Running | `./executions/03-ai-devops-kubernetes.md` | "Starting My Kubernetes Cluster" |
| Image Loaded | `./executions/03-ai-devops-kubernetes.md` | "Loading the Docker image into Minikube" |
| Deployment Created | `./executions/03-ai-devops-kubernetes.md` | "Deploying to Kubernetes" |
| Service Created | `./executions/03-ai-devops-kubernetes.md` | "Creating a Service" |
| External Access | `./executions/03-ai-devops-kubernetes.md` | "Accessing My API Through Kubernetes" |
| Self-Healing Verified | `./executions/03-ai-devops-kubernetes.md` | "Testing Self-Healing" |
| Git Initialized | `./executions/04-ai-devops-githubactions.md` | "Initializing Git and Pushing to GitHub" |
| Semantic Tests Created | `./executions/04-ai-devops-githubactions.md` | "Creating Semantic Tests" |
| Mock Mode Implemented | `./executions/04-ai-devops-githubactions.md` | "Adding Mock LLM Mode" |
| Workflow Created | `./executions/04-ai-devops-githubactions.md` | "Creating GitHub Actions Workflow" |
| Data Quality Detected | `./executions/04-ai-devops-githubactions.md` | "Testing Data Quality" |
| Multi-Document Validated | `./executions/04-ai-devops-githubactions.md` | "Scaling with Multiple Documents" |

---

## Known Limitations

- Validation performed in local development environment
- Minikube cluster used for orchestration validation (not production-scale)
- TinyLLama model used for development (not production-grade)
- Manual testing used in addition to automated CI validation
- Performance metrics not captured in detail

---

## Relationship to Other Documents

- **Business Requirements:** `business-context.md`
- **Design Intent:** `architecture.md`
- **Execution Record:** `implementation.md`

This document provides proof. Nothing more.

---

## Navigation

| Previous | Next |
|----------|------|
| [Implementation](./implementation.md) | [README](./README.md) |
