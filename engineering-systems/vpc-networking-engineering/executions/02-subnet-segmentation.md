<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-vpc)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Canonical  
**Audience:** Builder | Designer | Learner  
**Production Use:** Yes  
**System Dependency:** Required

**Prerequisites:**
- AWS account with VPC service access
- Understanding of CIDR block notation
- Knowledge of subnet design principles
- Basic familiarity with availability zones
- Understanding of public vs. private subnet concepts

**Outputs:**
- VPC with CIDR block configuration
- Public and private subnets across multiple AZs
- Subnet routing configuration
- Network segmentation validation results

---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

This project documents the construction of a foundational Amazon VPC to establish controlled network isolation within AWS. The focus is on defining address space, routing boundaries, and connectivity primitives required for predictable and secure cloud networking.

### What is Amazon VPC?

Amazon VPC is a logically isolated networking boundary within an AWS account. It defines IP address space, routing domains, and traffic control points that govern how resources communicate internally and externally.

The VPC exists to enforce deterministic network isolation, establish security boundaries, and enable controlled connectivity to dependent services while supporting future scalability.

### Personal reflection

The project scope was intentionally limited to core networking primitives. The emphasis was on understanding configuration boundaries and their downstream impact rather than deploying application workloads.

The depth of configuration options highlights how routing tables, subnet placement, and security controls directly influence reachability and isolation. These elements must be aligned to prevent unintended exposure or loss of connectivity.

---

## Virtual Private Clouds (VPCs)

### What I did in this step

A custom VPC was created to serve as the primary network boundary for AWS resources. This establishes the foundational layer required for routing, security enforcement, and subnet segmentation.

### How VPCs work

VPCs are the central networking construct in AWS. They provide an isolated address space and control mechanisms for IP allocation, subnetting, routing, and traffic filtering. All compute and managed services operate within this boundary.

### Why there is a default VPC in AWS accounts

AWS automatically provisions a default VPC in each region to allow immediate resource launch without manual network setup. While convenient, default VPCs abstract critical configuration decisions. This project assumes explicit VPC creation to retain full control over network design.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-vpc_2facf927)

### Defining IPv4 CIDR blocks

A CIDR block defines the private IP address range allocated to the VPC. It constrains all subnets and resources within the network. CIDR selection must avoid overlap with existing or anticipated networks to preserve future connectivity options such as peering or hybrid routing.

---

## Subnets

### What I did in this step

Subnets were created to segment the VPC address space and allocate IP ranges for resources. This enables fault isolation, traffic control, and structured placement across Availability Zones.

### Creating and configuring subnets

Subnets are scoped to a single Availability Zone and define routing behavior through associated route tables. This project uses subnet separation to establish clear boundaries for resource placement and traffic flow.

### Public vs private subnets

Public and private subnets differ by routing configuration. Public subnets include a route to an internet gateway and support externally reachable resources. Private subnets exclude such routes and restrict direct internet ingress, supporting internal or protected workloads.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-vpc_157c4219)

### Auto-assigning public IPv4 addresses

Automatic public IP assignment was disabled for private subnets to prevent unintended internet exposure. This ensures resources remain unreachable from public networks unless explicitly designed for external access.

---

## Internet gateways

### What I did in this step

An internet gateway was attached to the VPC to enable controlled internet connectivity. Route tables were updated to define which subnets are permitted to send or receive internet traffic.

### Setting up internet gateways

Internet gateways provide a managed attachment point between a VPC and the public internet. Without an attached and routed gateway, all resources remain isolated from external networks.

Connecting an internet gateway alone is insufficient. Route table associations determine whether traffic can traverse the gateway. Misconfiguration results in unreachable resources despite gateway attachment.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

### What I'm doing in this extension

VPC components were also created using the AWS CLI through CloudShell. This demonstrates how network infrastructure can be provisioned programmatically for repeatability and automation.

### Exploring CloudShell and CLI

CloudShell provides a browser-based, pre-authenticated CLI environment. The AWS CLI enables direct command execution and scripting for managing VPC resources in a consistent and auditable manner.

### Debugging my setup

CLI-driven configuration requires precise parameters. Errors in CIDR ranges, subnet associations, or gateway attachments propagate quickly and affect dependent resources. Validation is required after each operation.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-vpc_9b2465411)

### Comparing CloudShell vs AWS Console

The AWS Console provides visual feedback and simplifies initial configuration and validation. The CLI supports automation, version control, and repeatable infrastructure definitions once the target architecture is established. Both interfaces serve complementary roles depending on lifecycle stage.

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Networking Introduction](./01-networking-introduction.md) | [Routing Boundaries](./03-routing-boundaries.md) |