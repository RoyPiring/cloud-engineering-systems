<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Canonical  
**Audience:** Builder | Designer | Learner  
**Production Use:** Yes  
**System Dependency:** Required

**Prerequisites:**
- VPC and subnets already created
- Understanding of route tables and routing
- Knowledge of Internet Gateway and NAT Gateway
- Basic understanding of network routing concepts
- Access to configure route table associations

**Outputs:**
- Route table configurations
- Internet Gateway attachment
- NAT Gateway configuration
- Routing validation test results
- Connectivity test evidence

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated network boundary within an AWS account. It defines IP address space, subnet segmentation, routing behavior, and traffic control points. The service exists to provide isolation, deterministic network control, and a foundation for secure communication between cloud resources and external networks.

### How I used Amazon VPC in this project

The VPC was used as a controlled environment to validate basic network reachability between compute resources and external endpoints. The focus was on understanding traffic flow, routing dependencies, and the impact of security controls on connectivity rather than on feature breadth.

### One thing I didn't expect in this project was...

Practical validation exposed how small configuration choices in routing tables and security controls directly affect reachability. The exercise demonstrated that theoretical understanding of VPC components is insufficient without observing real traffic behavior and failure modes.

### This project took me...

The work was scoped to a short execution window and focused on a single objective: validating VPC connectivity using EC2 instances. Time was allocated to configuration review, validation, and troubleshooting rather than automation or optimization.

---

## Connecting to an EC2 Instance

In a VPC, connectivity determines whether resources can communicate internally or reach external destinations. This depends on routing tables, subnet placement, and security controls. When misconfigured, failures range from partial reachability to complete isolation.

The EC2 instance was accessed to confirm baseline network functionality, including subnet routing, inbound access controls, and instance-level reachability. Successful access indicated that the VPC and associated security constructs supported basic inbound communication.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

EC2 Instance Connect provides temporary, AWS-managed SSH access to Linux instances without managing persistent key pairs. It reduces key distribution overhead while still relying on standard network paths and security controls.

Initial access failed due to network or security misconfiguration. Potential causes included missing inbound rules, incorrect source IP restrictions, improper protocol or port settings, or incorrect association of security groups with the instance.

The issue was resolved by validating subnet routing and confirming a valid route to the internet gateway. Route table entries were adjusted to ensure outbound and return traffic could traverse the expected path, restoring external reachability and access.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

ICMP was used to test connectivity between the EC2 instance and external endpoints. This validated that traffic could leave the subnet and receive responses through the configured routing path.

Ping results provided a basic signal of network reachability. Successful replies indicated that routing, security groups, and network ACLs allowed ICMP traffic. Failures would have pointed to blocked protocols or missing routes.

Successful tests confirmed that the VPC configuration supported basic traffic flow. This step validated the combined behavior of subnets, routing tables, and security controls rather than the EC2 instance in isolation.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

Connectivity issues were investigated by reviewing security group rules, network ACLs, and network interface attachments. Diagnostic tools such as ping and traceroute were used to identify where traffic was being dropped or blocked.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl was used as an application-layer validation tool to confirm outbound internet access. Unlike ICMP, it tests TCP-based communication and validates that higher-layer traffic can reach external services.

The curl request confirmed that the EC2 instance could establish outbound connections and receive application data. This demonstrated that routing, security controls, and DNS resolution supported real-world traffic patterns.

### Ping vs Curl

Ping validates basic network reachability using ICMP and is useful for confirming routing and latency. Curl operates at the application layer, validating protocol-specific connectivity and data transfer behavior. Both tools provide complementary signals during network validation.

---

## Connectivity to the Internet

Retrieving HTML content with curl confirmed successful data transfer from an external endpoint. This demonstrated functional outbound connectivity and validated that the instance could support application-level network operations.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-connectivity_8ee57662)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Subnet Segmentation](./02-subnet-segmentation.md) | [Network Security Groups](./04-network-security-groups.md) |
