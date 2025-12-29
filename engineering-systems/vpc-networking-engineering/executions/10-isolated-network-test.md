<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Exploratory  
**Audience:** Learner | Designer  
**Production Use:** No  
**System Dependency:** Independent

**Prerequisites:**
- VPC and subnet configuration experience
- Understanding of network isolation concepts
- Knowledge of security boundary testing
- Basic familiarity with connectivity testing tools
- Understanding of isolated subnet patterns
- Access to create and test network configurations

**Outputs:**
- Isolated subnet configuration
- Network isolation validation results
- Security boundary test evidence
- Connectivity test documentation
- Isolation pattern validation

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

This project focuses on isolating workloads within an Amazon VPC by introducing a private subnet. The intent is to enforce network boundaries that prevent direct internet exposure while still allowing controlled internal and outbound communication as required by the architecture.

Amazon VPC is a logically isolated virtual network within an AWS account that provides control over IP addressing, routing, and traffic filtering. It exists to give operators deterministic control over network topology, security boundaries, and connectivity patterns while meeting security and compliance constraints.

### How I used Amazon VPC in this project

A private subnet was defined within an existing VPC with an explicit CIDR range and associated routing configuration. The subnet was attached to a dedicated route table and governed by security groups to ensure traffic flows aligned with isolation and access requirements.

### One thing I didn't expect in this project was...

The configuration steps required careful attention to routing and associations to avoid unintended internet exposure or loss of outbound connectivity. The exercise highlighted how small routing decisions materially affect subnet behavior and security posture.

### This project took me...

The implementation was completed within a short time window due to the limited scope of changes and the absence of dependent application workloads. The effort was focused on correctness of network configuration rather than operational scale.

---

## Private vs Public Subnets

Public subnets are designed for resources that require direct internet reachability through an internet gateway. Private subnets are designed to restrict direct internet access and rely on controlled routing and filtering to limit exposure.

Private subnets are used to host internal or sensitive resources that should not be directly reachable from the internet. This design reduces the attack surface and supports compliance and internal service isolation requirements.

Each subnet requires a unique, non-overlapping CIDR range within the VPC. This prevents routing ambiguity and ensures deterministic traffic flow between public and private network segments.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

Private subnets do not require routes to an internet gateway for direct inbound or outbound traffic. Instead, routing is scoped to internal VPC traffic and explicitly defined egress paths.

A separate route table was created and associated with the private subnet to control traffic behavior. This route table directs outbound traffic to a NAT gateway when internet access is required while preventing inbound internet-initiated connections.

The route table constrains traffic paths to only those explicitly defined. This enforces network boundaries and ensures instances operate within the intended security and connectivity model.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

The private subnet uses routing that limits traffic to internal VPC paths unless explicitly permitted. This reinforces the principle that private resources should not be internet-addressable.

A network ACL was introduced to provide stateless, subnet-level traffic controls. This adds an additional enforcement layer beyond security groups and supports tighter control and auditability of allowed traffic patterns.

Misconfigured network ACL rules can unintentionally block valid traffic. Rule order, directionality, and testing discipline are critical to avoid connectivity failures and false assumptions about network behavior.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-private_1ed2cb07)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [CloudFront Integration](./09-cloudfront-integration.md) | [Flow Logs Validation](./11-flow-logs-validation.md) |
