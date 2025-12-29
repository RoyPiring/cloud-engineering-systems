<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy an App with Docker

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eb)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eb_c4df13c84)

---

## Introducing Today's Project!

### What is Docker?

Docker packages applications and their dependencies into container images to ensure consistent runtime behavior across environments. In this project, Docker was used to build a containerized web application and deploy it through AWS Elastic Beanstalk, reducing environment-specific variance during deploymen

### One thing I didn't expect...

The Dockerfile required explicit definition of the container startup behavior. Omitting or misconfiguring CMD or ENTRYPOINT resulted in runtime failures, highlighting the need to align image configuration with the execution model expected by Elastic Beanstalk.

### This project took me...

The implementation required approximately two hours. Most effort was spent validating the Dockerfile execution path. Once the container image behavior was corrected, deployment through Elastic Beanstalk proceeded without additional infrastructure changes.

---

## Understanding Containers and Docker

### Containers

Containers encapsulate an application, its runtime, and required system libraries into an isolated execution unit. This abstraction reduces configuration drift and simplifies deployment, scaling, and operational consistency across environments.

Container images are immutable templates used to instantiate containers. They define filesystem state and runtime configuration and serve as the deployment artifact for container-based platforms.

### Docker

Docker provides tooling to build, package, and run container images. Docker Desktop was used locally to manage images and containers through both CLI and GUI interfaces.

The Docker daemon is responsible for building images, running containers, and managing Docker objects. It executes build instructions defined in Dockerfiles and enforces container lifecycle operations.

---

## Running an Nginx Image

Nginx functions as an HTTP server and reverse proxy optimized for handling concurrent connections with low overhead. It is commonly used to serve static content and front web applications.

An Nginx container was started using docker run, with runtime options to expose network ports as required. This validated basic container execution and network accessibility before building a custom image.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eb_6245f5bb10)

---

## Creating a Custom Image

A Dockerfile defines the build process for a custom container image. It specifies the base image, file system changes, and runtime configuration required for the application.

Each Dockerfile instruction executes sequentially during image build. The base image establishes the runtime foundation, while subsequent instructions copy application artifacts and configure execution behavior.

The image was built using docker build -t my-app ., with the current directory serving as the build context for the Dockerfile and associated application files.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eb_4c741d1913)

---

## Running My Custom Image

The initial custom image failed to start because no execution command was defined. This was resolved by explicitly specifying CMD or ENTRYPOINT in the Dockerfile to define the container startup process.

This distinction reinforces the separation between images as immutable templates and containers as running instances that require a defined execution path.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eb_74b5c3d619)

---

## Elastic Beanstalk

AWS Elastic Beanstalk abstracts infrastructure provisioning and lifecycle management for web applications. It manages compute resources, scaling, and health monitoring based on the provided application artifact.

Deploying a Docker-based application required the container image to expose a valid startup command. Once corrected, Elastic Beanstalk handled orchestration and deployment without further manual infrastructure configuration.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eb_26d5573b23)

---

## Deploying App Updates

Application updates were performed by modifying application files such as index.html. Changes were validated through local testing before redeployment.

Elastic Beanstalk managed the rollout of updated container versions. Verification focused on confirming successful deployment and application responsiveness after the update.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-eb_5b7034684)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Complete Three-Tier Application](./03-complete-three-tier-application.md) | [Container Registry ECR](./05-container-registry-ecr.md) |
