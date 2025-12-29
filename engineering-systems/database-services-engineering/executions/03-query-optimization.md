<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Query Data with DynamoDB

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-query)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Query Data with DynamoDB

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-query_733d9399)

---

## Introducing Today's Project!

### What is Amazon DynamoDB?

Amazon DynamoDB is a fully managed NoSQL key value and document database designed for predictable performance at scale. It abstracts infrastructure management while providing single digit millisecond latency, automatic scaling, and native high availability. The service enforces access patterns through primary keys and optional secondary indexes, which drives data modeling decisions and query efficiency.

### How I used Amazon DynamoDB in this project

This project uses Amazon DynamoDB as a backing data store to demonstrate basic read access patterns through the AWS CLI in CloudShell. The focus is on how partition keys and sort keys control query behavior, how Query and GetItem operations differ from Scan, and how these choices affect performance and cost characteristics.

### One thing I didn't expect in this project was...

Insufficient planning of partition and sort keys led to inefficient access patterns, reinforcing that DynamoDB schema design is an upfront architectural concern rather than an implementation detail.

### This project took me...

The work was completed within a short, bounded session focused on table interaction rather than infrastructure provisioning. The time was primarily spent validating query behavior through the CLI and observing how different key selections affect response efficiency.

---

## Querying DynamoDB Tables

The partition key defines how data is distributed across storage partitions and is required for all efficient point lookups and queries. It represents the primary access dimension and directly impacts scalability and throughput behavior.

The sort key orders items within a partition and enables range based queries on related items. When paired correctly with the partition key, it allows selective retrieval without scanning, which is critical for maintaining predictable performance as data volume increases.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-query_d105b0b0)

---

## Limits of Using DynamoDB

An initial query failure occurred due to attempting to retrieve items using an attribute that was not defined as the partition key. This resulted in an inefficient access pattern. Correcting the table design to align the partition key with the primary lookup attribute restored efficient query behavior.

The Comment table supports aggregate style insights such as basic sentiment grouping, frequency counts, and temporal activity trends. It does not support complex relational analysis, cross table joins, or advanced analytics without external processing systems or downstream data pipelines.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-query_cb3e260c)

---

## Running Queries with CLI

The project uses the AWS CLI get-item operation to retrieve a single item by its primary key. This operation performs a direct lookup and returns the matching item when the key schema is correctly defined.

Additional CLI options control attribute projection, read consistency, and capacity reporting. Query operations support conditional retrieval based on sort keys, while Scan operations perform full table reads and are unsuitable for performance sensitive workloads.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-query_733d9399)

---

## Transactions

A DynamoDB transaction groups multiple write operations into a single atomic unit, ensuring all changes either succeed together or are rolled back. This guarantees consistency across related items without requiring external locking mechanisms.

The demonstrated transaction updates an existing product record and creates a corresponding order record in a separate table. Both operations are executed as a single transactional request to preserve data integrity across tables.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-query_2f65f83e)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [NoSQL DynamoDB](./02-nosql-dynamodb.md) | [Relational Aurora](./04-relational-aurora.md) |
