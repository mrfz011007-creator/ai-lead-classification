# Project Architecture — AI Lead/Data Classification Automation

## 1. Purpose

The system processes unstructured lead information and converts it into structured, validated, qualified, and actionable lead data.

It is a portfolio project demonstrating:

- business problem understanding
- workflow design
- AI integration
- structured data processing
- deterministic business logic
- state management
- human approval
- persistence
- auditability
- testing
- failure handling

The architecture describes the intended product. It must not be confused with the V3.1 execution framework used to build and verify the product.

---

## 2. Core Principle

**AI interprets. Deterministic code controls predictable rules. Humans control important decisions.**

AI is responsible for interpretation and extraction.

Deterministic application logic is responsible for validation, qualification, state transitions, duplicate handling, and other predictable rules.

Humans remain responsible for important decisions when uncertainty or business consequences make automation inappropriate.

---

## 3. High-Level Architecture

```
Lead Input
    ↓
Input Normalization
    ↓
AI Analysis / Extraction
    ↓
AI Output Validation
    ↓
Qualification Engine
    ↓
Duplicate Detection
    ↓
State Management
    ↓
Human Approval if Required
    ↓
Persistence
    ↓
Audit Log
    ↓
Recommendation / Routing
```

The exact implementation may change only when requirements or evidence justify it.

---

## 4. Main Components

### 4.1 API Layer

**Technology:** FastAPI

Responsibilities:

- receive lead input
- expose application endpoints
- return structured responses
- provide API documentation
- connect the external interface with application services

The API layer should not contain the main business logic.

### 4.2 Input and Normalization Layer

Responsibilities:

- receive raw lead information
- normalize basic input
- clean obvious formatting inconsistencies
- create a consistent internal representation
- preserve original input for auditing

### 4.3 AI Layer

Responsibilities:

- interpret unstructured lead information
- extract relevant business information
- classify lead information
- summarize the lead
- identify uncertainty

Expected information may include:

- name
- company
- need
- intent
- category
- volume
- budget
- timeline
- decision-maker information
- pain points
- summary
- confidence

The AI must not invent information absent from the source. Unknown information should be represented explicitly as `null` or another defined unknown state.

### 4.4 AI Provider Interface

The application communicates with AI through an internal abstraction:

```
Application
    ↓
AI Interface
    ↓
AI Provider
```

This prevents tight coupling to one provider and allows replacement without redesigning application logic.

### 4.5 AI Output Validation

All AI-generated structured data must pass validation before entering downstream business logic.

**Technology:** Pydantic

Responsibilities:

- validate required fields
- validate data types
- validate allowed values
- reject malformed output
- prevent unexpected fields where appropriate

Invalid AI output must not silently continue.

### 4.6 Qualification Engine

The qualification engine uses deterministic rules.

Example factors:

- business need
- budget
- timeline
- lead volume
- decision-maker status
- information-only intent
- unclear requirements

The prototype produces:

- score
- qualification category
- reasons
- recommended priority

The scoring model is a V1 simulation and may change after testing.

### 4.7 Duplicate Detection

Responsibilities:

- detect possible duplicate leads
- compare relevant identifying information
- prevent unnecessary duplicate processing
- preserve existing records when appropriate

Distinguish:

- confirmed duplicate
- possible duplicate
- unique lead

Avoid destructive automatic merging when confidence is insufficient.

### 4.8 State Management

Conceptual states:

```
RECEIVED
  ↓
NORMALIZED
  ↓
ANALYZED
  ↓
VALIDATED
  ↓
QUALIFIED
  ↓
DUPLICATE_CHECKED
  ↓
AWAITING_APPROVAL
  ↓
APPROVED / REJECTED
  ↓
COMPLETED
```

Failure states may be introduced where required.

State transitions must be explicit and testable.

### 4.9 Human Approval

Human approval may be required when:

- the system is uncertain
- an important business decision cannot safely be automated
- duplicate detection is ambiguous
- a high-impact action requires confirmation

The system should present enough information for the human to understand why approval is required.

Possible actions:

- approve
- reject
- modify
- request further processing

### 4.10 Persistence Layer

Initial technology:

- SQLite
- SQLAlchemy

Stores relevant information such as:

- lead records
- normalized data
- AI analysis
- qualification results
- processing state
- approval decisions
- audit information

The database implementation should remain replaceable if PostgreSQL becomes justified.

### 4.11 Audit Log

Important system events should be recorded:

- lead received
- normalization completed
- AI analysis executed
- validation failed
- qualification calculated
- duplicate detected
- approval requested
- approval completed
- processing failed
- state changed

The audit log should make it possible to understand what happened to a lead and when.

### 4.12 Failure and Recovery

Expected failures include:

- AI provider unavailable
- timeout
- invalid AI response
- validation failure
- database failure
- duplicate detection conflict
- incomplete input

The system should:

1. detect the failure
2. preserve relevant information
3. record the failure
4. place processing in an appropriate state
5. allow recovery or human intervention when possible

---

## 5. Data Flow

```
Raw Lead
   ↓
Normalized Lead
   ↓
AI Analysis
   ↓
Validated Analysis
   ↓
Qualification
   ↓
Duplicate Detection
   ↓
Processing State
   ↓
Human Approval (if required)
   ↓
Stored Result
   ↓
Audit History
```

Original raw input must remain distinguishable from transformed or AI-generated data.

---

## 6. Separation of Responsibilities

| Responsibility | Primary Owner |
|---|---|
| Receiving input | API/Application |
| Normalization | Application |
| Interpretation | AI |
| Extraction | AI |
| Schema validation | Pydantic/Application |
| Qualification rules | Deterministic code |
| State transitions | Application |
| Duplicate detection | Application |
| Business approval | Human |
| Persistence | Database layer |
| Audit history | Application |
| Error handling | Application |

---

## 7. Technology Baseline

Initial stack:

- Python
- FastAPI
- Pydantic
- SQLAlchemy
- SQLite
- AI provider through an abstraction layer
- Pytest
- Git
- GitHub
- HTML/CSS/JavaScript for the initial interface

Technology changes require evidence or project requirements.

The runtime environment is intentionally separated from the architecture specification; the local Android environment is not assumed to support every dependency.

---

## 8. Design Constraints

Priorities:

1. correctness
2. reproducibility
3. simplicity
4. maintainability
5. testability
6. observability
7. clear separation of responsibilities

Do not introduce complexity merely to make the architecture appear advanced.

Future features such as agents, queues, background workers, external integrations, or multiple databases require an actual requirement or measurable benefit.

---

## 9. Security and Configuration

- never hardcode secrets
- supply API keys through environment configuration or an equivalent secure mechanism
- never commit `.env` containing secrets
- avoid unnecessarily exposing sensitive lead information in logs
- keep credentials out of tests, commits, and diagnostic output

---

## 10. Testing Strategy

### Unit Tests

Test components such as:

- normalization
- validation
- qualification rules
- duplicate detection
- state transitions

### Integration Tests

Test interactions between:

- API and application services
- AI interface and provider
- application and database

### End-to-End Tests

Test the complete lead-processing flow from input to final state.

### Failure Tests

Verify controlled behavior when dependencies or inputs fail.

### Evidence Gate

A feature progresses:

```
IMPLEMENTED
    ↓
TESTED
    ↓
VERIFIED
    ↓
DONE
```

Implementation alone is not completion evidence.

---

## 11. Architecture Evolution

Potential future additions:

- multiple AI providers
- PostgreSQL
- external CRM integration
- email integration
- webhook triggers
- background processing
- analytics
- advanced routing
- agentic components

These are deferred until actual requirements justify them.

---

## 12. Source of Truth

Different sources govern different truths:

- Git repository → actual source code
- `PROJECT_STATE.md` → current execution position
- `EXECUTION_MAP.md` → planned project journey
- `AI_PROTOCOL.md` → execution rules
- `PROJECT_ARCHITECTURE.md` → intended product architecture
- `DECISIONS.md` → strategic decisions and rationale
- runtime/test output → execution evidence

If sources conflict, follow the Conflict Gate in `AI_PROTOCOL.md`. Never silently select one source.

---

## 13. V3.1 Execution Boundary

This document defines the **product architecture**.

The V3.1 execution framework is separate:

```
ChatGPT — Director
    ↓
Codespaces — Runner
    ↓
GitHub — Source of Truth
```

The execution framework determines how the project is built and verified. It does not become part of the product unless a later requirement explicitly makes it a product feature.

---

## 14. Current Architectural Status

**Selected architecture:**

Stateful Workflow + AI + Deterministic Rules + Human Approval + Audit Log

**Implementation status:**

NOT IMPLEMENTED

This document is a design specification. Its existence is not evidence that the described components have already been built.

Current project execution position is maintained separately in `PROJECT_STATE.md`.
