<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Add Custom Slots to a Lex Chatbot

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-ai-lex2)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

## Add Custom Slots to a Lex Chatbot

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex2_c4fc89af)

---

## Introducing Today's Project!

This project implements custom slot types in an Amazon Lex chatbot to extract structured user input and route requests based on specific attributes such as account type. The system uses slots to constrain and capture required data so intents can respond deterministically rather than relying on free-form text. The design focuses on improving input accuracy, reducing ambiguity, and enabling intent logic to operate on validated values instead of raw user messages.

### What is Amazon Lex?

Amazon Lex is a managed service for building conversational interfaces that performs automatic speech recognition and natural language understanding. In this project, Lex serves as the intent classification and slot extraction layer, translating user utterances into structured requests that downstream logic can reliably process. Its value here is enforcement of input constraints and predictable conversation flow rather than conversational richness.

### One thing I didn't expect in this project was...

The implementation highlighted how much behavioral control is driven by slot configuration rather than intent logic. Slot types, value constraints, and resolution behavior have a direct impact on conversation correctness, error handling, and system reliability.

### This project took me...

The implementation was completed within a short execution window, but the primary outcome was understanding how slot configuration decisions affect correctness, failure handling, and long-term maintainability of conversational systems.

---

## Slots

Slots exist to extract required parameters from user input so intents can execute with complete and validated data. They act as typed inputs to the intent, ensuring downstream logic receives values in an expected format and domain rather than free-text strings.

The configured slots allow users to provide specific attributes such as account type as part of natural language requests. This reduces follow-up clarification logic and enables the chatbot to return responses aligned to the provided context instead of generic replies.

Slots were also configured to capture account balance related attributes so the chatbot can identify which financial context the user is referencing without additional intent branching.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex2_97dc2351)

---

## Connecting slots with intents

The slot type configuration restricts accepted values to a predefined set, preventing unexpected or unsupported inputs from reaching the intent. This constraint improves intent reliability and reduces error handling complexity by enforcing valid input at the NLU layer.

The intent is designed to handle account balance inquiries by requiring the relevant slot values before execution. This ensures the intent response logic operates only when all required contextual data has been collected.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex2_c4fc89af)

---

## Slot values in utterances

Utterances reference slot placeholders so Lex can associate portions of user input with specific slot types. This mapping allows the system to bind values directly from natural language phrases into structured intent inputs without custom parsing logic.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex2_505be5b8)

---

## Handling failures in slot values

Failure prompts are configured to progressively request missing or invalid slot data using increasingly explicit guidance. This approach keeps the conversation active while enforcing data completeness requirements before intent fulfillment.

The slot resolution configuration enables Lex to continue prompting for required values when they are omitted or ambiguous. Adjusting the empty slot resolution behavior ensures the intent does not execute until all required inputs are collected, maintaining response correctness and predictable system behavior.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/aws-ai-lex2_a028bc8d2)

---

---

## Navigation

| Previous | Next |
|----------|------|
| [Lex Bot Creation](./02-lex-bot-creation.md) | [Lex Lambda Integration](./04-lex-lambda-integration.md) |
