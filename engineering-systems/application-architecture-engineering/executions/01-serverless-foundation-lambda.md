<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Fetch Data with AWS Lambda

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-lambda)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Fetch Data with AWS Lambda

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-lambda_p9thryj2)

---

## Introducing Today's Project!

This project implements a serverless read path for user data stored in Amazon DynamoDB. A Lambda function retrieves a single item by partition key and returns a structured JSON response. The design validates basic data access patterns, IAM scoping, and function testing without introducing infrastructure orchestration or API gateways. 

This project exists to demonstrate how a Lambda execution role, DynamoDB access patterns, and SDK usage interact at runtime. It focuses on correctness of permissions, request handling, and response behavior rather than scale or production integration.

### Tools and concepts

The implementation uses Amazon DynamoDB for data storage and AWS Lambda for compute. Core concepts include partition-key-based access, Lambda execution roles, IAM policy scoping, and SDK-based service calls. 

### Project reflection

The work surfaced common failure modes when SDK calls are under-specified, particularly around key conditions and request parameters. The primary technical constraint was ensuring the function returned deterministic results only when permissions and query parameters were correctly aligned.

The project was selected to reinforce serverless read patterns and IAM boundaries in isolation. It intentionally avoids broader system concerns such as APIs, authentication layers, or event-driven fanout to keep the scope focused on data access correctness. 

---

## Project Setup

A DynamoDB table was created with a single partition key named userId. This key defines the access boundary for all read operations and enables direct item retrieval without secondary indexes. The table design assumes point lookups rather than scans or complex queries. 

A sample item was inserted to validate end-to-end retrieval. DynamoDB’s schemaless model allows attributes such as name and email to exist without predefined columns, with the partition key remaining the only enforced constraint. 

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-lambda_a112c3d5)

### AWS Lambda

AWS Lambda is used to execute stateless compute in response to invocation events. In this design, the function encapsulates the data access logic and abstracts infrastructure concerns such as server provisioning, patching, and scaling.

---

## AWS Lambda Function

The Lambda function runs under a custom execution role that defines explicit permissions for DynamoDB access and CloudWatch logging. The role constrains what the function can read and write, independent of the function code itself. 

The function accepts an input containing a userId, retrieves the corresponding item from DynamoDB, and returns the result as JSON. It emits logs to CloudWatch to surface execution outcomes and error conditions for troubleshooting.

The implementation uses the AWS SDK to issue a GetItem-style request against DynamoDB. Correct parameterization of the partition key is required for the call to return data rather than an empty response.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-lambda_a1b2c3d5)

---

## Function Testing

A JavaScript unit test using Jest was created to invoke the Lambda handler and validate its response shape. The test verifies that a successful execution returns structured output when valid input is provided.

An initial test pass masked a functional defect. The test asserted on console output rather than the returned payload, allowing the function to return an empty object due to missing DynamoDB request parameters. This exposed a gap between test assertions and actual behavior.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-lambda_u1v2w3x4)

---

## Function Permissions

An AccessDenied error revealed that the function’s permissions were misaligned with its intended access pattern. The function required permission to retrieve items by key rather than broad read or write access.

Permissions were refined to follow least privilege. The execution role was limited to the specific DynamoDB actions required for item retrieval, reducing the blast radius of the function. 

AmazonDynamoDBFullAccess was intentionally avoided because it allows destructive actions outside the function’s scope. Such permissions introduce unnecessary risk when the function’s responsibility is read-only access. 

AmazonDynamoDBReadOnlyAccess better aligns with the function’s role. It permits item retrieval without allowing modification or deletion of data, matching the system’s access intent

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-lambda_3ethryj2)

---

## Final Testing and Reflection

After updating the execution role, the unit test and a manual invocation were rerun. The function successfully retrieved the expected item when provided with a valid userId, confirming that permissions and request parameters were correctly configured.

The project can be extended into higher-level systems such as authenticated APIs or event-driven workflows, but those concerns are intentionally out of scope for this implementation. 

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-lambda_p9thryj2)

---

## Enahancing Security

Input validation and authorization checks are required to prevent unauthorized access and malformed requests. Without these controls, the function assumes trusted input and operates solely on IAM boundaries.

The execution role combines AWS managed policies with inline policies to constrain access at the action and resource level. This approach balances maintainability with precision when limiting DynamoDB access to specific operations. 

Policy changes introduce the risk of over-permissioning or functional regression. Validation was performed by re-running unit tests and invoking the function directly to confirm continued access without expanding privileges.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-lambda_1qthryj2)

---

---

## Navigation

| Next |
|------|
| [API Layer Gateway Lambda](./02-api-layer-gateway-lambda.md) |
