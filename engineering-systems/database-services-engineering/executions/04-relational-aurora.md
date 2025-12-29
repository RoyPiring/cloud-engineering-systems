<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Aurora Database with EC2

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-aurora)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Connect a Web App to Amazon Aurora

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-aurora_44443546)

---

## Introducing Today's Project!

### What is Amazon Aurora?

Amazon Aurora is a managed relational database service compatible with MySQL and PostgreSQL. It is designed to provide higher throughput than standard managed databases while maintaining automated backups, fault tolerance, and managed failover. The service abstracts storage replication and recovery to reduce operational overhead for relational workloads.

### How I used Amazon Aurora in this project

Amazon Aurora was used as the relational data layer for a web application. The database cluster was provisioned to support scalable reads, managed availability, and durability without manual replication management. The intent was to validate connectivity and integration between a compute tier and a managed relational database under standard AWS networking and security constraints.

### One thing I didn't expect in this project was...

Configuring security group rules required more deliberate design than anticipated. Inbound and outbound rules needed to explicitly account for application-to-database traffic while limiting exposure. Misconfiguration at this layer would prevent connectivity regardless of database or instance health, making network policy correctness a critical dependency.

### This project took me...

The work was completed within approximately one hour. This included provisioning the Aurora cluster, configuring networking and security boundaries, launching an EC2 instance, and validating connectivity. The scope was intentionally limited to core integration rather than schema design or application-level optimization.

---

## In the first part of my project...

### Creating an Aurora Cluster

A relational database stores structured data in tables with defined schemas and relationships. In this project, an Aurora cluster was created from scratch to serve as the managed relational backend. Cluster configuration focused on engine compatibility, baseline availability, and default storage replication rather than custom parameter tuning or performance benchmarking.

Aurora was selected to demonstrate a managed database option that supports high availability and horizontal read scaling while remaining compatible with common relational engines. The service reduces operational responsibility for backups, replication, and failover compared to self-managed database deployments.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-aurora_44443546)

---

## Halfway through I stopped!

Work briefly shifted to provisioning the EC2 instance before completing the database setup. This introduced a dependency inversion, as the compute layer relies on the database endpoint and security configuration. The pause highlighted the importance of sequencing infrastructure components based on dependency order rather than perceived simplicity.

### Features of my EC2 instance

A dedicated key pair was created to enforce controlled SSH access using asymmetric authentication. This aligns with standard AWS access patterns and avoids shared or password-based access mechanisms.

The EC2 instance was selected to support lightweight web application hosting. An appropriate AMI was chosen, the instance type balanced cost and capacity, and security group rules restricted inbound SSH access to a known IP range. These controls ensured the instance could be accessed for configuration while minimizing unnecessary network exposure.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-aurora_91b9fd1g)

---

## Then I could finish setting up my database

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-aurora_1fddb0b5)

The Aurora deployment uses a cluster-based architecture to provide availability and durability. Data is replicated across multiple storage nodes, and the cluster design allows instances to fail without data loss. This architecture supports scaling and resilience at the storage layer, independent of individual database instance lifecycle events.

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Query Optimization](./03-query-optimization.md) | [Database Webapp Integration](./05-database-webapp-integration.md) |
