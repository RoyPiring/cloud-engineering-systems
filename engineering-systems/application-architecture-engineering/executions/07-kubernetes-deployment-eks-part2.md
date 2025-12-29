<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up Kubernetes Deployment

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks2)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Set Up Kubernetes Deployment

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks2_45e6c3de5)

---

## Introducing Today's Project!

This project prepares an application backend for deployment on Kubernetes. The system establishes a repeatable path for packaging a backend service as a container image and running it under a managed Kubernetes control plane to support consistent deployment, scaling, and service exposure.

### Tools and concepts

The implementation uses Amazon EKS for cluster orchestration, Docker for container image creation, Amazon ECR for image storage, and Git for source control. The workflow moves from source retrieval to image build, registry publication, Kubernetes deployment definition, image pull configuration, and service exposure to make the backend reachable within the cluster network.

### Project reflection

The primary complexity in this implementation is enforcing Kubernetes network isolation correctly. Network policy configuration requires understanding pod-to-pod and service-level communication boundaries to avoid unintended access while preserving application functionality.

This implementation demonstrates how Kubernetes network policies restrict traffic between workloads and how Amazon ECR functions as a controlled image source for Kubernetes, ensuring that deployed containers originate from a trusted and access-controlled registry.

---

## What I'm deploying

The system consists of a managed Kubernetes cluster running on Amazon EKS. The cluster is created with explicit node capacity, network segmentation through VPC and subnets, and security controls applied at both the infrastructure and Kubernetes layers. Network policies are applied to constrain traffic paths within the cluster.

### I'm deploying an app's backend

The backend represents server-side application logic exposed through APIs and responsible for request handling and data processing. The codebase is sourced from a Git repository and treated as an immutable input to the container build process, ensuring consistency between builds and deployments.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks2_1ebb86c71)

---

## Building a container image

Containerization packages the backend application and its runtime dependencies into a portable unit that behaves consistently across environments. This enables predictable scheduling, isolation, and lifecycle management when the workload runs under Kubernetes.

A permissions issue occurred during image creation due to insufficient file access for the build user. This class of issue is addressed by aligning filesystem permissions with the build process requirements rather than altering the container runtime behavior.

The resolution ensures the executing user has appropriate access and membership in the Docker group. This allows Docker commands to run without elevated privileges while maintaining separation between user access and root-level system control.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks2_45e6c3de5)

---

## Container Registry

Amazon ECR serves as the authoritative repository for container images used by the Kubernetes cluster. It provides controlled storage, versioned artifacts, and IAM-based access enforcement so that only approved images are pulled into the runtime environment.

Using a centralized registry establishes a single source of truth for application images. This supports repeatable deployments, controlled rollbacks, and consistent promotion across environments while integrating directly with AWS-native authentication and Kubernetes image pull mechanisms.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks2_l2m3n4o5)

---

## EXTRA: Backend Explained

The backend repository is structured around a minimal set of files that define runtime behavior, dependencies, and build instructions. Reviewing these files clarifies how application logic is packaged and executed within a containerized environment.

### Unpacking three key backend files

The requirements.txt file defines external Python dependencies and pinned versions. This ensures deterministic builds and prevents runtime drift between development and deployed containers.

The Dockerfile specifies the container build process, including base image selection, filesystem layout, dependency installation, exposed ports, and startup command. It defines how the backend transitions from source code to a runnable container artifact.

The app.py file contains the application entry point and request-handling logic. It defines API routes and coordinates backend behavior, serving as the execution core once the container is started within the Kubernetes pod.

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Kubernetes Cluster EKS Part 1](./06-kubernetes-cluster-eks-part1.md) | [Kubernetes Scaling EKS Part 3](./08-kubernetes-scaling-eks-part3.md) |
