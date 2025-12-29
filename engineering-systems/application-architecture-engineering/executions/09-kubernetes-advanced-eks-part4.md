<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy Backend with Kubernetes

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks4)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Deploy Backend with Kubernetes

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks4_6cfb382f2)

---

## Introducing Today's Project!

This project provisions and deploys a backend application onto an existing Amazon EKS cluster. The system establishes a containerized runtime using Kubernetes primitives and AWS-managed services. The objective is to validate a standard backend deployment path using EKS for orchestration, ECR for image distribution, and EC2 worker nodes for compute, without introducing application-level customization.

### Tools and concepts

The system relies on Kubernetes for orchestration, Amazon ECR for container image storage, and kubectl as the control-plane interface. Manifests define desired state for deployments and services, allowing the cluster to reconcile application runtime, networking, and scaling behavior. This approach enforces repeatability, version control, and deterministic infrastructure behavior.

### Project reflection

The implementation scope is intentionally constrained to a minimal backend deployment. The primary complexity lies in aligning IAM permissions to allow cluster visibility and console access without overprivileging. Successful exposure of the service through a load balancer confirms correct integration between Kubernetes resources and AWS-managed networking components.

---

## Project Set Up

### Kubernetes cluster

The Kubernetes cluster acts as the control plane for scheduling and managing backend workloads. It abstracts underlying EC2 capacity and enforces desired state for pods, networking, and availability. This layer exists to decouple application deployment from host-level configuration while supporting horizontal scaling and fault tolerance.

### Backend code

The backend source repository provides the application artifact required for containerization. Access to source code is a prerequisite for building a deployable image and defining runtime behavior. Without the codebase, the system cannot produce an immutable artifact suitable for orchestration.

### Container image

The container image encapsulates the backend application and its runtime dependencies into a single, portable unit. This artifact ensures consistent execution across nodes and environments. Kubernetes depends on this image to instantiate pods reliably and to replace failed or scaled instances without manual intervention.

The container image is stored in Amazon Elastic Container Registry to provide a centralized, authenticated distribution point. ECR enables worker nodes to pull identical image versions on demand, supporting scaling events and rolling updates. Versioned images allow Kubernetes to coordinate controlled updates while minimizing service disruption.

---

## Manifest files

Kubernetes manifests define the desired state of application resources using declarative configuration. They specify deployments, services, replica counts, container images, and networking behavior. This model exists to ensure that infrastructure state can be recreated, audited, and versioned without imperative scripting.

The Deployment manifest defines how many pod replicas must run and which container image they execute. Kubernetes continuously enforces this state, restarting or rescheduling pods as needed to maintain availability.

The Service resource provides a stable access point to the backend application. It abstracts pod IP churn and load balances traffic across replicas. The service configuration defines selectors, port mappings, and exposure type to ensure requests reach healthy application instances.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks4_b01876554)

---

## Backend Deployment!

The manifests are applied using kubectl to submit desired state to the Kubernetes API server. The cluster control plane reconciles this configuration by creating or updating deployments, services, and pods. This workflow relies on Kubernetes reconciliation rather than procedural deployment logic, enabling predictable updates and rollback behavior.

### kubectl

kubectl is the primary interface for interacting with the Kubernetes API. It is used to apply manifests, inspect resource state, and validate deployment health. eksctl is not used in this phase because cluster provisioning is already complete; the focus is runtime resource management within the existing cluster.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks4_6cfb382f2)

---

## Verifying Deployment

The EKS console is used as a secondary visibility layer to observe cluster state and resource health. IAM policies are configured to grant read-level access appropriate for inspection without modifying cluster configuration. This separation supports least-privilege access while enabling operational verification.

Pods represent the smallest schedulable units in the system, grouping one or more containers with shared networking and storage namespaces. This design allows containers within a pod to communicate locally and share lifecycle constraints while remaining isolated from other workloads.

The EKS console confirms that pods are running and services are active without error conditions. This validation demonstrates that the manifests were reconciled correctly and that the backend application is reachable through the configured service endpoint.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks4_3b391f873)

---

---

## Navigation

| Previous |
|----------|
| [Kubernetes Scaling EKS Part 3](./08-kubernetes-scaling-eks-part3.md) |
