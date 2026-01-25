<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build an AI Security Guard for AWS

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-aws-security-guard)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-security-guard_aws2m3n4o)

---

## Introducing Today's Project!

This project focuses on building an automated S3 security scanner to detect and fix common security issues in AWS. The goal is to apply AI and automation to a real cloud security problem rather than relying on manual reviews.

The project is designed to strengthen understanding of AWS security fundamentals, boto3 automation, and how AI-assisted tools can be used to identify and remediate misconfigurations in a live cloud environment.

### Key tools and concepts

This project uses Python 3.12 or newer, the AWS CLI, boto3, uv, and Cursor integrated with AWS MCP. These tools work together to provide programmatic access to AWS resources and enable AI-assisted interaction with the environment.

The core concepts include Amazon S3 security, boto3-based automation, AI-assisted remediation, and secure access to AWS through MCP. The most important learning outcome was understanding how AI can be applied safely and effectively to automate repetitive security tasks while operating within AWS best practices.

### Challenges and wins

The project took approximately one hour to complete. The most challenging part was configuring Cursor with AWS MCP in a way that allowed reliable access to AWS resources without authentication issues.

The biggest win was seeing the scanner automatically identify insecure S3 configurations and then successfully remediate them. This demonstrated that AI-driven automation can meaningfully reduce the effort required to maintain a secure cloud environment.

### Why I did this project

I completed this project to deepen my understanding of how AI can be used in cloud security, specifically for automating S3 vulnerability detection and remediation. It provided hands-on experience using AI-assisted tooling to secure real AWS resources instead of working with simulated examples.

As a next step, I plan to explore additional S3 security controls such as server-side encryption, lifecycle policies, and more advanced monitoring to further strengthen data protection and compliance.

---

## Setting Up Your Environment

In this step, the environment is prepared by installing and configuring the required tools. Python provides the programming foundation, while the AWS CLI enables authenticated access to AWS services. boto3 allows the scanner to interact with S3 programmatically, and uv is used for Python package management.


![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-security-guard_aws2c3d4e)


The setup is verified by running aws sts get-caller-identity, which confirms that the AWS CLI is correctly configured and that the account and permissions are available for use by the scanner.

---

## Building the S3 Security Scanner

The security scanner is built to examine all S3 buckets in the account and evaluate their configurations. It lists each bucket and checks access control settings and bucket policies to identify potential vulnerabilities such as public access.



![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-security-guard_aws5f6g7h)

Error handling is implemented using try and except blocks to ensure the scanner continues running even if it encounters permission issues or misconfigured buckets. This makes the scanner resilient and suitable for use across real AWS environments with varying configurations.

Through this step, I learned that securing S3 requires multiple layers of protection, including strict access controls, regular configuration reviews, and continuous monitoring to quickly detect and respond to security risks.

---

## Connecting Cursor to AWS with MCP

In this step, Cursor is connected to AWS using AWS MCP. This integration allows Cursor to authenticate with the AWS account and interact directly with S3 resources.



![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-security-guard_aws8i9j0k)

The connection is configured by entering AWS credentials into Cursor and verifying that the MCP status shows a successful connection. A simple resource query confirms that Cursor can access S3 and retrieve expected data, ensuring the environment is ready for AI-assisted remediation.

---

## Testing Your Scanner

The scanner is tested by creating an intentionally insecure S3 bucket. A new bucket is created with public read access to simulate a common security misconfiguration.

When the scanner is run, it correctly identifies the bucket as insecure and flags it as a potential risk. This confirms that the scanner is functioning as expected and can detect real-world S3 security issues

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-security-guard_aws2m3n4o)

I created the test bucket by using Cursor to create a new S3 bucket and intentionally setting its access permissions to "Public Read" to simulate a security vulnerability. When I ran `scanner.py`, it detected the S3 bucket with public read access, flagging it as a potential security risk. This shows that my S3 security scanner is functioning correctly and can identify common vulnerabilities like public access settings.

---

## Fixing Security Issues with AI

AI is used to automatically remediate the detected security issues by modifying S3 bucket permissions. Cursor and AWS MCP enable this process through natural language prompts that translate into secure configuration changes.



![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-security-guard_awssec2b3c)

The public access settings are removed, reducing the risk of unauthorized data exposure. The scanner is run again to confirm that the issues are resolved. This demonstrates how AI-assisted workflows can enforce consistent security posture while reducing manual effort.

---

## Wrap-up

---

---
