Project Architecture

Project

AI Lead/Data Classification Automation

---

1. Purpose

The system is designed to process unstructured lead information and convert it into structured, validated, qualified, and actionable lead data.

The system should reduce repetitive manual work while keeping important business decisions reviewable by humans.

The system is a portfolio project intended to demonstrate:

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

---

2. Core Principle

AI is responsible for interpretation and extraction.

Deterministic application logic is responsible for validation, qualification, state transitions, and other rules that should produce predictable results.

Humans remain responsible for important decisions when the system is uncertain or when an action has meaningful business consequences.

---

3. High-Level Architecture

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
 ┌───────────────────────┐
 │ Human Approval Needed?│
 └───────────┬───────────┘
             │
       Yes   │   No
        ↓    │    ↓
 Human Review│ Continue
        ↓    │
 Approval / Rejection
        ↓
 Persistence
        ↓
 Audit Log
        ↓
 Recommendation / Routing

---

4. Main Components

4.1 API Layer

Technology:

- FastAPI

Responsibilities:

- receive lead input
- expose application endpoints
- return structured responses
- provide API documentation
- connect the external interface with application services

The API layer should not contain the main business logic.

---

4.2 Input and Normalization Layer

Responsibilities:

- receive raw lead information
- normalize basic input
- clean obvious formatting inconsistencies
- create a consistent internal representation

Examples:

- normalize whitespace
- normalize empty values
- normalize basic contact information
- preserve the original input

The original input must remain available for auditing.

---

4.3 AI Layer

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
- decision-maker status
- pain points
- summary
- confidence

The AI must not invent information that is absent from the source.

Unknown information should be represented as "null" or another explicitly defined unknown state.

---

4.4 AI Provider Interface

The application should communicate with AI through an internal abstraction.

Application
     ↓
AI Interface
     ↓
AI Provider

This prevents the application from becoming tightly coupled to one AI provider.

A provider can be replaced without redesigning the entire application.

---

4.5 AI Output Validation

All AI-generated structured data must pass validation before entering downstream business logic.

Technology:

- Pydantic

Responsibilities:

- validate required fields
- validate data types
- validate allowed values
- reject malformed output
- prevent unexpected fields when appropriate

Invalid AI output must not silently continue through the workflow.

---

4.6 Qualification Engine

The qualification engine uses deterministic rules.

Example factors:

- business need
- budget
- timeline
- lead volume
- decision-maker status
- information-only intent
- unclear requirements

The initial scoring model is a prototype and may be changed after testing.

The engine should produce:

- score
- qualification category
- reasons
- recommended priority

The qualification result must be reproducible from the same input and rules.

---

4.7 Duplicate Detection

Responsibilities:

- detect possible duplicate leads
- compare relevant identifying information
- prevent unnecessary duplicate processing
- preserve existing records when appropriate

Duplicate detection should distinguish between:

- confirmed duplicate
- possible duplicate
- unique lead

The system should avoid destructive automatic merging when confidence is insufficient.

---

4.8 State Management

Each lead moves through defined processing states.

Initial conceptual states:

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

Failure states may be introduced where required.

State transitions must be explicit and testable.

---

4.9 Human Approval

Human approval is required when:

- the system is uncertain
- an important business decision cannot safely be automated
- duplicate detection is ambiguous
- a high-impact action requires confirmation

The system should present enough information for the human to understand why the lead reached the approval stage.

Possible actions:

- approve
- reject
- modify
- request further processing

---

4.10 Persistence Layer

Initial technology:

- SQLite
- SQLAlchemy

The persistence layer stores relevant information such as:

- lead records
- normalized data
- AI analysis
- qualification results
- processing state
- approval decisions
- audit information

The database implementation should remain replaceable if the project later requires PostgreSQL.

---

4.11 Audit Log

Important system events should be recorded.

Examples:

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

---

4.12 Failure and Recovery

The system must explicitly handle important failures.

Examples:

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
4. place the process in an appropriate state
5. allow recovery or human intervention when possible

---

5. Data Flow

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

The original raw input should remain distinguishable from transformed or AI-generated data.

---

6. Separation of Responsibilities

The system should maintain clear boundaries.

Responsibility| Primary Owner
Receiving input| API/Application
Normalization| Application
Interpretation| AI
Extraction| AI
Schema validation| Pydantic/Application
Qualification rules| Deterministic code
State transitions| Application
Duplicate detection| Application
Business approval| Human
Persistence| Database layer
Audit history| Application
Error handling| Application

---

7. Technology Baseline

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

Technology may be changed later only when evidence or project requirements justify the change.

---

8. Design Constraints

The project should prioritize:

1. correctness
2. reproducibility
3. simplicity
4. maintainability
5. testability
6. observability
7. clear separation of responsibilities

The project should not introduce complexity merely to make the architecture appear advanced.

---

9. Security and Configuration

Secrets must not be hardcoded into source code.

API keys and other credentials must be supplied through environment configuration or an equivalent secure mechanism.

Sensitive lead information should not be unnecessarily exposed in logs.

---

10. Testing Strategy

Testing should occur at multiple levels.

Unit Tests

Test individual components such as:

- normalization
- validation
- qualification rules
- duplicate detection
- state transitions

Integration Tests

Test interactions between:

- API and application services
- AI interface and provider
- application and database

End-to-End Tests

Test the complete lead processing flow from input to final state.

Failure Tests

Verify expected behavior when dependencies or inputs fail.

A feature should not be considered complete merely because its implementation exists.

Expected evidence progression:

IMPLEMENTED
    ↓
TESTED
    ↓
VERIFIED
    ↓
DONE

---

11. Architecture Evolution

The architecture is intentionally designed to support future expansion.

Potential future additions may include:

- multiple AI providers
- PostgreSQL
- external CRM integration
- email integration
- webhook triggers
- background processing
- analytics
- advanced routing
- agentic components

These should only be introduced when actual requirements justify them.

---

12. Source of Truth

The project uses different sources for different types of truth:

- Git repository → actual source code
- "PROJECT_STATE.md" → current execution position
- "EXECUTION_MAP.md" → planned project journey
- "AI_PROTOCOL.md" → AI execution rules
- "PROJECT_ARCHITECTURE.md" → intended system architecture
- "DECISIONS.md" → strategic decisions and their rationale

If these sources conflict, follow the conflict-handling rules in "AI_PROTOCOL.md".

---

13. Current Architectural Status

Architecture selected:

Stateful Workflow + AI + Deterministic Rules + Human Approval + Audit Log

Implementation status:

NOT IMPLEMENTED

The architecture is currently a design specification and must not be treated as evidence that the system has already been built.
