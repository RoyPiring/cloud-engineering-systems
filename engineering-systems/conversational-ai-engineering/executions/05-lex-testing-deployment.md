<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Save User Info with a Lex Chatbot

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-ai-lex4)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Save User Info with a Lex Chatbot

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex4_505be5b8)

---

## Introducing Today's Project!

### What is Amazon Lex?

This project implements an Amazon Lex chatbot designed to capture and retain limited user-provided attributes during a conversational session. The system demonstrates controlled state handling across multi-turn interactions, with a focus on intent scoping and context propagation rather than persistent storage.

Amazon Lex is a managed service for building conversational interfaces using text or voice input. In this implementation, Lex provides intent recognition, slot extraction, and context management to support deterministic conversation flows without custom natural language processing logic.

### How I used Amazon Lex in this project

The chatbot is configured to collect user identifiers such as name, email address, and preferred contact method through structured slots. Context is used to temporarily associate these values with the active conversation, enabling subsequent intents to reference prior inputs within defined boundaries.

### One thing I didn't expect in this project was...

Context expiry behavior materially affects conversational continuity. Misaligned expiry values can prematurely invalidate follow-up intents or allow stale assumptions to persist, directly impacting response accuracy and user flow control

### This project took me...

The implementation was scoped as a short, focused build to validate intent chaining, slot capture, and context expiry behavior. Effort was concentrated on configuration correctness rather than external integrations or backend fulfillment logic.

---

## Context Tags

Context tags are used to control intent activation and conversational state within Lex. They serve as explicit gates that determine when downstream intents are eligible to execute based on prior interactions.

Personal and community tag classifications are organizational labels rather than runtime controls. In this project, tagging supports internal categorization of intents and associated context usage.

The context tag is applied to the UserInformation intent to indicate when user attributes have been successfully collected. This context allows subsequent intents to reference captured slot values during the same conversational window.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex4_97dc2351)

---

## FollowUpCheckBalance

This intent is designed to operate only after a balance-related interaction has occurred. It exists to demonstrate conditional follow-up behavior based on previously established conversational context rather than unsolicited intent triggering.

The intent relationship enforces sequencing. Follow-up responses are permitted only when the prerequisite intent has executed and established the required context, preventing invalid or out-of-order requests.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex4_12345678)

---

## Input Context Tag

The input context contextCheckBalance acts as a hard dependency for the FollowUpCheckBalance intent. Without this context, the intent is intentionally suppressed to maintain predictable conversational logic.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex4_c4fc89af)

---

## The final result!

When user details are collected and a balance inquiry is made within the active context window, the chatbot can respond appropriately

Requests made outside the required context fail by design, demonstrating explicit control over intent eligibility.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex4_505be5b8)

---

## Managing context expiry

Context expiry defines how long conversational state remains valid. It constrains how long captured data and intent eligibility persist before being automatically cleared.

The shortened expiry window limits how long follow-up intents can execute after the initial interaction. This configuration highlights the tradeoff between conversational flexibility and protection against outdated or sensitive context reuse.

Longer expiry supports extended, multi-turn interactions where continuity is required. It is appropriate when user input remains valid over time and follow-up actions are expected.

Short expiry reduces the risk of acting on stale or sensitive information. It is appropriate for time-bound data or workflows where assumptions must reset quickly to preserve correctness.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex4_81b763822)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Lex Lambda Integration](./04-lex-lambda-integration.md) | [Lex Advanced Conversations](./06-lex-advanced-conversations.md) |
