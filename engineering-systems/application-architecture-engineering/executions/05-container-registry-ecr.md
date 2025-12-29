<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy an App Across Accounts

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-ecr)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-ecr_3e91948719)

---

## Introducing Today's Project!

This project deploys a containerized application across two AWS accounts. The system validates cross-account image access using Amazon ECR, IAM repository policies, Docker, and the AWS CLI. The objective is to demonstrate controlled image distribution without sharing credentials or expanding trust beyond the repository boundary.

### What is Amazon ECR?

Amazon ECR is used as the system of record for container images. It stores, versions, and serves images over authenticated AWS APIs. In this design, ECR enables one AWS account to publish an image while a separate account consumes it through explicitly granted read permissions.

### One thing I didn't expect...

ECR cross-account access is enforced at the repository policy layer, not through IAM role attachment alone. Read access requires explicit actions such as ecr:GetDownloadUrlForLayer, ecr:BatchGetImage, and ecr:GetRepositoryPolicy. Omitting any required action results in image pull failures.

### This project took me...

The implementation required coordinating two AWS accounts, configuring isolated CLI credentials, building and tagging a Docker image, and validating repository policy behavior. The primary outcome was confirming that ECR repository policies are the authoritative control point for cross-account image consumption.

---

## Creating a Docker Image

Two AWS accounts were configured with separate AWS CLI profiles to ensure isolated authentication and access control. Each account operates independently and interacts only through explicitly defined AWS resource policies.

The Dockerfile defines the application runtime environment. It specifies the base image, installs dependencies, copies application artifacts, and defines the container entry point. This ensures consistent behavior across build and deployment environments.

### I also set up an ECR repository

An Amazon ECR repository was created to host the image. The repository centralizes image storage and enables controlled sharing across accounts while maintaining AWS-managed encryption and access auditing.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-ecr_e7f8g9h0)

---

## Set Up AWS CLI Access

### AWS CLI can let me run ECR commands

The AWS CLI is used to interact with ECR and related services programmatically. It enables repeatable authentication, image publishing, and image retrieval operations.

An IAM user with AmazonECRFullAccess was created for image publishing. Access keys were generated to authenticate CLI requests and authorize ECR operations.

The aws configure command was used to register credentials, region, and output format locally. This establishes a scoped CLI context for each AWS account.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-ecr_4aa3e4fe6)

---

## Pushing My Image to ECR

Docker push operations transfer the built image to ECR. This requires tagging the image with the repository URI, authenticating Docker to ECR, and executing the push operation.

### There are three main push commands

The login command retrieves a temporary authorization token from ECR and authenticates the Docker client.

Authentication is scoped to the account and region.

The push command uploads the tagged image to the repository. The tag uniquely identifies the image version and enables downstream consumers to reference a specific artifact.

---

## Resolving Permission Issues

An unauthorized error occurred when the consuming account attempted to pull the image. The ECR repository policy did not allow cross-account read access.

The repository owner updated the policy to grant the consuming account permission to retrieve image layers and metadata. Required actions were explicitly listed to enable successful image pulls.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-ecr_74b90da414)

---

## Deploying the App

Elastic Beanstalk was used as the deployment platform. The environment configuration defines compute resources, scaling behavior, and operating system settings.

An IAM role was created for Elastic Beanstalk with permission to pull images from ECR. This role allows the service to retrieve the container image at deployment time.

The Dockerrun.aws.json file defines the container image source, exposed application port, required environment variables, and logging configuration. This file acts as the contract between Elastic Beanstalk and the container runtime.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-ecr_70ed85fa3)

---

## Resolving Deployment Issues

A 500 error indicated that the application failed during startup. Elastic Beanstalk logs showed missing environment variables required by the application.

The deployment configuration was updated to include the required variables in Dockerrun.aws.json. After redeployment, the application started successfully.

Cross-account image access was validated after correcting the ECR repository policy. The consuming environment was able to retrieve the image without further authorization errors.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-ecr_74b90da411)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Container Deployment Elastic Beanstalk](./04-container-deployment-elastic-beanstalk.md) | [Kubernetes Cluster EKS Part 1](./06-kubernetes-cluster-eks-part1.md) |
