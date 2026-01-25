# Architecture: AI-Enabled Cloud Security Automation Engineering

## Quick Orientation

**Scope:** AI-enabled cloud security automation using boto3-based scanning, Lambda functions, EventBridge scheduling, Gemini API for AI analysis, and Cursor with AWS MCP for remediation, covering threat detection, automated security response, code scanning, and continuous monitoring.

**Non-Goals:**
- Multi-cloud security automation
- Custom AI model training and development
- Advanced threat hunting beyond automated detection
- Security information and event management (SIEM) platform development
- Custom security orchestration tooling
- Multi-region security automation

**Key Tradeoffs:**
- **Threat Detection:** boto3-based scanning (direct control, programmatic) vs. managed services (simpler, less customization) vs. AI-assisted analysis (contextual, flexible)
- **Security Automation:** EventBridge + Lambda (serverless automation) vs. manual execution (more control, less scalable)
- **AI Services:** Gemini API (external AI, flexible prompts) vs. AWS managed AI services (integrated, less flexible)
- **Code Scanning:** AI-assisted scanning with Gemini (contextual analysis) vs. static analysis tools (pattern-based, faster)
- **Storage Security:** boto3-based automated scanning (programmatic, customizable) vs. manual reviews (thorough, time-consuming) vs. AI-enhanced analysis (contextual insights)
- **Remediation Approach:** Cursor with AWS MCP (AI-assisted, interactive) vs. automated scripts (faster, less flexible) vs. manual remediation (more control, slower)

---

## System Design

This system covers AI-enabled cloud security automation architecture, from threat detection to automated response, documenting tradeoffs in detection accuracy, automation complexity, and operational overhead.

## Core Components

### 1. Threat Detection
- boto3-based S3 configuration scanning
- Security event collection and analysis
- AI-powered analysis via Gemini API
- Direct AWS API integration

### 2. Security Automation
- EventBridge for scheduled security scans
- Lambda functions for serverless security scanning
- Automated security assessment execution
- Scheduled execution patterns

### 3. AI-Assisted Remediation
- Cursor with AWS MCP for interactive remediation
- Natural language interaction for security fixes
- AI-guided configuration changes
- Real-time security posture improvement

### 4. AI/ML Services
- Gemini API for code security analysis
- Gemini API for S3 configuration analysis
- AI-assisted vulnerability detection
- Structured prompt engineering for security insights

### 5. Code Security Scanning
- AI-powered code analysis with Gemini
- Vulnerability detection and categorization
- Severity classification (Critical, High, Medium, Low, Informational)
- Color-coded output using Colorama library
- File-based scanning for complete code analysis

### 6. Storage Security Assessment
- boto3-based S3 bucket configuration scanning
- Encryption status detection
- Access control evaluation
- AI-enhanced security analysis via Gemini
- Lambda-based continuous scanning

### 7. Continuous Monitoring
- EventBridge scheduling for automated scans (12-hour intervals)
- Lambda-based security scanners
- Scheduled execution patterns
- Continuous security posture assessment

### 8. Development and Deployment Tools
- Python 3.12+ for scripting and automation
- uv package manager for dependency management
- AWS CLI for authentication and configuration
- Cursor IDE for development and AI-assisted workflows
- Environment variables for secure credential storage

---

## Architecture Patterns

### Pattern 1: S3 Security Scanning with boto3
```
S3 Bucket → boto3 Scanner → Configuration Analysis → Security Findings
```

### Pattern 2: AI-Powered Code Analysis
```
Python File → Scanner → Gemini API → Security Analysis → Color-coded Vulnerability Report
```

### Pattern 3: AI-Enhanced Storage Analysis
```
S3 Configuration → Lambda → Gemini API → Encryption Analysis → Security Report
```

### Pattern 4: Continuous Security Monitoring
```
EventBridge Schedule (12 hours) → Lambda Scanner → S3 Assessment → Gemini Analysis → Security Report
```

### Pattern 5: AI-Assisted Remediation
```
Security Finding → Cursor + AWS MCP → Natural Language Prompt → Automated Remediation → Verification
```

### Pattern 6: Serverless Security Scanning
```
EventBridge Trigger → Lambda Function → boto3 S3 Scan → Gemini Analysis → Structured Security Report
```

---

## Design Decisions

- **Direct AWS API integration:** boto3 for S3 configuration scanning over managed security services
- **Serverless automation:** Lambda and EventBridge for automated security scanning
- **AI service selection:** Gemini API for code and configuration analysis with structured prompts
- **AI-assisted remediation:** Cursor with AWS MCP for interactive, natural language-driven security fixes
- **Code scanning approach:** File-based scanning with Gemini API for contextual vulnerability detection
- **Severity visualization:** Colorama library for color-coded severity output (Critical=red, High=yellow, Medium=orange, Low=blue, Informational=green)
- **Event-driven architecture:** EventBridge for scheduled security scans (12-hour intervals)
- **Continuous monitoring:** Scheduled Lambda functions for regular security assessments
- **Least-privilege IAM:** Scoped read-only permissions for security scanning functions
- **Development tooling:** Python 3.12+, uv for package management, AWS CLI for authentication
- **Secret management:** Environment variables for API keys and sensitive configuration

---

## Failure Model

**What fails:** S3 scanning failures, Lambda execution errors, AI service unavailability, EventBridge scheduling failures, code scanning errors, AWS MCP connection issues, IAM permission errors

**How it fails:** boto3 scanning fails from permission issues; Lambda execution fails from timeout or dependency errors; Gemini API unavailable causes analysis delays; EventBridge rule misconfiguration prevents scheduled execution; code scanning fails on file parsing errors; AWS MCP connection fails from authentication issues; IAM permission errors block resource access

**Blast Radius:** S3 scanning failure affects only that bucket; Lambda failure affects only that execution; AI service failure affects only that analysis; EventBridge failure affects only scheduled scans; code scanning failure affects only that file; AWS MCP failure affects only interactive remediation; IAM error affects only resources requiring those permissions

**Recovery:** Error handling in boto3 scanners continues with other buckets; Lambda retries for transient failures; AI service fallbacks or manual review for analysis delays; EventBridge rule validation in deployment; code scanning error handling continues with other files; AWS MCP reconnection for authentication issues; IAM role audit and permission fixes

---

## Security Model

**Trust Boundaries:** External AI service boundary (Gemini API calls); AWS MCP boundary (Cursor-to-AWS communication); automation boundary (Lambda execution); code repository boundary (source code analysis); storage boundary (S3 configuration access via boto3)

**IAM Model:** Least-privilege IAM roles for Lambda functions; read-only S3 access for scanning operations; Lambda execution permissions for function runtime; no write permissions for scanning functions; AWS MCP credentials scoped to required resources

**Encryption:** TLS 1.2+ for all API traffic (boto3, Gemini API); API keys stored in Lambda environment variables; AWS MCP credentials stored securely in Cursor configuration; no hardcoded secrets in code

**Audit Trail:** CloudTrail logs all boto3 API calls; Lambda execution logs in CloudWatch Logs; Gemini API usage tracked through API key; code scanning results logged to console/output; S3 scanning results captured in Lambda logs; AWS MCP interactions logged in Cursor

---

## Cost Model

**Primary Drivers:** Lambda ($0.20 per 1M requests + compute time), EventBridge ($1.00 per 1M events), Gemini API (per-request pricing based on model and tokens), S3 API calls (minimal cost for GetBucketEncryption, GetBucketPublicAccessBlock), CloudWatch Logs ($0.50 per GB ingested)

**Guardrails:** Budget alert at $60/month; Lambda concurrency limits prevent runaway costs; Gemini API usage monitored for cost control; scheduled scans limited to every 12 hours (730 executions/month); Lambda timeout limits prevent excessive compute time; environment variable storage (no additional cost)

**Expected Monthly Range:** $15-30/month for lab environment (730 scheduled Lambda executions, moderate Gemini API usage for S3 analysis, CloudWatch Logs for execution history, minimal S3 API costs)

---

## Constraints

**Policy:** Single cloud provider (AWS only); no multi-cloud security automation

**Org:** Team skill sets limited to AWS managed security and AI services; no custom AI model development

**Cost Ceiling:** Security automation infrastructure budget <$60/month for lab environment

**Latency:** Threat detection <5 minutes; automated response <2 minutes; code scanning <30 seconds per file; storage scanning <1 minute per bucket

**Data Classification:** System handles security event data and threat intelligence; requires encryption in transit and at rest; security data subject to standard compliance requirements

**Regions:** Single region deployment (us-east-1 for service availability)

---

## Quality Goals (Detailed)

1. **Threat Detection Accuracy** - How judged: Security threats detected within 5 minutes; false positive rate reduced by 60%; security events correlated and prioritized automatically; detection coverage >95%

2. **Response Automation** - How judged: Automated remediation executes within 2 minutes; mean time to resolution reduced by 50%; security playbooks execute automatically; response success rate >90%

3. **Policy Enforcement** - How judged: Policy violations detected automatically; compliance checks pass validation; policy violations reduced by 80%; enforcement actions logged and auditable

4. **Code Security** - How judged: Vulnerabilities detected during development; security issues categorized by severity; actionable remediation guidance provided; scanning completes <30 seconds per file

5. **Storage Security** - How judged: S3 misconfigurations detected automatically; encryption gaps identified and reported; continuous monitoring enabled; scanning completes <1 minute per bucket

6. **Operational Efficiency** - How judged: Alert investigation time reduced by 70%; automated reports generated without manual effort; security operations productivity increased by 50%; false positive reduction improves signal-to-noise ratio

7. **Cost Efficiency** - How judged: Security automation costs constrained to <$60/month; AI service usage optimized; cost per security check tracked; right-sized automation resources

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |
