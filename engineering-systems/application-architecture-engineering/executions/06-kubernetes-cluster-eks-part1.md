<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launch a Kubernetes Cluster

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks1)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Launch a Kubernetes Cluster

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks1_e5f6g7h8)

---

## Introducing Today's Project!

This project provisions a managed Kubernetes control plane using Amazon EKS to establish a baseline cluster suitable for non production workloads. The scope focuses on control plane creation, worker node provisioning, and access configuration using AWS managed services. The objective is to validate fundamental EKS architecture, IAM integration, and infrastructure orchestration rather than application deployment.

### What is Amazon EKS?

### One thing I didn't expect

### This project took me...

---

## What is Kubernetes?

Kubernetes is a container orchestration system that manages scheduling, scaling, and lifecycle of containerized workloads across a cluster. It exists to abstract infrastructure concerns away from application teams while enforcing consistent deployment and runtime behavior.

The cluster was created using eksctl, which acts as a higher level abstraction over CloudFormation. The configuration defined cluster identity, region, Kubernetes version, managed node groups, networking ranges, IAM roles, and VPC integration to produce a functional control plane and worker fleet.

Initial failures exposed dependency boundaries. Missing AWS credentials prevented API authentication. An invalid CIDR range blocked VPC creation. Both failures highlighted the tight coupling between IAM configuration and network correctness during EKS provisioning.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks1_ff9bfc221)

---

## eksctl and CloudFormation

An EKS access entry was required to authorize administrative interaction with the cluster. This mapping binds an IAM principal to Kubernetes RBAC permissions, enabling authenticated access to the Kubernetes API without embedding static credentials.

Two CloudFormation stacks were created. The primary stack provisions the EKS control plane and supporting VPC resources. A secondary stack provisions the managed node group. The cluster represents the managed control plane and API endpoint, while the node group represents the EC2 backed compute capacity that executes workloads.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks1_w3e4r5t6)

---

## The EKS console

An EKS access entry was required to authorize administrative interaction with the cluster. This mapping binds an IAM principal to Kubernetes RBAC permissions, enabling authenticated access to the Kubernetes API without embedding static credentials.

Provisioning completed in approximately forty five minutes. Total duration was driven by CloudFormation stack creation, control plane readiness checks, and node group scaling. Runtime could be reduced through pre validated IAM roles, reusable networking templates, and automated access configuration.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks1_e5f6g7h8)

---

## EXTRA: Deleting nodes

EKS worker nodes are implemented as EC2 instances managed through a node group. The node group maintains desired, minimum, and maximum capacity to ensure cluster availability and controlled scaling behavior.

Desired capacity defines the steady state number of nodes. Minimum and maximum bounds constrain autoscaling behavior to prevent resource exhaustion or uncontrolled cost growth.

Individual EC2 instances were terminated to observe node replacement behavior and workload rescheduling. This validated that the managed node group reconciles state automatically and that cluster health remains intact during transient capacity loss.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eks1_q7r8s9t0)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Container Registry ECR](./05-container-registry-ecr.md) | [Kubernetes Deployment EKS Part 2](./07-kubernetes-deployment-eks-part2.md) |
