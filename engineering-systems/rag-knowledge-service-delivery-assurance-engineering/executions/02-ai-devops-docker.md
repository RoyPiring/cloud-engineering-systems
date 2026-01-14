<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Containerize a RAG API with Docker

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-devops-docker)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-docker_x7y8z9a0)

---

## Introducing Today's Project!

This project demonstrates how to containerize a Retrieval-Augmented Generation (RAG) API using Docker. The objective is to package an existing AI application into a portable, reproducible container that can run consistently across environments.

The focus is on applying Docker in a practical DevOps context while reinforcing how AI systems are prepared for deployment. By containerizing the RAG API, this project bridges application development and operational readiness.

### Key services and concepts

The services used in this project are FastAPI, Chroma, Uvicorn, Ollama, and Docker.

FastAPI provides the API layer, Chroma serves as the vector database for retrieval, Uvicorn runs the application server, and Ollama supplies the local language model. Docker is used to package the entire system into a consistent runtime environment.

Key concepts explored include containerization, Retrieval-Augmented Generation (RAG), vector databases, AI model integration, API development, and Dockerfile creation.

### Challenges and wins

This project took approximately 90 minutes to complete. The primary challenge was integrating the Ollama language model into the containerized environment and ensuring it functioned correctly alongside the retrieval components.

The most rewarding outcome was successfully running the RAG API inside a Docker container with behavior identical to the local setup. This confirmed that the application was fully portable and consistently deployable.

### Why I did this project

I completed this project to strengthen my DevOps skill set by learning how to containerize AI-driven applications. Containerization is a critical step in moving from local development to reliable deployment.

This project also reinforced how AI systems are packaged and delivered in real environments, providing hands-on experience with Docker alongside FastAPI, Chroma, Uvicorn, and Ollama.

---

## Setting Up the RAG API

In this step, the foundational components of the RAG API are prepared for containerization. The API must be fully functional locally before it can be packaged and deployed reliably.

The setup includes preparing the application code, ensuring dependencies are installed, and verifying that the local language model is accessible.

### API setup and workspace

A Dockerfile is created to define the runtime environment for the RAG API container. This file specifies the base image, dependencies, application files, and startup commands.

Docker Desktop is installed to enable local container builds and execution. Containerizing the application ensures that all required libraries, configurations, and runtime settings are packaged together, reducing environment-specific issues.

### Dependencies installed

The installed dependencies include FastAPI, Chroma, Uvicorn, and Ollama.

FastAPI is used to build the API endpoints. Chroma stores and retrieves vector embeddings for the RAG process. Uvicorn serves the API efficiently. Ollama provides access to a local language model used for generation.

Each dependency has a defined role within the system and is required for end-to-end RAG functionality.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-docker_c9d0e1f2)

### Local API working

The RAG API was validated locally by sending a test query to the API endpoint. The response confirmed that retrieval and generation were functioning correctly.

This verification step ensures that FastAPI, Chroma, Uvicorn, and Ollama are properly integrated before introducing Docker into the workflow.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-docker_v5w6x7y8)

---

## Installing Docker Desktop

### Docker Desktop setup

Docker Desktop provides a graphical interface and supporting tools for building and managing containers locally. It simplifies the containerization workflow by handling Docker engine setup, image management, and container execution.

Using Docker Desktop ensures that the RAG API can be packaged and run consistently, regardless of the underlying operating system. This portability is essential for deployment and scaling.

### Docker verification

Docker was verified by running the docker run hello-world command. This command pulls and executes a simple test container, confirming that Docker is installed and functioning correctly.

Successful execution validates that the local system can build and run containers, which is required for the remainder of the project.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-docker_i9j0k1l2)

---

## Creating the Dockerfile

In this step, the application is prepared for containerization by defining all required files and instructions.

The project includes:

- A Dockerfile to define the container image

- A requirements.txt file for Python dependencies

- API source code files

- Supporting data files

These components ensure the container can be built and run independently.

### How the Dockerfile works

A Dockerfile is a declarative set of instructions used to build a container image.

The primary instructions used are:

- FROM, which specifies the base image

- COPY, which transfers application files into the container

- RUN, which executes commands such as dependency installation

- CMD, which defines the command executed when the container starts

Together, these instructions create a reproducible and self-contained runtime environment.

### Containerized API test results

After containerization, the API was tested and confirmed to function identically to the local version. Query responses, performance, and behavior remained consistent.

The key difference between local execution and Docker execution is environment control. The container provides a standardized runtime that eliminates system-specific differences, improving reliability and deployment confidence.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-docker_o1p2q3r4)

---

## Building and Running the Container

### Docker image build complete

Building the Docker image packages the application code, dependencies, and runtime into a single portable artifact.

The image build was verified using docker images to confirm its presence and metadata. The container was then started using docker run -p 8000:8000 <image-name>, and the API endpoint was accessed successfully.

This confirms that the RAG API is fully containerized and operational inside Docker.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-docker_p9q0r1s2)

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-docker_x7y8z9a0)

---

## Pushing to Docker Hub

This project extension publishes the container image to Docker Hub, a centralized container registry.

Pushing the image allows it to be shared, reused, and deployed across different systems and environments without rebuilding locally.

### Docker Hub push complete

The image was pushed to Docker Hub by authenticating with docker login, tagging the local image with the appropriate repository name, and executing docker push.

Using Docker Hub enables collaboration, version control, and consistent deployments by providing a trusted source for container images.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-docker_m5n6o7p8)

### Pulling from Docker Hub

Pulling an image from Docker Hub downloads a pre-built container image from the registry to a local system.

The difference between building locally and pulling from Docker Hub is control versus convenience. Building allows customization, while pulling enables rapid reuse and deployment. Both approaches support consistent, reproducible environments when using Docker.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-docker_f5g6h7i8)

---

---
