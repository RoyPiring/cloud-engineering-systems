<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Encrypt Data with AWS KMS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-kms)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Canonical  
**Audience:** Builder | Designer | Learner  
**Production Use:** Yes  
**System Dependency:** Required

**Prerequisites:**
- AWS account with KMS and DynamoDB access
- Understanding of encryption concepts
- Knowledge of IAM policies and key policies
- Basic familiarity with DynamoDB operations
- Understanding of envelope encryption patterns

**Outputs:**
- Customer-managed KMS key configuration
- DynamoDB table with encryption enabled
- IAM policies for key access control
- Encryption validation test results
- Access denial test evidence

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-kms_w0x1y2z3)

---

## Introducing Today's Project!

### Project overview

This project implements encryption at rest for data stored in Amazon DynamoDB using AWS Key Management Service. The system integrates a customer-managed KMS key with DynamoDB to enforce encryption, key ownership, and access boundaries through IAM and key policies.

### Tools and concepts

The implementation uses AWS KMS for key lifecycle and access control and Amazon DynamoDB as the encrypted data store. Core concepts include envelope encryption, symmetric customer-managed keys, IAM authorization, and service-integrated encryption behavior.

### Project reflection

The work focused on evaluating DynamoDB encryption options and selecting a customer-managed KMS key to meet auditability and access control requirements. The primary complexity was understanding how DynamoDB encryption interacts with IAM and KMS key policies.

The project exists to establish a baseline pattern for protecting sensitive data in managed AWS services where encryption must be enforced independently of application logic.

---

## Encryption and KMS

Encryption converts plaintext into ciphertext using a cryptographic key to protect confidentiality and integrity. Effective systems separate key management from data storage to reduce blast radius and support auditing.

AWS KMS provides centralized key creation, policy enforcement, rotation, and audit logging. It integrates with AWS services to apply encryption without exposing key material to applications.

Encryption keys are either symmetric or asymmetric. This implementation uses a symmetric customer-managed key, which DynamoDB requires for server-side encryption and which supports high-throughput data operations through envelope encryption.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

The DynamoDB table is configured to use server-side encryption with a customer-managed KMS key. DynamoDB handles encryption and decryption operations internally while delegating key usage decisions to KMS.

DynamoDB supports encryption using AWS-owned keys, AWS-managed keys, or customer-managed keys. A customer-managed key was selected to enable explicit control over key policy, access grants, rotation, and audit visibility beyond the defaults provided by DynamoDB-managed keys.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

Access to encrypted data is governed by both DynamoDB permissions and KMS key permissions. IAM policies control who can read or write table items, while the KMS key policy controls who can decrypt the data keys used by DynamoDB.

Encryption is transparent to applications. DynamoDB encrypts data at rest and decrypts it on access when the caller is authorized, without requiring application-level cryptographic handling.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

A test IAM user was configured with permissions to describe the DynamoDB table but without permissions to use the associated KMS key. This setup isolates data visibility from metadata visibility.

When accessing the table as the test user, item contents were not readable because DynamoDB could not obtain decryption permission from KMS. This behavior confirms that KMS authorization is enforced independently of DynamoDB read permissions.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

The test user was granted kms:Decrypt and kms:GenerateDataKey permissions scoped to the specific KMS key. The key policy was updated to allow the user to use the key for DynamoDB encryption operations.

After updating permissions, the test user could read decrypted item data from the DynamoDB table. This demonstrates that successful data access requires both DynamoDB permissions and explicit KMS key authorization.

Encryption complements access controls by enforcing cryptographic boundaries. When combined with IAM and service policies, it provides defense in depth without relying on application-level safeguards.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-security-kms_feffb2fb8)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Secrets Management](./02-secrets-management.md) | [Compliance Checklist](./04-compliance-checklist.md) |
