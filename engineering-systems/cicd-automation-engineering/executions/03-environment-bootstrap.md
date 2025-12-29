<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a Web App in the Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-vscode)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Execution Metadata

**Execution Type:** Reference  
**Audience:** Builder | Learner  
**Production Use:** Conditional  
**System Dependency:** Independent

**Prerequisites:**
- VS Code or similar IDE installed
- AWS CLI configured
- Understanding of development environment setup
- Basic knowledge of application frameworks
- Familiarity with local development workflows
- Access to configure development tools

**Outputs:**
- Development environment configuration
- Local application setup
- Development workflow documentation
- Environment validation results
- Tooling configuration files

---

## Set Up a Web App Using AWS and VS Code

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-vscode_7a1de541)

---

## Introducing Today's Project!

This project implements a basic Java-based web application on AWS using an EC2 instance and Visual Studio Code. The objective is to establish a functional cloud-hosted development workflow that includes compute provisioning, secure remote access, and direct application changes executed within the target runtime environment.

Amazon EC2 serves as the primary compute platform for hosting the application. Core concepts applied include instance provisioning, SSH-based access control, and remote development using Visual Studio Code connected directly to the running cloud system.

This project reinforces foundational cloud application deployment patterns and remote development workflows. It establishes a baseline for later automation and CI/CD work by validating direct development, build, and execution within cloud-hosted infrastructure.

### Key tools and concepts

Amazon EC2 provides cloud-based compute and application hosting. Visual Studio Code with Remote SSH enables direct development against the cloud-hosted system. Apache Maven manages project structure, dependencies, and build automation for the Java application.

### Project reflection

The project was completed in approximately 1.5 hours. The primary challenge involved establishing secure connectivity and aligning the development environment on the EC2 instance. The key outcome was validating end-to-end visibility from code change to application behavior.

A key takeaway was the effectiveness of Visual Studio Code’s remote development model when working with cloud-hosted systems. Developing directly on the EC2 instance reduced environment drift and simplified validation by aligning development and runtime environments.

---

## Launching an EC2 instance

### What I did in this step

In this step, a new Amazon EC2 instance was launched, a key pair was created for secure authentication, and baseline network access was configured to support application management and deployment.

The EC2 instance provides cloud-based compute with full operating system control, enabling direct installation of dependencies, runtime configuration, and hands-on management of the application host.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-vscode_7852fbf3)

### I also enabled SSH

SSH was enabled to provide secure remote access to the EC2 instance. This access supports software installation, system configuration, application deployment, and direct troubleshooting on the server.

### Key pairs

Key pairs provide secure, passwordless authentication for EC2 instances. AWS stores the public key, while the private key is retained locally and used to establish encrypted SSH sessions.

### Downloaded key pair file

AWS generated a private key file required for SSH authentication. The key was stored securely and referenced when connecting to the EC2 instance via the terminal and Visual Studio Code.

---

## Set up VS Code

### What I did in this step

In this step, Visual Studio Code was installed, the local terminal was configured, and SSH key permissions were updated to support secure remote development. This enabled direct interaction with the EC2 instance for file management, command execution, and application development.

### What is VS Code?

Visual Studio Code is a lightweight, extensible code editor that supports multiple languages and remote development through extensions, making it suitable for working directly with cloud-hosted systems.

Visual Studio Code was used to edit code, access a remote terminal, and manage project files directly on the EC2 instance. This allowed development and validation to occur within the same environment where the application runs.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-vscode_53d05e68)

---

## My first terminal commands

The terminal was used to interact with both the local system and the EC2 instance. Initial commands validated access, navigated the file system, and prepared the environment for secure remote connectivity and application management.

### Updating file permissions

Permissions on the private SSH key were restricted to the owning user. This is required for SSH authentication and reduces the risk of unauthorized key access or misuse.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-vscode_9328ada1)

---

## SSH connection to EC2 instance

### What I did in this step

In this step, SSH was used to establish secure command-line access to the EC2 instance. This access enabled software installation, system configuration, and execution of the deployed application.

### Connecting to EC2

The EC2 instance was accessed using SSH with the private key file, the ec2-user account, and the instance’s public address, establishing an encrypted, passwordless session.

### This command required an IPv4 address

The EC2 instance’s IPv4 DNS address was used to resolve its network location and establish the SSH connection, avoiding reliance on static numeric IP addresses.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-vscode_e3069dca)

---

## Maven & Java

### What I did in this step

In this step, Apache Maven and Amazon Corretto 8 were installed and verified on the EC2 instance. These tools are required to build, package, and run the Java application directly within the cloud-hosted environment.

### Why I'm using Maven

Apache Maven manages dependencies, enforces a standard project structure, and automates builds for Java applications through a consistent lifecycle and centralized dependency management.

Maven is required to resolve dependencies, enforce a consistent directory structure, and automate builds. This supports repeatable builds and aligns with CI/CD-compatible workflows.

### Why I'm using Java

Java is used as the application runtime due to its maturity, portability, and consistent execution model through the Java Virtual Machine.

A Java Development Kit is required on the EC2 instance to compile, run, and deploy the application during development and testing.

---

## Create the Application

### What I did in this step

In this step, a basic Java web application was generated using Maven to establish an initial project structure and required dependencies.

### Creating the Java web app

The application was generated using a Maven archetype, which created a standardized project layout and initialized configuration files.

### Installing Remote - SSH

The Remote SSH extension was installed in Visual Studio Code to enable direct development, terminal access, and debugging on the EC2 instance.

### SSH configuration details

The remote connection was configured using the EC2 instance’s IPv4 DNS address, the private key file for authentication, and the ec2-user account.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-vscode_2939cf01)

---

## Create the Application

### Exploring the project structure

The Maven-generated project includes a standard directory structure.

The src directory contains application source code, webapp holds web resources such as JSP files, and pom.xml defines project metadata, dependencies, and build configuration.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-vscode_45f91fd7)

---

## Using Remote - SSH

### What I did in this step

In this step, the VS Code Remote SSH extension was used to work directly on application files hosted on the EC2 instance, allowing changes, testing, and validation to occur in the runtime environment.

### Updating the web app

The index.jsp file serves as the entry point for the application. JSP files support dynamic content generation by embedding Java expressions within page markup.

The index.jsp file was updated to replace placeholder content, validating that changes made through Remote SSH were applied correctly and rendered by the running application.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-devops-vscode_7a1de541)

---

## Using nano

### Additional improvements

### Terminal vs IDE

### Verifying my work

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Source Control GitHub](./02-source-control-github.md) | [Infrastructure CloudFormation](./04-infrastructure-cloudformation.md) |
