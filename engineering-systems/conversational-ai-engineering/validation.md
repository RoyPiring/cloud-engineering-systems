# Validation: Conversational AI Engineering

## Purpose

This document provides **objective validation evidence** that the conversational AI system behaves exactly as designed.

It records:
- What was tested
- What was expected
- What was observed
- Where the evidence exists

No rationale.  
No architecture explanation.  
No implementation detail.

---

## Validation Summary

| Domain | Status | Primary Evidence |
|--------|--------|------------------|
| Lex Bot Creation | PASS | 02-lex-bot-creation.md |
| Intent Definition | PASS | 03-lex-intent-slot-definition.md |
| Lambda Integration | PASS | 04-lex-lambda-integration.md |
| Testing and Deployment | PASS | 05-lex-testing-deployment.md |
| Advanced Conversations | PASS | 06-lex-advanced-conversations.md |

---

## Validation Scope

Validation covers:

- Amazon Lex bot creation and configuration
- Intent recognition and slot extraction
- Lambda function integration
- Context management and multi-turn conversations
- Fallback handling
- Testing and deployment

---

## Lex Bot Creation

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Bot creation | Bot created with intents and responses | The implementation was completed in a short, bounded timeframe | 02-lex-bot-creation.md |
| WelcomeIntent | Intent matches greeting utterances | Utterances such as "Hello" or "Hi" were used to validate that the WelcomeIntent is correctly matched and that the configured response is returned | 02-lex-bot-creation.md |
| FallbackIntent configuration | FallbackIntent handles unrecognized input | FallbackIntent responses were customized to provide guidance rather than default system messages | 02-lex-bot-creation.md |
| Confidence threshold | Intent selection based on confidence score | If the confidence score is below the defined threshold of 0.40, the system does not select a specific intent and instead routes the interaction to fallback handling | 02-lex-bot-creation.md |
| IAM role configuration | Bot assigned IAM role with least privilege | An IAM role was assigned to the bot with only the permissions required for Amazon Lex operation | 02-lex-bot-creation.md |

---

## Intent Definition

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Intent creation | Intents created with utterances | The intent is designed to handle account balance inquiries by requiring the relevant slot values before execution; this ensures the intent response logic operates only when all required contextual data has been collected | 03-lex-intent-slot-definition.md |
| Slot definition | Slots defined for data capture | Slots exist to extract required parameters from user input so intents can execute with complete and validated data; the configured slots allow users to provide specific attributes such as account type as part of natural language requests; slots were also configured to capture account balance related attributes | 03-lex-intent-slot-definition.md |
| Slot validation | Slot values validated correctly | The slot type configuration restricts accepted values to a predefined set, preventing unexpected or unsupported inputs from reaching the intent; failure prompts are configured to progressively request missing or invalid slot data using increasingly explicit guidance; the slot resolution configuration enables Lex to continue prompting for required values when they are omitted or ambiguous | 03-lex-intent-slot-definition.md |

---

## Lambda Integration

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Lambda function creation | Function processes intent requests | A Lambda function was implemented to process incoming intent requests and return a randomized numeric value | 04-lex-lambda-integration.md |
| Code hook configuration | Lex invokes Lambda via code hooks | Code hooks are configured within the Lex console at the intent level. Each hook specifies when execution occurs and which Lambda function is invoked | 04-lex-lambda-integration.md |
| Chatbot alias | Alias points to bot version | The chatbot alias was configured to point to the active bot version used for validation | 04-lex-lambda-integration.md |
| Lambda invocation | Lambda invoked successfully | The chatbot successfully invokes a Lambda function when users express interest in financial planning or investment topics | 04-lex-lambda-integration.md |
| Response handling | Lambda response returned to user | The response includes a randomized dollar figure generated at runtime, demonstrating dynamic response handling | 04-lex-lambda-integration.md |

---

## Testing and Deployment

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Context tag configuration | Context tags control intent activation | Context tags are used to control intent activation and conversational state within Lex | 05-lex-testing-deployment.md |
| Follow-up intent behavior | Follow-up intents execute when context present | When user details are collected and a balance inquiry is made within the active context window, the chatbot can respond appropriately | 05-lex-testing-deployment.md |
| Context expiry | Context expires after defined time | Requests made outside the required context fail by design, demonstrating explicit control over intent eligibility | 05-lex-testing-deployment.md |
| Multi-turn conversations | Conversations maintain state across turns | When user details are collected and a balance inquiry is made within the active context window, the chatbot can respond appropriately; context tags are used to control intent activation and conversational state within Lex; the context tag is applied to the UserInformation intent to indicate when user attributes have been successfully collected | 05-lex-testing-deployment.md |

---

## Advanced Conversations

| Test | Expected Result | Observed Result | Evidence |
|------|----------------|-----------------|----------|
| Advanced intent patterns | Complex conversation flows supported | The chatbot defines a single intent for simulated money transfers and uses multiple slots to capture structured input; slot reuse is applied to confirm sensitive values; the configuration exercises Lex capabilities such as intent recognition, slot prompting, conditional flow based on slot completion, and recovery from incomplete or unexpected input | 06-lex-advanced-conversations.md |
| Context management | Context managed across multiple intents | The visual builder is used to add Get slot value cards to the dialog flow; these cards control when and how the bot prompts for missing information and bind user responses to the appropriate slots; this ensures required data is collected before the intent can complete; after remediation, the intent correctly prompted for and captured all required values | 06-lex-advanced-conversations.md |

---

## Negative Testing Summary

| Scenario | Expected Result | Observed Result | Evidence |
|----------|----------------|-----------------|----------|
| Low confidence input | FallbackIntent triggered | FallbackIntent is invoked when no trained intent exceeds the confidence threshold | 02-lex-bot-creation.md |
| Missing context | Follow-up intent fails | Requests made outside the required context fail by design | 05-lex-testing-deployment.md |

---

## Evidence Map to Executions

| Validation Check | Execution File | Section Reference |
|-----------------|----------------|-------------------|
| Lex Bot Creation | `./executions/02-lex-bot-creation.md` | Bot creation and configuration |
| Intent Definition | `./executions/03-lex-intent-slot-definition.md` | Intent and slot definition |
| Lambda Integration | `./executions/04-lex-lambda-integration.md` | Lambda fulfillment integration |
| Testing and Deployment | `./executions/05-lex-testing-deployment.md` | Testing and deployment |
| Advanced Conversations | `./executions/06-lex-advanced-conversations.md` | Multi-turn conversation support |

---

## Known Limitations

- Validation performed in non-production environment
- Manual testing used for conversation validation
- Performance metrics not captured
- Cost observations not recorded
- Implementation completed in short, bounded timeframes

---

## Relationship to Other Documents

- **Business Requirements:** `business-context.md`
- **Design Intent:** `architecture.md`
- **Execution Record:** `implementation.md`

This document provides proof. Nothing more.

---

## Navigation

| Previous | Next |
|----------|------|
| [Implementation](./implementation.md) | [README](./README.md) |
