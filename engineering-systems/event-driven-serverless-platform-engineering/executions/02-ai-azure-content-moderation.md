<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build AI Chat Moderator with Gemini

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-azure-content-moderation)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-content-moderation_cm1b4g8y)

---

## Introducing Today's Project!

This project focuses on building a production-grade content moderation API using Gemini to detect and filter toxic chat messages. The goal is to design a system that can automatically evaluate incoming messages, block harmful content, and store moderation decisions for later review.

This work is valuable because AI-driven content moderation is a core requirement for modern platforms that host user-generated content. The project provides hands-on experience with Gemini, Azure Functions, Cosmos DB, and moderation patterns that are commonly used in real production systems.

### Key tools and concepts

The primary tools used in this project are the Gemini API, Azure Functions, and Azure Cosmos DB. Together, these services enable real-time AI analysis, serverless execution, and scalable data storage.

The key concepts explored include content moderation, secure API key management, the fail-open pattern, structured data storage and retrieval, and building a moderator dashboard API. The focus is on designing a system that is both safe and resilient under real-world conditions.

### Challenges and wins

This project took approximately forty-five minutes to complete. The most challenging part was integrating the Gemini API while ensuring the fail-open pattern behaved correctly during error scenarios.

The most rewarding outcome was seeing the system successfully filter toxic messages while still allowing legitimate messages to flow. Building a functional moderator dashboard reinforced how automated moderation and human oversight work together.

---

## Generating a Gemini API Key

The API key is created by following the instructions on the Google AI platform and ensuring all security requirements are met. The key is used to authenticate the application with the Gemini API and enable real-time content moderation.

This establishes the trust boundary between the application and the Gemini service.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-content-moderation_cm1d6j2k)

### Creating the API key

The API key is created by following the instructions on the Google AI platform and ensuring all security requirements are met. The key is used to authenticate the application with the Gemini API and enable real-time content moderation.

This establishes the trust boundary between the application and the Gemini service.

### Configuring Azure with the API key

The API key is added to the Azure Function App through the Application Settings section in the Azure portal under the name GEMINI_API_KEY.

Application settings are used because they provide a secure and centralized way to store sensitive data. This prevents secrets from being hardcoded, allows updates without redeployment, and improves long-term maintainability.

---

## Creating the Violations Container

A separate violations container is created in Cosmos DB, Gemini integration is added to the Azure Function, and the POST /message endpoint is modified to evaluate messages before saving them.

This step is important because it creates structured storage for flagged content, integrates AI moderation into the request path, and ensures unsafe content is handled appropriately.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-content-moderation_cm2b9q5r)

### Why separate violations from messages

The violations container is created with its own identifier and partition key optimized for querying moderation events. It is kept separate from the messages container to support focused analysis and reporting.

This separation maintains data integrity, improves query efficiency, simplifies auditing, and allows moderation workflows to evolve without impacting normal message storage.

---

## Building the AI Moderation Code

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-content-moderation_cm2d1u7v)

### How the moderation logic works

When a message is received, its text is sent to Gemini for analysis against moderation guidelines. If Gemini flags the content, the message is written to the violations container and not saved to the main messages database.

The system uses a fail-open pattern. If an error occurs during moderation, such as a Gemini API issue or database failure, the message is still saved and the error is logged. This prevents moderation outages from breaking core chat functionality while preserving signals for later review.

---

## Testing the Content Moderation System

The updated Function App is deployed and tested with both clean and toxic messages. This validates that harmful content is blocked while legitimate messages are handled normally.

Testing confirms that the moderation logic is accurate, reliable, and does not disrupt expected application behavior.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-content-moderation_cm3b0z2a)

### Testing with toxic messages

A message containing explicit and hateful language is submitted to the API. The system flags the message and stores it in the violations container instead of saving it as a normal message.

This demonstrates that Gemini integration is functioning correctly and that toxic content is being effectively filtered.

---

## Reviewing Violations in Cosmos DB

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-content-moderation_cm3d2b4c)

### Understanding violation metadata

Each violation record includes the original message text, the timestamp of the violation, the reason provided by Gemini, and the associated user ID.

This metadata enables auditing, pattern analysis, identification of repeat offenders, and provides a clear record of why moderation decisions were made.

---

## Building the Moderator Dashboard API

A Moderator Dashboard API is added to support human review of flagged content. While AI moderation is effective, human oversight is required to handle edge cases and maintain fairness.

The dashboard provides a centralized interface for reviewing and managing violations.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-content-moderation_smb2n4p8)

### Creating the GET /violations endpoint

A GET endpoint is implemented using Azure Functions to retrieve violations from Cosmos DB. The endpoint supports filtering by message content, timestamps, and severity.

Error handling ensures the API remains responsive even if database issues occur.

---

## Implementing Human-in-the-Loop Review

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-azure-content-moderation_smd4s6t0)

### How the review system works

Moderators submit review decisions through the PATCH endpoint. Each action is recorded with an audit trail that includes the moderator ID, timestamp, message ID, previous status, and new status.

This audit trail supports accountability, bias detection, compliance needs, and ensures moderation decisions are transparent and traceable.

---

## Project Wrap-Up

This project was completed to learn how to build a production-grade content moderation API using Gemini, Azure Functions, and Cosmos DB. It demonstrates how automated moderation, safe failure patterns, and human review work together in real systems.

A future area of learning is deploying similar systems using Azure DevOps pipelines for continuous delivery and governance.

---

---
