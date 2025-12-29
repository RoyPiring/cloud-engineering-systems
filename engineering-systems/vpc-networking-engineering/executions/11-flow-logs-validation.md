<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-monitoring)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Reference  
**Audience:** Builder | Designer | Learner  
**Production Use:** Conditional  
**System Dependency:** Optional

**Prerequisites:**
- VPC and network resources configured
- Understanding of network monitoring concepts
- Knowledge of CloudWatch Logs or S3
- Understanding of Flow Logs data format
- Basic familiarity with log analysis
- Access to configure Flow Logs destinations

**Outputs:**
- VPC Flow Logs configuration
- Flow Logs destination setup (CloudWatch Logs or S3)
- Network traffic analysis results
- Flow Logs validation evidence
- Network monitoring documentation

---

## VPC Monitoring with Flow Logs

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

This project implements VPC Flow Logs to observe and analyze network traffic within isolated AWS virtual networks. The system captures metadata about network flows to support visibility, troubleshooting, and security analysis without inspecting packet payloads.

### How I used Amazon VPC in this project

Amazon VPC provides logically isolated networking for AWS resources. It defines IP addressing, routing, and traffic boundaries to control how resources communicate internally and externally. The construct exists to enforce isolation, enable deterministic network design, and support scalable application deployment.

### One thing I didn't expect in this project was...

Flow Logs integrate directly with CloudWatch Logs, allowing correlation with metrics and alarms. This enables network telemetry to be analyzed alongside operational signals, improving root cause analysis and reducing time to diagnose connectivity issues.

### This project took me...

The implementation was completed within a short, bounded timeframe and focused on configuring VPC networking, EC2 connectivity, and CloudWatch-based log analysis. The scope emphasized correctness of configuration rather than scale or automation depth.

---

## In the first part of my project...

### Step 1 - Set up VPCs

Two VPCs were created to establish isolated network domains for controlled testing. Separate CIDR ranges enable comparison of routing behavior and validation of traffic visibility across independent network boundaries.

### Step 2 - Launch EC2 instances

An EC2 instance was deployed in each VPC to generate network traffic. These instances serve as endpoints to validate connectivity, routing, and flow log capture.

### Step 3 - Set up Logs

VPC Flow Logs were configured to record accepted and rejected traffic. Centralized logging supports post-hoc analysis of network behavior, security rule effectiveness, and troubleshooting scenarios.

### Step 4 - Set IAM permissions for Logs

IAM permissions were configured to allow VPC Flow Logs to publish data to CloudWatch Logs. The configuration ensures logs are delivered reliably while limiting permissions to only those required for log delivery.

---

## Multi-VPC Architecture

Each VPC was defined with its own CIDR block, subnets, and routing tables. Distinct address ranges prevent overlap and ensure deterministic routing decisions across peered networks.

VPC 1 and VPC 2 use non-overlapping CIDR ranges to avoid routing ambiguity. Overlapping address space would prevent correct packet forwarding and invalidate connectivity testing.

### I also launched EC2 instances in each subnet

EC2 instances were launched within each subnet to generate traffic for monitoring. ICMP was temporarily permitted for testing, acknowledging the associated exposure risk in non-production environments.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

CloudWatch Logs stores VPC Flow Logs and provides centralized access for querying and inspection. This supports near-real-time visibility into network activity and historical analysis.

Log groups organize flow log streams by scope and resource association. This structure simplifies filtering, retention management, and targeted analysis.

### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

IAM policies define which actions are permitted against AWS resources. Least-privilege access reduces the risk of unauthorized operations and supports auditability.

An IAM role was created to grant AWS services permission to deliver logs without embedding credentials. This approach aligns with AWS security best practices and simplifies credential management.

Principals define which identities are allowed to assume roles or access resources. Explicit trust relationships limit access to intended services and accounts.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

ICMP traffic was generated between instances to validate baseline connectivity. This test confirms whether routing and security controls permit expected communication paths.

### Step 6 - Set up a peering connection

VPC peering was established to enable direct communication between the two VPCs. This allows traffic to traverse VPC boundaries without transitive routing or gateways.

### Step 7 - Analyze flow logs

Flow logs from the public subnet were reviewed to confirm traffic acceptance and rejection patterns. The analysis focused on identifying routing gaps and security rule impacts.

---

## Connectivity troubleshooting

Initial ping attempts failed, indicating blocked or misrouted traffic. Potential causes included security group rules, network ACLs, route tables, host firewalls, or instance state.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-monitoring_99d4ba42)

Public IP connectivity succeeded while private IP connectivity failed, indicating missing private routing configuration rather than instance-level failure.

---

## Connectivity troubleshooting

The route table in VPC 1 did not include a route to the destination CIDR in VPC 2. Without this entry, traffic could not be forwarded across the peering connection.

### To solve this, I set up a peering connection between my VPCs

A VPC peering connection was created and route tables in both VPCs were updated to enable bidirectional traffic flow.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

After routing updates, instances responded to ICMP traffic as expected. Successful replies confirm functional routing and security configuration.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs record metadata about network flows, including addresses, ports, protocols, and disposition. This data supports security validation and network troubleshooting.

Captured fields include traffic direction, packet and byte counts, and accept or reject actions. These attributes allow precise identification of where and why traffic is permitted or blocked.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

CloudWatch Logs Insights provides a query interface for analyzing log data at scale. It enables filtering and aggregation without exporting logs to external systems.

Queries were used to identify traffic patterns, protocol usage, and data volume. The results support validation of expected network behavior and identification of anomalies.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-networks-monitoring_3e1e79a1)

---

---

## Navigation

| Previous |
|----------|
| [Isolated Network Test](./10-isolated-network-test.md) |
