<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build Your First Azure Function

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-azure-streaming-backend)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-streaming-backend_c9r4t6w1)

---

## Introducing Today's Project!

This project focuses on building a serverless streaming backend using Azure Functions. The goal is to create a backend that can automatically scale and process incoming data in real time without managing servers.

Serverless streaming backends are important for applications that need to react quickly to incoming data, such as IoT systems, real-time analytics, and messaging platforms. Azure Functions provides a managed execution environment that simplifies this type of workload.

### Key tools and concepts

This project uses the Azure CLI, Azure Functions Core Tools, and Python. The main concepts explored include Azure Functions, HTTP triggers, Resource Groups, Function Apps, Cosmos DB, and secure connection strings.
The key takeaway is understanding how serverless compute works in Azure and how individual services are composed to build a scalable backend without manual infrastructure management. 

### Challenges and wins

The project took approximately ninety minutes to complete. The most challenging part was configuring Cosmos DB correctly, especially selecting an appropriate partition key for scalable data storage.
The most rewarding outcome was seeing the function process incoming data in real time and persist it successfully. This validated both the serverless execution model and the database integration.

---

## Setting Up My Azure Environment

The environment is prepared by creating an Azure account, defining a Resource Group, and installing Azure Functions Core Tools. These steps provide the foundation required to build and run serverless workloads in Azure.

The Resource Group is used to logically organize all related Azure resources, making deployment, monitoring, and cost tracking easier.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-streaming-backend_c9r4t6w1)

### Creating a Resource Group

A Resource Group named Streaming-Backend-RG is created in the East US region. This group serves as a container for all resources related to the streaming backend, allowing them to be managed as a single unit.

### Installing Azure Tools

The Azure Functions Core Tools installation is verified by running func --version, which confirms the local runtime is available. Authentication is completed using az login, allowing command-line access to Azure resources.

This ensures the local environment is ready for development and deployment.

---

## Building My First Azure Function

A new Azure Functions project is created using an HTTP trigger. HTTP triggers allow functions to execute in response to incoming HTTP requests, making them suitable for receiving streaming messages.

This setup allows the function to be tested locally before deploying it to Azure.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-streaming-backend_g6k9m1n4)

### Initializing the Project

The project initialization creates the required configuration and dependency files needed for Azure Functions to run correctly. These files define runtime behavior, dependency management, and local settings for development.

This structure ensures consistent behavior across environments and supports safe local testing.

### Testing Locally

The function is tested locally by sending an HTTP POST request with sample JSON data. The function returns a successful response and echoes the processed message.

This confirms the function is correctly handling requests and processing input data as expected.

---

## Deploying to Azure

The function is deployed to Azure so it can run in the cloud. Deployment is done through a Function App, which provides the managed runtime environment for Azure Functions.

A Storage Account is created as part of this process because Azure Functions rely on it for logs, metadata, and runtime state.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-streaming-backend_k2x6a8b3)

### Creating the Function App

A Function App named MyStreamFunctionApp is created using the Consumption hosting plan. This hosting model automatically scales based on demand and charges only for execution time.

This removes the need to manage servers or capacity planning.

### Testing the Live Endpoint

The deployed function is tested by sending a POST request to the public Azure endpoint. The response confirms successful execution and correct message handling.

This verifies that the function works correctly in the cloud environment.

---

## Adding Persistent Storage with Cosmos DB

Persistent storage is added using Azure Cosmos DB to store incoming messages. Cosmos DB is a managed NoSQL database designed for scalability and low-latency access, making it suitable for streaming data.

This ensures data is not lost and can be retrieved for later processing or analysis.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-streaming-backend_p4s7u9w2)

### Creating the Database

A database named StreamingDB is created with a container called MessageContainer. The partition key is set to /username, which enables efficient data distribution and scalable queries.

Choosing the correct partition key is critical for performance and long-term scalability.

### Verifying Persistence

Persistence is verified by sending data to the function and confirming it is stored in Cosmos DB. A successful insert returns a “201 Created” response, and a subsequent query retrieves the same data.

This confirms that the database integration is working correctly.

---

## Project Reflection

This project was completed to learn how to build and deploy a serverless streaming backend using Azure Functions and Cosmos DB. It demonstrates how serverless compute and managed databases can be combined to create scalable, real-time systems.

A future area of learning is integrating AI moderation services and deploying Azure workloads using Azure DevOps pipelines.

---

---
