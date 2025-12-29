<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Connect a Web App with Aurora

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-webapp)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Connect a Web App to Amazon Aurora

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-webapp_1709b26b)

---

## Introducing Today's Project!

### What is Amazon Aurora?

This project establishes a simple web application backed by a managed relational database. The system demonstrates how an application tier running on Amazon EC2 connects to Amazon Aurora for persistent data storage. The goal is to validate basic application to database integration within AWS networking and security boundaries.

Amazon Aurora is a managed relational database service compatible with MySQL and PostgreSQL engines. It is designed to provide higher availability and durability than self-managed databases by separating compute from storage and replicating data across multiple Availability Zones. In this project, Aurora is used to provide a managed database backend without requiring database host management.

### How I used Amazon Aurora in this project

Aurora functions as the primary data store for the web application. The application connects to the database using the Aurora cluster endpoint, database name, and credentials configured at the application layer. This design decouples the application runtime from database infrastructure while relying on AWS-managed availability and backups.

### One thing I didn't expect in this project was...

Security group configuration required explicit alignment between the EC2 instance and the Aurora cluster. Network access depended on correctly scoping inbound rules on the database security group to allow traffic from the EC2 security group over the database port. Misalignment at this layer prevented connectivity despite correct application configuration.

### This project took me...

The implementation was completed in approximately one hour. The time included provisioning the EC2 instance, configuring the web application environment, creating or connecting to the Aurora database, updating application connection parameters, and validating end-to-end connectivity.

---

## Creating a Web App

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-webapp_b7999168)

An EC2 instance hosts the web application and serves HTTP traffic. The instance security group permits inbound access for SSH on port 22 and web traffic on ports 80 and 443.

Administrative access is established using SSH with a key pair. The application is validated by accessing it through the instance’s public or elastic IP address.

---

## Connecting my Web App to Aurora

The web application is configured with the Aurora database endpoint, database name, and credentials. Network communication is enabled by allowing the EC2 security group to reach the Aurora security group on the database port. This configuration ensures that database access is restricted to the application tier rather than exposed publicly.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-webapp_1709b25b)

---

## My Web App Upgrade

The application was extended to support filtered search queries based on defined criteria such as date ranges and keywords. This change affects application logic only and relies on the existing Aurora backend to process more selective database queries without altering the underlying infrastructure.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-webapp_2709b25b)

---

## Testing my Web App

Validation focused on application behavior and database integration. Tests included verifying basic application functionality, confirming successful database connections, exercising edge cases in user input, checking UI consistency, and observing response behavior under normal usage conditions.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-databases-webapp_1409z22b)

---

---

## Navigation

| Previous |
|----------|
| [Relational Aurora](./04-relational-aurora.md) |
