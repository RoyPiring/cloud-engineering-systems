<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a RAG API with FastAPI

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-devops-api)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-api_g3h4i5j6)

---

## Introducing Today's Project!

This project demonstrates how to build a Retrieval-Augmented Generation (RAG) API using FastAPI to answer user questions based on a supplied set of files. The goal is to design a working AI system that combines retrieval and generation into a single, reusable service rather than a conceptual example.

The focus is on understanding how RAG systems function end to end, strengthening Python and FastAPI skills, and producing a practical API that can be extended or adapted for real-world use.

### Key services and concepts

The services used in this project are Python, FastAPI, Chroma, Uvicorn, and Ollama.

Python provides the application logic and orchestration layer. FastAPI is used to expose the AI system through a clean and well-defined API. Chroma serves as the vector database that enables semantic search over the knowledge base. Uvicorn runs the application as an ASGI service. Ollama allows the system to run a local language model without relying on external cloud services.

Key concepts explored include Retrieval-Augmented Generation (RAG), vector embeddings, semantic search, API-based AI system design, and local LLM execution.

### Challenges and wins

This project took approximately two hours to complete. The primary challenge was configuring the Python virtual environment and ensuring that all dependencies were installed correctly and compatible with one another.

The most rewarding outcome was observing the API consistently return accurate, context-aware answers based on the knowledge base. This confirmed that the retrieval pipeline and the local language model were functioning correctly together.

### Why I did this project

I completed this project to gain hands-on experience building a RAG system from the ground up rather than relying on managed or abstracted solutions. The objective was to understand how retrieval, embeddings, and generation interact at runtime.

By building this API, I expanded my practical experience with Python, FastAPI, vector databases, and local LLMs while producing a functional system that demonstrates how RAG improves response accuracy through grounded context.

---

## Setting Up Python and Ollama

Python is a flexible and widely supported language with strong AI and API ecosystems, making it well suited for this project. Ollama is an open-source platform that simplifies running local language models, enabling experimentation without cloud costs.

These tools are required because Python and FastAPI form the API foundation, while Ollama provides the local generative model used to process retrieved context and produce responses.

Python and Ollama setup

Python was installed and verified locally to ensure compatibility with FastAPI and supporting libraries. Ollama was installed to manage and run local language models required by the RAG system.

Verifying Python is working

Python was validated by confirming the installed version and successfully executing test commands. This step ensures the runtime environment is stable before introducing additional dependencies.

### Python and Ollama setup

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-api_i9j0k1l2)

### Verifying Python is working

### Ollama and tinyllama ready

Ollama was configured with the tinyllama model. This model was selected because it is lightweight, efficient, and well suited for local experimentation. While not intended for production-scale workloads, it is sufficient for validating RAG behavior and understanding how retrieved context influences generated responses.

---

## Setting Up a Python Workspace

A dedicated project directory was created to organize application code, configuration files, and supporting scripts. This structure improves maintainability and clarity as the project evolves.

### Python workspace setup

### Virtual environment

A virtual environment isolates project dependencies from the system Python installation. This prevents version conflicts and allows precise control over installed packages.

The environment was created using the standard Python venv module and activated before installing any dependencies.

### Dependencies

The following packages were installed for this project: FastAPI, Chroma, Uvicorn, and Ollama.

FastAPI is used to build the API layer. Chroma manages vector embeddings and similarity search. Uvicorn serves the application. Ollama runs the local language model used for generation.

Each dependency has a specific role and was chosen to keep the system simple and understandable.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-api_u1v2w3x4)

---

## Setting Up a Knowledge Base

In this step, a knowledge base is created to provide external context for the RAG system. The knowledge base consists of written content that the AI can retrieve and reference when answering questions.

This component is essential because it allows the system to generate responses grounded in actual data rather than relying solely on the language model's internal knowledge.

Knowledge base setup

Content was written and organized in a format suitable for embedding. A preprocessing script was used to convert this content into a searchable form by generating vector embeddings.

### Knowledge base setup

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-api_t1u2v3w4)

### Embeddings created

Embeddings are numerical representations of text that capture semantic meaning. These embeddings were generated using a pre-trained model and stored in a Chroma database.

The database stores both the embeddings and their associated text, enabling efficient similarity searches. This retrieval capability is critical to the accuracy and relevance of the RAG system's responses.

---

## Building the RAG API

This step involves implementing the API that connects user queries to the retrieval and generation pipeline. FastAPI is used to define endpoints and handle requests.

The API provides a reusable interface that allows users to interact with the AI system programmatically.

FastAPI setup

A FastAPI application was created with clearly defined endpoints. Uvicorn was used to run the service locally and expose the API for testing and interaction.

### FastAPI setup

### How the RAG API works

When a user submits a question, the API performs a similarity search against the Chroma vector database to retrieve relevant context. That context is combined with the original question and sent to the local language model.

The model then generates a response that is informed by the retrieved data, producing an answer that is both relevant and grounded in the knowledge base.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-api_f3g4h5i6)

---

## Testing the RAG API

This step validates that the API behaves as expected. Testing ensures that queries are processed correctly and that responses are accurate and consistent.

Testing the API

Swagger UI was used to test the API endpoints interactively. This allowed questions to be submitted directly through the browser and responses to be observed in real time.

### Testing the API

### API query breakdown

A POST request was sent to the /query endpoint with the question "What is Kubernetes?". The API retrieved relevant information from the knowledge base and passed it to the local language model.

The response correctly defined Kubernetes as an open-source system for automating the deployment, scaling, and management of containerized applications, confirming end-to-end functionality.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-api_g3h4i5j6)

### Swagger UI exploration

Swagger UI provided a clear and intuitive way to explore and test the API. The ability to interact with the endpoints directly simplified validation and debugging during development.

---

## Adding Dynamic Content

This extension enhances the RAG API by allowing new content to be added dynamically. Instead of rebuilding the knowledge base, the system can accept new data at runtime.

Adding the /add endpoint

A new /add POST endpoint was implemented to accept additional content. This endpoint generates embeddings for the new data and stores them in the Chroma database.

### Adding the /add endpoint

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-api_w9x0y1z2)

### Dynamic content endpoint working

The /add endpoint allows the knowledge base to grow over time. This makes the RAG system more flexible and better suited for evolving datasets, enabling more accurate and up-to-date responses as new information is introduced.

---

---
