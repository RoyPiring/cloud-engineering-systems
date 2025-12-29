# Validation: Application Architecture Engineering

## Purpose

This document provides **objective validation evidence** that the application architecture system behaves exactly as designed.

It records:
- What was tested
- What was expected
- What was observed
- Where the evidence exists

No rationale.  
No architecture explanation.  
No implementation detail.

---

## Validation Summary

| Domain | Status | Primary Evidence |
|--------|--------|------------------|
| Serverless Function Execution | PASS | 01-serverless-foundation-lambda.md |
| IAM Permissions | PASS | 01-serverless-foundation-lambda.md |
| API Gateway Integration | PASS | 02-api-layer-gateway-lambda.md |
| Three-Tier Application | PASS | 03-complete-three-tier-application.md |
| Container Deployment | PASS | 04-container-deployment-elastic-beanstalk.md |
| Container Registry | PASS | 05-container-registry-ecr.md |
| Kubernetes Cluster | PASS | 06-kubernetes-cluster-eks-part1.md |
| Kubernetes Deployment | PASS | 07-kubernetes-deployment-eks-part2.md |
| Kubernetes Scaling | PASS | 08-kubernetes-scaling-eks-part3.md |
| Kubernetes Advanced | PASS | 09-kubernetes-advanced-eks-part4.md |

---

## Validation Scope

Validation covers:

- Serverless function execution and IAM permissions
- API Gateway endpoint functionality
- Three-tier application integration
- Container deployment and orchestration
- Kubernetes cluster provisioning and management
- Application functionality and integration
- Performance and scalability behavior

---

## Serverless Function Execution

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Lambda function invocation | Function executes successfully | Function successfully retrieved the expected item when provided with a valid userId | 01-serverless-foundation-lambda.md |
| DynamoDB access | Function retrieves data from DynamoDB | The function accepts an input containing a userId, retrieves the corresponding item from DynamoDB, and returns the result as JSON; a DynamoDB table was created with a single partition key named userId and a sample item was inserted to validate end-to-end retrieval | 01-serverless-foundation-lambda.md |
| Unit test execution | Test validates function response shape | Unit test and manual invocation rerun successfully | 01-serverless-foundation-lambda.md |

---

## IAM Permissions

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Execution role permissions | Function has correct DynamoDB permissions | AccessDenied error revealed misaligned permissions; permissions refined to follow least privilege | 01-serverless-foundation-lambda.md |
| Least privilege enforcement | Permissions limited to required actions | AmazonDynamoDBFullAccess avoided; AmazonDynamoDBReadOnlyAccess used | 01-serverless-foundation-lambda.md |
| Permission validation | Policy changes validated without regression | Validation performed by re-running unit tests and invoking function directly | 01-serverless-foundation-lambda.md |

---

## API Gateway Integration

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| API endpoint functionality | Endpoints respond correctly | The completed system validates that the API functions correctly without pre-provisioned servers and scales based on request volume | 02-api-layer-gateway-lambda.md |
| Lambda integration | API Gateway invokes Lambda functions | Client requests are received by API Gateway and matched to a resource path and HTTP method; API Gateway invokes the associated Lambda function with the request context and payload; the Lambda function executes application logic, interacts with DynamoDB, and returns a response object | 02-api-layer-gateway-lambda.md |
| API deployment stages | Stages provide isolated environments | API deployed to development and production stages; each stage provides an isolated URL and configuration context; stage separation enables controlled promotion of changes and independent testing without impacting production consumers | 02-api-layer-gateway-lambda.md |
| API documentation | Documentation published per stage | API documentation defines how consumers interact with the service; documentation is published per API Gateway stage to align with deployed environments and ensure consumers reference the correct interface version; publishing documentation binds it to a specific API stage | 02-api-layer-gateway-lambda.md |

---

## Three-Tier Application

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Presentation tier (S3/CloudFront) | Static content served via CloudFront | The presentation tier consists of an S3 bucket configured for static website hosting and fronted by a CloudFront distribution; end users access the application through the CloudFront distribution URL, which serves cached static assets while abstracting direct access to the S3 origin | 03-complete-three-tier-application.md |
| Logic tier (API Gateway/Lambda) | API Gateway processes requests | The logic tier uses API Gateway to expose HTTP endpoints backed by AWS Lambda; Lambda functions are invoked by API Gateway and perform DynamoDB queries to retrieve or write data; client-side JavaScript in script.js issues API requests to API Gateway | 03-complete-three-tier-application.md |
| Data tier (DynamoDB) | DynamoDB stores and retrieves data | The data tier is implemented using Amazon DynamoDB to provide a fully managed NoSQL datastore; the table uses userId as the partition key to group related records and enable efficient access patterns; API behavior was validated using HTTP clients such as Postman or curl | 03-complete-three-tier-application.md |
| End-to-end integration | Three tiers communicate correctly | Successful resolution was confirmed by loading the application in a browser and observing correct data retrieval from the API | 03-complete-three-tier-application.md |
| CORS configuration | CORS errors resolved | CORS enabled on API Gateway resources; API redeployed after configuration changes | 03-complete-three-tier-application.md |
| Error handling | Console errors resolved | Endpoint reference corrected; CORS configuration completed | 03-complete-three-tier-application.md |

---

## Container Deployment

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Docker image creation | Custom image built successfully | Initial custom image failed to start; resolved by explicitly specifying CMD or ENTRYPOINT | 04-container-deployment-elastic-beanstalk.md |
| Elastic Beanstalk deployment | Application deployed via Elastic Beanstalk | Implementation required approximately two hours; deployment proceeded after container image behavior corrected | 04-container-deployment-elastic-beanstalk.md |
| Container execution | Container runs with correct startup behavior | An Nginx container was started using docker run, with runtime options to expose network ports as required; this validated basic container execution and network accessibility; once the container image behavior was corrected, deployment through Elastic Beanstalk proceeded without additional infrastructure changes | 04-container-deployment-elastic-beanstalk.md |

---

## Container Registry

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| ECR repository creation | Repository created for image storage | An Amazon ECR repository was created to host the image; the repository centralizes image storage and enables controlled sharing across accounts while maintaining AWS-managed encryption and access auditing | 05-container-registry-ecr.md |
| Cross-account access | Images accessible across accounts | ECR repository policies are the authoritative control point for cross-account image consumption; the repository owner updated the policy to grant the consuming account permission to retrieve image layers and metadata; cross-account image access was validated after correcting the ECR repository policy | 05-container-registry-ecr.md |
| Image push/pull | Images pushed and pulled successfully | Docker push operations transfer the built image to ECR; the login command retrieves a temporary authorization token from ECR and authenticates the Docker client; the push command uploads the tagged image to the repository; the consuming environment was able to retrieve the image without further authorization errors | 05-container-registry-ecr.md |

---

## Kubernetes Cluster

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| EKS cluster provisioning | Cluster created with control plane and worker nodes | Cluster created using eksctl; provisioning completed in approximately forty five minutes | 06-kubernetes-cluster-eks-part1.md |
| EKS access entry | Administrative access configured | EKS access entry required to authorize administrative interaction with the cluster | 06-kubernetes-cluster-eks-part1.md |
| Node group management | Node group maintains desired capacity | Individual EC2 instances were terminated to observe node replacement behavior and workload rescheduling; validated that managed node group reconciles state automatically | 06-kubernetes-cluster-eks-part1.md |
| Cluster failures | Initial failures identified and resolved | Missing AWS credentials prevented API authentication; invalid CIDR range blocked VPC creation | 06-kubernetes-cluster-eks-part1.md |

---

## Kubernetes Deployment

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Container image build | Backend packaged as container image | A permissions issue occurred during image creation due to insufficient file access; resolved by aligning filesystem permissions | 07-kubernetes-deployment-eks-part2.md |
| ECR integration | Images stored in ECR and pulled by cluster | Amazon ECR serves as the authoritative repository for container images used by the Kubernetes cluster; the container image was pushed to a container registry to make it accessible to the Kubernetes cluster; to push the image to ECR, the workflow authenticated the local Docker client to the registry, applied a repository-qualified tag to the image, and pushed the image to the remote registry | 07-kubernetes-deployment-eks-part2.md |
| Kubernetes deployment | Application deployed to cluster | The manifests are applied using kubectl to submit desired state to the Kubernetes API server; the cluster control plane reconciles this configuration by creating or updating deployments, services, and pods; the EKS console confirms that pods are running and services are active without error conditions | 07-kubernetes-deployment-eks-part2.md |
| Network policies | Network isolation enforced correctly | Network policy configuration requires understanding pod-to-pod and service-level communication boundaries; this implementation demonstrates how Kubernetes network policies restrict traffic between workloads and how Amazon ECR functions as a controlled image source for Kubernetes | 07-kubernetes-deployment-eks-part2.md |

---

## Kubernetes Scaling

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Horizontal pod autoscaling | Pods scale based on demand | The Deployment manifest defines how the application is replicated and maintained over time; it specifies the desired number of Pods and the template used to create them, allowing Kubernetes to replace failed Pods and manage rolling updates; the replica count controls how many identical Pod instances are expected to run concurrently | 08-kubernetes-scaling-eks-part3.md |
| Cluster autoscaling | Node capacity adjusts automatically | Kubernetes continuously enforces desired state, restarting or rescheduling pods as needed to maintain availability; the cluster control plane reconciles configuration by creating or updating deployments, services, and pods | 08-kubernetes-scaling-eks-part3.md |
| Scaling behavior validation | Scaling operates within defined bounds | The replica count supports basic availability and load distribution by ensuring multiple instances of the application exist; Kubernetes depends on the container image to instantiate pods reliably and to replace failed or scaled instances without manual intervention | 08-kubernetes-scaling-eks-part3.md |

---

## Kubernetes Advanced

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Advanced features | Advanced Kubernetes features functional | The Service resource provides a stable access point to the backend application; it abstracts pod IP churn and load balances traffic across replicas; the service configuration defines selectors, port mappings, and exposure type; the Service manifest configures a LoadBalancer to expose the application externally, resulting in a cloud-managed load balancer that forwards traffic to healthy Pods | 09-kubernetes-advanced-eks-part4.md |
| Production readiness | Cluster ready for production workloads | The EKS console confirms that pods are running and services are active without error conditions; this validation demonstrates that the manifests were reconciled correctly and that the backend application is reachable through the configured service endpoint; successful exposure of the service through a load balancer confirms correct integration between Kubernetes resources and AWS-managed networking components | 09-kubernetes-advanced-eks-part4.md |

---

## Negative Testing Summary

| Scenario | Expected Result | Observed Result | Evidence |
|----------|----------------|-----------------|----------|
| Missing AWS credentials | API authentication fails | Missing AWS credentials prevented API authentication | 06-kubernetes-cluster-eks-part1.md |
| Invalid CIDR range | VPC creation fails | Invalid CIDR range blocked VPC creation | 06-kubernetes-cluster-eks-part1.md |
| Missing container startup command | Container fails to start | Initial custom image failed to start because no execution command was defined | 04-container-deployment-elastic-beanstalk.md |
| Incorrect API endpoint | Browser cannot reach logic tier | Initial failures were caused by an incorrect API endpoint configured in script.js | 03-complete-three-tier-application.md |
| Missing CORS configuration | Browser requests blocked | Error traced to missing or incomplete CORS configuration in API Gateway | 03-complete-three-tier-application.md |
| Insufficient file permissions | Image build fails | A permissions issue occurred during image creation due to insufficient file access for the build user | 07-kubernetes-deployment-eks-part2.md |

---

## Known Limitations

- Validation performed in non-production environments
- Manual testing used for integration validation
- Performance metrics not captured for all components
- Scaling behavior validated in limited scenarios
- Cost observations not systematically recorded

---

## Relationship to Other Documents

- **Business Requirements:** `business-context.md`
- **Design Intent:** `architecture.md`
- **Execution Record:** `implementation.md`

This document provides proof. Nothing more.

---

## Navigation

| Previous | Next |
|----------|------|
| [Implementation](./implementation.md) | [README](./README.md) |
