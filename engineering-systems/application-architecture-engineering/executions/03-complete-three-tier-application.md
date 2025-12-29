<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Three-Tier Web App

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-threetier)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Build a Three-Tier Web App

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-threetier_2b3c4d5e)

---

## Introducing Today's Project!

This project implements a basic three-tier web application on AWS to demonstrate separation of concerns across presentation, logic, and data tiers using managed services.

The system uses S3 and CloudFront for static content delivery, API Gateway and Lambda for request handling, and DynamoDB for data persistence. The tiers are integrated through HTTP-based APIs.

### Tools and concepts

Amazon S3 provides object storage for static assets. Amazon CloudFront distributes those assets globally with edge caching. AWS Lambda executes request logic without server management. Amazon API Gateway exposes REST endpoints. Amazon DynamoDB stores application data with low-latency access.

The core concepts exercised include serverless compute, managed API routing, NoSQL data modeling, static content delivery, and service-to-service integration.

### Project reflection

The implementation focused on validating service integration rather than production hardening. The primary complexity involved cross-origin request handling between CloudFront-hosted assets and API Gateway endpoints.

The outcome confirms that the three tiers communicate correctly and return data end to end under expected request paths.

---

## Presentation tier

The presentation tier consists of an S3 bucket configured for static website hosting and fronted by a CloudFront distribution. This design provides low-cost storage and global content delivery with minimal operational overhead.

End users access the application through the CloudFront distribution URL, which serves cached static assets while abstracting direct access to the S3 origin.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-threetier_3a4b5c6d)

---

## Logic tier

The logic tier uses API Gateway to expose HTTP endpoints backed by AWS Lambda. This tier processes incoming requests and coordinates access to the data layer.

Lambda functions are invoked by API Gateway and perform DynamoDB queries to retrieve or write data. This model enables horizontal scaling without managing servers.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-threetier_6a7b8c9d)

---

## Data tier

The data tier is implemented using Amazon DynamoDB to provide a fully managed NoSQL datastore with predictable performance characteristics.

The table uses userId as the partition key to group related records and enable efficient access patterns. Partitioning supports horizontal scaling across underlying storage nodes.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-threetier_u1v2w3x4)

---

## Logic and Data tier

Client-side JavaScript in script.js issues API requests to API Gateway, allowing the presentation tier to retrieve data from the backend services.

API behavior was validated using HTTP clients such as Postman or curl. Successful requests returned expected payloads and status codes, while invalid requests produced appropriate 4xx or 5xx responses.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-threetier_a112c3d5)

---

## Console Errors

Initial failures were caused by an incorrect API endpoint configured in script.js, preventing the browser from reaching the logic tier.

The endpoint reference was corrected and the updated script was reuploaded to S3 so the CloudFront-served site reflected the change.

A subsequent error was traced to missing or incomplete CORS configuration in API Gateway, which blocked browser-based requests from the CloudFront domain.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-threetier_a1b2c3d5)

---

## Resolving CORS Errors

CORS was enabled on the API Gateway resources to allow requests from the application’s origin by returning the required Access-Control-Allow-Origin headers. The API was redeployed after configuration changes.

The Lambda function was updated to validate inputs, handle error conditions consistently, and return structured responses suitable for client consumption.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-threetier_1qthryj2)

---

## Fixed Solution

Successful resolution was confirmed by loading the application in a browser and observing correct data retrieval from the API.

The browser developer console showed no client-side errors related to API calls. API Gateway integration logs indicated successful Lambda execution and DynamoDB access.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-compute-threetier_2b3c4d5e)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [API Layer Gateway Lambda](./02-api-layer-gateway-lambda.md) | [Container Deployment Elastic Beanstalk](./04-container-deployment-elastic-beanstalk.md) |
