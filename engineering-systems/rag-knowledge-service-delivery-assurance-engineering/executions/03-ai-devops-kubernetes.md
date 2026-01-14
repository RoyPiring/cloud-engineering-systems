<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy a RAG API to Kubernetes

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-devops-kubernetes)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_y7z8a9b0)

---

## Introducing Today's Project!

This project deploys a Retrieval-Augmented Generation (RAG) API to Kubernetes to demonstrate how containerized AI services are orchestrated, managed, and kept available in a production-style environment.

The goal is to move beyond single-host container execution and apply Kubernetes primitives to manage application lifecycle, availability, and access. This project focuses on understanding how Kubernetes abstracts infrastructure complexity while providing reliability guarantees for AI-driven services.

### Key services and concepts

The tools used in this project are Minikube, kubectl, Docker, and FastAPI.

Docker is used to package the RAG API into a container image. Minikube provides a local Kubernetes cluster for experimentation and validation. kubectl is used to interact with the cluster and manage resources. FastAPI serves as the application framework for the RAG API.

Key concepts explored include Kubernetes orchestration, container lifecycle management, deployments, services, self-healing behavior, and applying RAG systems in an orchestrated environment.

### Challenges and wins

This project took approximately 90 minutes to complete. The most challenging aspect was understanding how Kubernetes YAML definitions translate into running infrastructure, particularly how Deployments and Services interact.

The most rewarding outcome was observing the RAG API running reliably inside Kubernetes, responding to requests, and automatically recovering from pod failures. This demonstrated Kubernetes' value as an orchestration platform for AI workloads.

### Why I did this project

I completed this project to gain hands-on experience with Kubernetes and understand how it simplifies the deployment and management of containerized AI applications.

The key takeaway is the practical use of declarative YAML configuration to define desired system state, allowing Kubernetes to manage availability, recovery, and routing without manual intervention.

---

## Setting Up My Docker Image

In this step, a Docker image is prepared for deployment to Kubernetes. Kubernetes schedules containers, and the Docker image serves as the immutable blueprint used to create those containers.

Using a Docker image ensures the RAG API runs consistently across environments, which is critical when deploying to a cluster.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_i9j0k1l2)

### What the Docker image contains

The Docker image was verified using docker images to confirm its presence locally.

The image contains the RAG API application code, all required Python dependencies, and the runtime environment needed to execute the FastAPI service. This includes the application logic, libraries, and configuration required for the API to function correctly inside Kubernetes.

Docker image vs container

A Docker image is a static artifact that defines how a container should be created. A container is a running instance of that image.

Kubernetes uses the image as input and creates containers from it dynamically, restarting or replacing them as needed to maintain the desired system state.

### Docker image vs container

---

## Installing Kubernetes Tools

This step installs the tools required to run and manage a Kubernetes cluster locally.

- Minikube creates a lightweight, single-node Kubernetes cluster for development and testing.

- kubectl provides the command-line interface for deploying applications, inspecting resources, and monitoring cluster health.

These tools are required to deploy and manage the RAG API within Kubernetes.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_u1v2w3x4)

### Verifying the tools are installed

Minikube was verified by running minikube status and confirming the cluster was in a running state.

kubectl was verified by running kubectl version and kubectl cluster-info, confirming successful communication with the Minikube cluster.

Minikube vs kubectl

Minikube provides the Kubernetes environment. kubectl is the control interface used to interact with that environment.

Minikube runs the cluster. kubectl manages what runs inside it.

### Minikube vs kubectl

---

## Starting My Kubernetes Cluster

In this step, the Kubernetes cluster is started using minikube start. The cluster serves as the execution environment for the RAG API.

Cluster health was verified using minikube status, confirming that the cluster was running and ready to accept workloads.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_g3h4i5j6)

### Loading the Docker image into Minikube

After starting Minikube, the Docker image was loaded into the cluster using minikube image load.

The node status was verified using kubectl get nodes, which showed the node in a Ready state, confirming that the cluster could schedule pods.

### Why load image into Minikube

The image must be available inside the Kubernetes cluster so that pods can be created successfully.

Loading the image into Minikube ensures Kubernetes can locate and run the RAG API container without relying on an external image registry.

---

## Deploying to Kubernetes

In this step, the RAG API is deployed using a Kubernetes Deployment.

A Deployment manages the lifecycle of application pods, ensuring that the desired number of replicas are always running. It also enables automatic restarts, updates, and rollbacks, which are critical for application reliability.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_s5t6u7v8)

### How the Deployment keeps my app running

The deployment.yaml file defines how Kubernetes should manage the RAG API.

Key components include:

- apiVersion to specify the Kubernetes API

- kind set to Deployment

- metadata for identification

- spec defining replicas and container configuration

The image field specifies which Docker image to run. The replicas field defines how many pod instances Kubernetes must keep running at all times.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_a3b4c5d6)

### What did you observe when checking your pods?

Running kubectl get pods showed the RAG API pod in a Running state.

The READY value of 1/1 confirmed that the container inside the pod was healthy and ready to serve traffic, indicating a successful deployment.

---

## Creating a Service

In this step, a Kubernetes Service is created to expose the RAG API.

A Service provides a stable network endpoint that abstracts away individual pod IP addresses. This allows clients to access the API reliably even as pods are created or replaced.

### What does the service.yaml file do?

The service.yaml file defines how traffic is routed to the RAG API pods.

The selector matches pods labeled app: rag-api. The port configuration forwards traffic to port 8000, where the API is listening. The Service ensures requests are routed to healthy pods automatically.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_m5n6o7p8)

### What kubectl commands did you run to create the service?

The Service was created using kubectl apply -f service.yaml.

Its status was verified using kubectl get services, confirming that the Service was active and accessible within the cluster.

---

## Accessing My API Through Kubernetes

This step validates external access to the RAG API through Kubernetes.

By using the Service's NodePort, requests can be sent from outside the cluster to the API, confirming end-to-end connectivity.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_y7z8a9b0)

### How I accessed my API

The API was accessed using a curl request targeting the Minikube service IP and NodePort.

The response returned a valid JSON payload, confirming that the API was running and reachable through Kubernetes. This highlights the difference between Docker, which runs containers locally, and Kubernetes, which manages and routes traffic across containerized workloads.

### Request flow through Kubernetes

The request flow moved from the client to the NodePort, then to the Service, and finally to the RAG API pod.

This demonstrates how Kubernetes abstracts routing and load balancing from the application.

---

## Testing Self-Healing

This project extension demonstrates Kubernetes self-healing behavior.

Self-healing ensures application availability by automatically replacing failed components without manual intervention.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_w8x9y0z1)

### What did you observe when you deleted the pod?

When the pod was deleted, Kubernetes immediately created a replacement pod to satisfy the Deployment's desired state.

This confirmed that Kubernetes actively monitors workloads and enforces availability guarantees.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-devops-kubernetes_sm3j8k9l)

### How the Service routed traffic to the new pod

The Service automatically routed traffic to the new pod because it selects pods based on labels.

As soon as the replacement pod became ready, traffic was redirected without manual reconfiguration. This behavior is critical in production systems to avoid downtime and operational intervention.

---

---
