<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Multi-Cloud Disaster Recovery with Pulumi

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-disaster-recovery-pulumi)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-pulumi_k5j9m2v7)

---

## Introducing Today's Project!

This project demonstrates how to build a multi-cloud disaster recovery setup using Pulumi to manage infrastructure across AWS and GCP. The goal is to create a three-way failover design that improves availability and resilience by distributing the application across multiple regions and cloud providers.

Multi-cloud disaster recovery reduces dependency on a single provider and limits the blast radius of outages. Using Infrastructure as Code makes this possible by allowing infrastructure to be deployed, tracked, and updated consistently through version-controlled code rather than manual configuration.

### Key tools and concepts

Pulumi is used as the Infrastructure as Code platform, with AWS App Runner providing regional services in AWS and GCP Cloud Run acting as an independent backup platform. TypeScript is used to define infrastructure declaratively across providers.

The key concepts include importing existing infrastructure into Pulumi, managing multi-cloud resources from a single codebase, and using IaC to enforce consistency, repeatability, and controlled change across environments.

### Challenges and wins

A major challenge was extending the existing AWS setup into GCP while keeping everything managed under one Pulumi project. This required careful configuration of credentials, APIs, and imports to ensure Pulumi accurately reflected the live infrastructure.

The biggest win was successfully managing AWS and GCP services together through a single Pulumi stack. This validated that multi-cloud infrastructure can be controlled coherently without fragmenting tooling or workflows.

---

## Initializing a Pulumi TypeScript Project

The Pulumi project is initialized using TypeScript to define the infrastructure. The project is named to reflect its multi-cloud disaster recovery purpose and configured to target AWS as the initial provider.

This setup establishes the foundation for managing infrastructure through code rather than manual console changes.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-pulumi_x4c7z1y9)

### Importing existing AWS infrastructure

The existing AWS App Runner services in us-east-1 and us-west-2 are imported into Pulumi using the pulumi import command. This allows Pulumi to take ownership of infrastructure that already exists without recreating it.

A pulumi preview confirms that the imported resources match the deployed infrastructure and that no destructive changes are planned. This ensures the code accurately represents the real environment and is safe to extend.

---

## Deploying to GCP Cloud Run

The application is deployed to GCP Cloud Run after configuring credentials and enabling required APIs. Running pulumi up provisions the Cloud Run service and returns a public URL, confirming the application is running successfully in GCP.

This step adds an independent cloud provider to the architecture, significantly strengthening disaster recovery by removing reliance on a single cloud.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-pulumi_q3r7t1u5)

### Managing multi-cloud infrastructure with Pulumi

The Cloud Run service is imported into Pulumi so it can be managed alongside the AWS App Runner services. At this point, Pulumi controls infrastructure in AWS us-east-1, AWS us-west-2, and GCP Cloud Run within a single project.

This unified management approach is what enables true multi-cloud IaC. Infrastructure across providers is defined, updated, and versioned using the same workflow and codebase.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-pulumi_a1b5c8e3)

---

## Configuring CloudFront Multi-Cloud Failover

CloudFront is configured to route traffic across cloud providers by replacing the secondary AWS origin with the GCP Cloud Run service. This creates a failover path from AWS to GCP.

The CloudFront configuration is then imported into Pulumi so routing and failover logic are also managed as code. This ensures changes to traffic routing are tracked and reproducible.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-pulumi_g5h8j3k7)

### Setting up origin groups for automatic failover

An origin group is configured with health checks to monitor the primary AWS App Runner service in us-east-1. The GCP Cloud Run service is defined as the secondary origin.

If the primary AWS service fails its health checks, CloudFront automatically routes traffic to GCP. This provides cross-cloud failover without requiring application-level logic.

---

## Testing Multi-Cloud Disaster Recovery

Failover is tested by pausing the AWS App Runner service in us-east-1. When the service becomes unavailable, CloudFront redirects traffic to the GCP Cloud Run service.

This confirms that the application remains available even when the primary cloud provider experiences an outage. Traffic switching happens automatically and transparently to users.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-pulumi_r2s5t8u1)

---

## Building a CloudWatch Monitoring Dashboard

A centralized monitoring dashboard is built using Cursor to visualize key metrics across AWS and GCP. The dashboard displays CPU usage, memory usage, error rates, latency, and request counts from both environments.

This unified view is important for disaster recovery because it allows operators to quickly see which platform is handling traffic and whether any service is under stress.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-pulumi_j8k2l5m9)

### Real-time observability for disaster recovery

The dashboard integrates metrics from AWS CloudWatch and GCP Monitoring into a single interface. When failover is triggered by pausing AWS App Runner in us-east-1, the increase in CPU usage on GCP Cloud Run confirms traffic redirection.

This validates both the failover behavior and the effectiveness of centralized observability across clouds.

---

---
