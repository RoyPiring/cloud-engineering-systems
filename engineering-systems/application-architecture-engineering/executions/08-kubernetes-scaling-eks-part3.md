<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Create Kubernetes Manifests

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks3)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Create Kubernetes Manifests

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks3_b01876555)

---

## Introducing Today's Project!

This project defines Kubernetes manifest files used to deploy and expose an application on a managed Kubernetes cluster. The manifests describe the desired runtime state for application workloads and supporting services, enabling repeatable deployment, controlled updates, and predictable behavior across environments.

### Tools and concepts

This implementation uses Amazon EKS as the managed control plane, with eksctl and AWS CLI for cluster provisioning, Docker for container image creation, and kubectl for interacting with the cluster API. The core concepts exercised are declarative configuration through manifests, container-based packaging, and Kubernetes primitives including Deployments, Services, and Pods.

### Project reflection

The project focuses on understanding how Kubernetes manifests encode deployment intent rather than imperative execution steps. It emphasizes how application lifecycle behavior is controlled through configuration, and how manifest-driven workflows reduce drift and manual intervention.

This project took approximately two hours. The primary complexity was understanding how pod termination behavior is governed by configuration rather than application logic. The successful outcome was validating that the deployed service was reachable through the configured external endpoint.

---

## Project Set Up

### Kubernetes cluster

A Kubernetes cluster was provisioned in AWS to host the application workloads. The cluster configuration defined worker node capacity, instance types, and networking placement within a VPC. Access controls and basic security boundaries were established, and cluster health was verified by confirming node registration and API connectivity through kubectl.

### Backend code

The backend application deployed to the cluster is a Python Flask service sourced from an existing Git repository. The codebase serves as a simple HTTP application suitable for validating containerization and Kubernetes deployment behavior.

### Container image

A container image was built to package the application and its runtime dependencies into a portable artifact. The image encapsulates the execution environment to ensure consistent behavior regardless of where the container is scheduled.

The container image was pushed to a container registry to make it accessible to the Kubernetes cluster. Storing images in a registry enables versioned deployments, controlled rollouts, and repeatable image pulls by cluster nodes.

To push the image to ECR, the workflow authenticated the local Docker client to the registry, applied a repository-qualified tag to the image, and pushed the image to the remote registry. This sequence ensures the image is addressable by Kubernetes using a stable registry URL and tag reference.

---

## Manifest files

Kubernetes manifests are declarative specifications that define the target state of cluster resources. They are used to describe how applications should run, how many instances should exist, and how components relate to each other, allowing Kubernetes to reconcile actual state against desired state.

The Deployment manifest defines how Pods are created and managed, including which container image version is used. The image reference in the manifest establishes an explicit dependency on a specific registry location and version, ensuring deterministic pod creation.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks3_b01876554)

---

## Service Manifest

A Kubernetes Service provides a stable access point to a dynamic set of Pods. The Service abstraction decouples consumers from individual pod lifecycles and defines how traffic is routed within or outside the cluster.

The Service manifest in this project configures a LoadBalancer to expose the application externally. This results in a cloud-managed load balancer that forwards traffic to healthy Pods, providing external reachability without requiring direct node access.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks3_b01876555)

---

## Deployment Manifest

The Deployment manifest defines how the application is replicated and maintained over time. It specifies the desired number of Pods and the template used to create them, allowing Kubernetes to replace failed Pods and manage rolling updates.

The replica count controls how many identical Pod instances are expected to run concurrently. This supports basic availability and load distribution by ensuring multiple instances of the application exist.

The terminationGracePeriodSeconds setting controls how long Kubernetes allows a Pod to shut down after receiving a termination signal. This value exists to give applications time to complete in-flight requests and release resources before the container is forcibly stopped, directly affecting rollout behavior and service continuity during updates or scaling events.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks3_6aae73e71)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Kubernetes Deployment EKS Part 2](./07-kubernetes-deployment-eks-part2.md) | [Kubernetes Advanced EKS Part 4](./09-kubernetes-advanced-eks-part4.md) |
