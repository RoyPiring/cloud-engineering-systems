<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# AI Security Scanner for AWS S3

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-aws-s3-security)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-s3-security_aws8i9j0k)

---

## Introducing Today's Project!

This project focuses on building an AI-powered security scanner for Amazon S3 that detects encryption-related vulnerabilities and produces actionable security insights. The objective is to automate security posture assessment using serverless AWS services combined with AI-driven analysis, reducing reliance on manual reviews.

This work matters because storage misconfigurations are a frequent cause of data exposure. By integrating Lambda, EventBridge, and Gemini AI, the system demonstrates how cloud security checks can be continuous, explainable, and scalable by design.

### Key tools and concepts

The project uses AWS Lambda for serverless execution, Amazon S3 as the security target, EventBridge for scheduling, boto3 for AWS API access, and Google Gemini AI for intelligent analysis. Cursor is used as the development environment to accelerate iteration and deployment.

The core concepts include AI-assisted security scanning, least-privilege IAM role design, environment variable–based secret management, scheduled execution, and packaging Python workloads for Lambda. Together, these represent a practical foundation for automated cloud security monitoring.

### Challenges and wins

The primary challenge was converting raw S3 configuration data into meaningful, accurate security insights using AI. This required careful prompt design and validation to ensure the analysis focused on real encryption risks rather than generic security advice.

The key win was producing a scanner that not only identifies missing or weak encryption but explains the impact and remediation steps clearly. Seeing the Lambda function return understandable, actionable findings confirmed that AI can enhance security workflows rather than obscure them.

### Why I did this project

This project was completed to strengthen practical knowledge of cloud security automation, with a specific focus on AI-driven analysis. It connects traditional AWS security fundamentals with modern AI tooling in a way that mirrors how security platforms are evolving.

The experience builds hands-on skill in vulnerability assessment, IAM design, serverless execution, and continuous monitoring, all of which are directly applicable to cloud security and platform engineering roles.

---

## Get API Key & Write Scanner

### Setting Up Gemini AI

Gemini AI serves as the analysis engine that evaluates S3 bucket configurations and identifies encryption weaknesses. The API key enables authenticated requests and controlled access to the model.

Using AI in this role allows the scanner to provide contextual explanations and remediation guidance rather than simple pass-or-fail checks.

### Understanding the Code

The scanner code is structured to separate data collection, AI analysis, and result formatting into clear, logical steps. First, boto3 is used to enumerate S3 buckets and retrieve their encryption configurations. This data is normalized into a concise representation that focuses only on security-relevant attributes.

That structured data is then passed to Gemini AI with a targeted prompt that asks the model to identify encryption risks and explain their implications. The response is parsed and returned as a structured report, ensuring the output is readable, actionable, and suitable for logging or downstream processing. This design keeps the AI component focused on analysis rather than control flow, which improves reliability and debuggability.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-s3-security_aws2c3d4e)

### Writing the Scanner Code

The scanner implementation retrieves S3 metadata programmatically and prepares it for analysis by Gemini AI. The model evaluates whether encryption is enabled, identifies weak or missing configurations, and explains why they matter.

The output is designed as a concise security report that highlights findings and recommended actions, making it useful to engineers and security teams rather than producing raw diagnostic data.

---

## Package Code & Create IAM Role

### Preparing the Deployment Package

The code is packaged using a requirements file and a zip archive that includes all dependencies and source files. This produces a self-contained artifact suitable for Lambda deployment.

This approach reduces deployment errors and ensures repeatable builds.

### Attaching Policies to the Role

A dedicated IAM role is created and granted only the permissions required to read S3 encryption settings and write execution logs. Basic Lambda execution permissions are included for observability.

This least-privilege approach limits blast radius and aligns with production security standards.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-s3-security_aws5f6g7h)

### Setting Up IAM Permissions

The role allows read-only access to S3 configuration metadata, ensuring the scanner cannot modify resources. This separation between scanning and remediation is intentional and supports controlled security workflows.

---

## Deploying and Testing Lambda

### Uploading the Function to AWS

Deployment includes validating the handler entry point and confirming that the Lambda runtime can execute the scanner logic successfully.

Successful execution confirms that packaging, permissions, and configuration are aligned.

### Testing the Security Scanner

The function is tested by manually invoking it and reviewing logs and output. The AI analysis identifies encryption gaps and provides recommendations.

This confirms correct integration between AWS data retrieval and AI analysis.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-s3-security_aws8i9j0k)

### Configuring Environment Variables

Environment variables are used to store sensitive configuration such as the Gemini API key. This avoids hardcoding secrets and simplifies updates.

This pattern reflects standard production practices for serverless applications.

---

## Automated Security Scans

### Setting Up EventBridge Scheduling

EventBridge is configured with a time-based rule that triggers the Lambda function every twelve hours. The Lambda function is set as the rule’s target.

This provides predictable, automated execution without maintaining additional infrastructure.

### How EventBridge Scheduling Works

EventBridge invokes the Lambda function according to the defined schedule, triggering fresh analysis of the current S3 configuration state.

This enables proactive, continuous security monitoring that scales with the environment.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-aws-s3-security_awssec2b3c)

### Production Workflow and Monitoring

---

## Wrap-up

---

---
