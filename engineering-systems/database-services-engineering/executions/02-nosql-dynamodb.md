<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Load Data into DynamoDB

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-dynamodb)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Load Data into a DynamoDB Table

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-dynamodb_b481c730)

---

## Introducing Today's Project!

### What is Amazon DynamoDB?

This project demonstrates the creation of an Amazon DynamoDB table and the loading of sample data using AWS-managed tooling. The scope is limited to basic table definition, capacity configuration, and data insertion to illustrate how DynamoDB operates as a managed NoSQL service without infrastructure management.

Amazon DynamoDB is a fully managed, serverless NoSQL key-value and document database designed for predictable performance at scale. It abstracts capacity provisioning, replication, and availability management while providing single-digit millisecond latency for read and write operations.

### How I used Amazon DynamoDB in this project

A DynamoDB table was created with explicitly defined attributes and a primary key to support deterministic item access. Read and write capacity settings were configured, and data was inserted using AWS CLI commands executed from CloudShell to validate table functionality and access patterns.

### One thing I didn't expect in this project was...

Initial interaction with AWS CLI and CloudShell required understanding credential context and command structure. Once established, these tools provided a consistent and repeatable interface for managing DynamoDB resources without local environment dependencies.

### This project took me...

The implementation was completed within a short time window, covering DynamoDB fundamentals, environment setup, table creation, and data loading. The effort reflects a constrained, non-production exercise focused on validating service mechanics rather than long-term operational tuning.

---

## Create a DynamoDB table

Attributes define the data elements stored in each item, while the primary key establishes the access pattern and uniqueness guarantees for the table. The primary key selection directly influences query efficiency, scalability, and partition distribution within DynamoDB.

An attribute represents a typed key-value pair within an item. Only primary key attributes are required at table creation time, allowing non-key attributes to vary across items without schema migrations or structural enforcement.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-dynamodb_a3cefee0)

---

## Read and Write Capacity

Read Capacity Units and Write Capacity Units define the maximum sustained throughput for a table. RCUs govern read operations based on item size and consistency model, while WCUs govern write throughput based on item size. These controls provide predictable performance boundaries.

The DynamoDB Free Tier includes limited RCUs, WCUs, and storage, suitable for validation and experimentation. Auto scaling was disabled to maintain fixed capacity limits, enabling direct observation of throughput behavior and cost boundaries under manual control.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-dynamodb_ef47dd8f)

---

## Using CLI and CloudShell

AWS CloudShell provides a browser-based, preconfigured environment for executing AWS CLI commands without local installation. It ensures consistent access to AWS services within the active account and region.

The AWS CLI provides programmatic control over DynamoDB resources, enabling repeatable table creation and data operations. Credential configuration is required when used outside of CloudShell to establish authenticated access.

A CLI command was executed in CloudShell to create a DynamoDB table named “Movies” with defined attribute types and a primary key. The table design supports direct lookup by the primary key without secondary indexes.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-dynamodb_81e0258b)

---

## Loading Data with CLI

Sample items were inserted into the “Movies” table using AWS CLI commands. Each item included attributes aligned with the table’s key schema, validating successful writes and confirming table availability for subsequent read operations.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-dynamodb_791c600b)

---

## Observing Item Attributes

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-dynamodb_b481c731)

Items within DynamoDB can contain varying attribute sets beyond the primary key. Observed attributes included identifiers, descriptive fields, categorical data, numeric values, and timestamps, demonstrating DynamoDB’s flexible item structure.

Additional items were observed with attributes specific to different content types, such as books. This highlights DynamoDB’s ability to store heterogeneous item structures within a single table when access patterns allow.

---

## Benefits of DynamoDB

DynamoDB supports flexible data models by enforcing schema only on primary keys, allowing non-key attributes to evolve without downtime. This reduces operational overhead when application data structures change.

Its distributed architecture enables high-throughput, low-latency access patterns optimized for key-based queries. By avoiding joins and complex relational constraints, DynamoDB is suited for large-scale and latency-sensitive workloads.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-dynamodb_b481c730)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Databases Introduction](./01-databases-introduction.md) | [Query Optimization](./03-query-optimization.md) |
