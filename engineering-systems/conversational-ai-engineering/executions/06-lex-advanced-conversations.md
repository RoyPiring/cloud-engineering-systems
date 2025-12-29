<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up Multiple Slots in a Lex Chatbot

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-ai-lex5)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Build a Chatbot with Multiple Slots

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex5_67890123)

---

## Introducing Today's Project!

### What is Amazon Lex?

This project implements a basic conversational interface using Amazon Lex to demonstrate intent handling with multiple required slots. The system accepts natural language input, extracts structured values, and enforces completion of required data before progressing. The purpose is to validate how Lex manages multi-slot intents and conversational flow without custom backend logic.

Amazon Lex is a managed service for building conversational interfaces using text or voice input. It provides intent classification, slot extraction, and dialog management. In this project, Lex is used as the primary control plane for conversation state and user input validation.

### How I used Amazon Lex in this project

The chatbot defines a single intent for simulated money transfers and uses multiple slots to capture structured input. Slot reuse is applied to confirm sensitive values. Infrastructure is provisioned through CloudFormation to ensure repeatability. The Lex visual builder is used to define prompts and slot elicitation logic without custom code.

### One thing I didn't expect in this project was...

The implementation highlighted how much conversational logic can be expressed directly through Lex configuration. Slot elicitation, validation, and flow control were handled within the service, reducing the need for external processing while still supporting non-trivial interaction patterns.

### This project took me...

Approximately two hours, covering template creation, deployment, validation, and correction of configuration gaps discovered during testing.

---

## TransferFunds

The TransferFunds intent represents a transactional request that requires multiple discrete inputs. Slots are defined for source account, destination account, and transfer amount. The intent does not execute real transfers and is scoped strictly to data capture and confirmation.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex5_67890123)

---

## Using multiple slots

Reusing slot types enables confirmation of critical values by requesting the same data more than once.

This approach reduces ambiguity in user input and demonstrates how Lex can enforce data consistency at the conversation layer.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex5_97dc2351)

---

## Exploring Lex features

The configuration exercises Lex capabilities such as intent recognition, slot prompting, conditional flow based on slot completion, and recovery from incomplete or unexpected input.

The project remains configuration-driven and avoids custom fulfillment logic.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex5_12345678)

---

## AWS CloudFormation

CloudFormation is used to define and deploy the Lex bot and its associated resources as infrastructure as code.

This ensures consistent environments across deployments and allows the chatbot configuration to be version-controlled.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex5_c4fc89af)

---

## The final result!

Testing identified a missing slot type definition in the TransferFunds intent. The issue was corrected by defining the required slot types and redeploying the bot.

After remediation, the intent correctly prompted for and captured all required values

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex5_505be5b8)

---

## Using the visual builder

The visual builder is used to add Get slot value cards to the dialog flow.

These cards control when and how the bot prompts for missing information and bind user responses to the appropriate slots. This ensures required data is collected before the intent can complete.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex5_9cac15cd4)

---

---

## Navigation

| Previous |
|----------|
| [Lex Testing Deployment](./05-lex-testing-deployment.md) |
