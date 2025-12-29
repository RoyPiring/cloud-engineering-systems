# Architecture: Conversational AI Engineering

## Quick Orientation

**Scope:** Conversational AI applications using Amazon Lex with multi-turn conversations, including intent design, slot definition, Lambda integration, and deployment strategies.

**Non-Goals:**
- Custom NLP model training
- Advanced conversation analytics beyond basic patterns
- Multi-language bot implementations
- Voice-only bot deployments

**Key Tradeoffs:**
- **Service Selection:** Amazon Lex (managed, integrated) vs. Custom NLP (more control, higher complexity)
- **Intent Design:** Broad intents (simpler) vs. Specific intents (more accurate)
- **Integration:** Lambda fulfillment (dynamic) vs. Direct backend (simpler, less flexible)
- **Deployment:** Single version (simpler) vs. Versioned aliases (production-ready, more complex)

**Diagram:** See [Architecture Patterns](#architecture-patterns) section below for visual representations.

---

## System Design

This system covers implementation of conversational AI using Amazon Lex, from bot creation to advanced multi-turn conversations.

## Core Components

### 1. Amazon Lex
- Natural language understanding (NLU)
- Intent recognition and slot extraction
- Conversation state management
- Bot versioning and aliases

### 2. Intent and Slot Design
- Intent definition for user goals
- Slot definition for entity extraction
- Prompt design for slot elicitation
- Confirmation and fulfillment patterns

### 3. Lambda Integration
- Dynamic response generation
- Backend system integration
- Business logic processing
- Data retrieval and processing

### 4. Deployment Channels
- Web chat integration
- Voice integration
- Messaging platform integration
- Custom application integration

## Architecture Patterns

### Pattern 1: Basic Lex Bot
```
User Input → Amazon Lex → Intent Recognition → Response → User
```

### Pattern 2: Lambda-Enhanced Bot
```
User Input → Lex → Intent + Slots → Lambda Function → Dynamic Response → User
```

### Pattern 3: Multi-Turn Conversation
```
User → Lex → Intent → Context Tag → Follow-Up Intent → Lambda → Response → User
```

### Pattern 4: Context-Aware Bot
```
User Input → Lex → Context Check → Intent Validation → Lambda → State Update → Response
```

## Design Decisions

- Service selection (Lex vs. custom NLP)
- Intent and slot design principles
- Integration patterns (Lambda vs. direct)
- Deployment and versioning strategies

---

## Failure Model

**What fails:** Lex intent misclassification, Lambda timeout, backend service unavailability, conversation state loss, slot validation failures

**How it fails:** Lex misclassifies user intent causing wrong response; Lambda exceeds 5-second timeout; backend API returns errors; conversation state not persisted; slot validation rejects valid input

**Blast Radius:** Intent misclassification affects single conversation turn; Lambda timeout affects that fulfillment; backend failure affects all conversations using that integration; state loss affects conversation continuity; slot failure affects that specific conversation flow

**Recovery:** Fallback intents handle misclassification; Lambda timeout retries with shorter operations; backend circuit breakers prevent cascade; conversation state persisted in DynamoDB; slot validation provides user feedback for correction

## Security Model

**Trust Boundaries:** User boundary (untrusted input); Lex boundary (validated intents); Lambda boundary (trusted fulfillment); backend boundary (authenticated services)

**IAM Model:** Least-privilege IAM roles for Lambda functions; Lex service role limited to required permissions; no cross-service over-privilege; DynamoDB access scoped to conversation state

**Encryption:** TLS for all API communications; conversation state encrypted at rest in DynamoDB; no PII in logs; secrets in Secrets Manager

**Audit Trail:** CloudWatch Logs for all Lambda executions (30-day retention); Lex conversation logs; DynamoDB access logs; CloudTrail for all AWS API calls; conversation metrics in CloudWatch

## Cost Model

**Primary Drivers:** Lex text processing ($0.004 per text request = ~$15/month for moderate usage), Lambda ($0.20 per 1M requests + compute = ~$3/month), DynamoDB ($0.25 per million reads = ~$2/month), CloudWatch ($0.50/GB logs = ~$3/month)

**Guardrails:** Budget alert at $35/month; Lex requests limited to 10K/month; Lambda concurrency limited to 100; DynamoDB on-demand mode; conversation state retention limited to 30 days

**Expected Monthly Range:** $20-30/month for lab environment with moderate usage (5K-10K conversations, standard Lambda usage, minimal DynamoDB storage, standard logging)

## Constraints

**Policy:** Single language (English); no custom NLP model training; managed services only

**Org:** Team expertise in Lex and Lambda; no advanced conversation analytics; basic multi-turn support

**Cost Ceiling:** Conversational AI infrastructure budget <$40/month for lab environment

**Latency:** Bot response must be <3 seconds p95; Lambda timeout set to 5 seconds; Lex processing <1 second

**Data Classification:** Handles user conversation data; requires data privacy compliance; no PII storage beyond session

**Regions:** Single region deployment (us-east-1 for Lex service availability)

## Quality Goals (Detailed)

1. **Conversation Quality** - How judged: Intent recognition accuracy >90% (tested with sample utterances); slot filling accuracy >95%; multi-turn context retention validated; fallback handling tested for unrecognized intents

2. **Response Latency** - How judged: Bot response time <2 seconds p95 (measured from user input to response); Lambda fulfillment completes in <1 second; Lex processing time <500ms; total end-to-end <2000ms

3. **Reliability** - How judged: Bot availability >99.9% (measured via health checks); Lambda error rate <1%; conversation state preserved across sessions; graceful error handling for backend failures

4. **Cost Efficiency** - How judged: Lex text processing costs <$20/month for moderate usage; Lambda invocation costs <$5/month; total bot infrastructure <$30/month; cost per conversation <$0.01

5. **User Experience** - How judged: Conversation flows complete successfully >95% of the time; user satisfaction measured via conversation completion rates; natural language understanding validated with diverse test cases

---

## Navigation

| Previous | Next |
|----------|------|
| [Business Context](./business-context.md) | [Implementation](./implementation.md) |

