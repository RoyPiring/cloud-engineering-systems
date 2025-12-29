<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Cloud Security with AWS IAM

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-iam)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Canonical  
**Audience:** Builder | Designer | Learner  
**Production Use:** Yes  
**System Dependency:** Required

**Prerequisites:**
- AWS account with appropriate permissions
- Understanding of IAM fundamentals
- Access to EC2 service for testing
- Basic knowledge of JSON policy syntax
- Familiarity with AWS Management Console

**Outputs:**
- IAM users, groups, and policies
- Account alias configuration
- Policy evaluation test results
- IAM Policy Simulator validation results
- Access control validation evidence

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-iam_1c864649)

---

## Introducing Today's Project!

### Project overview

This project configures AWS Identity and Access Management to control access to AWS resources. The scope includes IAM users, groups, policies, account aliases, and permission evaluation against EC2 resources.

### Tools and concepts

The system uses IAM to define who can perform actions against specific AWS resources. Policies express allowed and denied actions, while users and groups provide a structure for assigning those permissions.

### Project reflection

The implementation validates how IAM enforces least-privilege access and how misaligned permissions surface as explicit access failures.

---

## Tags

### What I did in this step

Tags provide metadata used to classify and scope resources. 

### Understanding tags

They enable policy conditions that differentiate access based on environment or purpose.

### My tag configuration

EC2 instances are tagged with an environment key to distinguish development and production workloads. These tags act as control inputs for conditional IAM policies.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-iam_2e0e5a5d)

---

## IAM Policies

### What I did in this step

IAM policies define authorization boundaries by explicitly allowing or denying actions on resources.

### Understanding IAM policies

The policy is defined in JSON and attached according to IAM policy syntax and evaluation rules.

### The policy I set up

The policy allows start, stop, and describe actions on EC2 instances tagged as development. 

### Policy effect

It explicitly denies tag creation and deletion across instances to prevent privilege escalation or scope manipulation.

### Understanding Effect, Action, and Resource

Each policy statement specifies Effect, Action, and Resource. Effect determines allow or deny behavior, with explicit deny taking precedence. Action defines the API operations controlled. Resource scopes the policy to specific AWS resources or patterns.

---

## My JSON Policy

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-iam_1c864649)

---

## Account Alias

### What I did in this step

An account alias provides a human-readable identifier for AWS console sign-in.

### Understanding account aliases

It replaces the numeric account ID in the login URL to reduce operational friction and user error.

### Setting up my account alias

Creating the alias generates a stable, user-facing sign-in endpoint without altering account security posture or permissions.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-iam_0eb4439b)

---

## IAM Users and User Groups

### What I did in this step

IAM users represent identities used by people or systems to authenticate into AWS. Each user has credentials and no permissions by default.

### Understanding user groups

User groups aggregate users under shared permission sets. Policies attached to a group apply uniformly to all members, simplifying access management and reducing configuration drift.

### Attaching policies to user groups

Attaching the policy to the group grants members conditional access to EC2 actions based on resource tags.

### Understanding IAM users

Group members inherit both allowed development actions and enforced production restrictions.

---

## Logging in as an IAM User

### Sharing sign-in details

IAM user credentials can be distributed through secure channels such as generated credentials or CSV exports.

### Observations from the IAM user dashboard

An access denied error on login indicates missing or insufficient permissions. This behavior confirms that IAM denies access by default unless explicitly allowed.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-iam_6f2ab446)

---

## Testing IAM Policies

### What I did in this step

Policy behavior is validated by attempting actions against resources in different environments.

### Testing policy actions

I have tested my JSON IAM policy to allow modifications to development resources while restricting such actions on production resources.

### Stopping the production instance

The stop action failed on the production instance because the policy does not allow modification of production-tagged resources.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-iam_0e7a9d6a)

### Stopping the development instance

The stop action succeeded on the development instance. This confirms that the policy correctly allows modifications only for resources matching the development tag condition.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-iam_1811801c)

---

## IAM Policy Simulator

The IAM Policy Simulator evaluates policies without executing live API calls.

### Understanding the IAM Policy Simulator

It shows how IAM resolves permissions for a given principal, action, and resource.

### How I used the simulator

The simulator was used to test policy outcomes and identify unintended access paths. Policy conditions were refined to enforce least privilege and align allowed actions with intended resource scope.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-iam_069d8a621)

---

---

## Navigation

| Next |
|------|
| [Secrets Management](./02-secrets-management.md) |
