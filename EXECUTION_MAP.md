Execution Map

Project

AI Lead/Data Classification Automation

Target

Build and verify a portfolio-ready lead management automation system that can:

1. receive unstructured lead information
2. normalize the input
3. extract structured information using AI
4. validate the AI output
5. qualify and prioritize leads using deterministic rules
6. detect potential duplicates
7. store lead data and processing results
8. recommend routing or next action
9. support human approval where required
10. maintain an auditable processing history
11. handle important failure cases
12. demonstrate the system with reproducible tests and evidence

---

Execution Rules

Each step contains:

- Objective
- Actions
- Entry Condition
- Exit Criteria
- Auto Execute
- User Decision Required
- Evidence Required
- Next Step

The AI should execute consecutive steps automatically when no user decision is required.

The AI must not stop merely because a step has been completed.

The AI should continue until:

- a genuine Decision Gate is reached
- the project is Blocked
- the Target Completion Criteria are satisfied

---

PHASE 1 — DISCOVERY

Step 1 — Select Real Problem

Objective

Identify a concrete business problem from LinkedIn that is suitable for a portfolio project.

Status

DONE

Result

Selected problem:

Unstructured lead information requires repetitive manual interpretation, qualification, prioritization, routing, and storage.

Evidence

LinkedIn problem research and documented problem pattern.

Next Step

Step 2

---

Step 2 — Problem Definition

Objective

Define the problem precisely enough to build against it.

Status

DONE

Exit Criteria

- problem clearly defined
- affected workflow identified
- repetitive work identified
- expected value identified

Next Step

Step 3

---

Step 3 — Business Simulation

Objective

Create a realistic business context for the project.

Status

DONE

Result

Simulation:

A B2B software/automation agency receives prospective client inquiries and needs to process and qualify them efficiently.

Next Step

Step 4

---

PHASE 2 — SYSTEM DESIGN

Step 4 — System Requirements

Objective

Define what the system must do.

Status

DONE

Core Requirements

- receive lead input
- normalize data
- analyze lead using AI
- extract structured fields
- validate output
- qualify lead
- prioritize lead
- detect duplicates
- store results
- recommend action/routing
- support human approval
- maintain audit history
- handle failures

Next Step

Step 5

---

Step 5 — Architecture Selection

Objective

Choose the system architecture.

Status

DONE

Selected Architecture

Stateful Workflow + AI + Deterministic Rules + Human Approval + Audit Log

Principle

AI interprets unstructured information.

Deterministic logic controls predictable business rules.

Human approval handles uncertain or important decisions.

The system maintains state and an audit trail.

Next Step

Step 6

---

Step 6 — Technology Stack

Objective

Select the initial implementation stack.

Status

DONE

Initial Stack

- Python
- FastAPI
- Pydantic
- LLM API through an abstraction layer
- SQLite initially
- SQLAlchemy
- Pytest
- HTML/CSS/JavaScript for a simple interface
- Git/GitHub

Design Principle

The AI provider must be replaceable without rewriting the application logic.

Next Step

Step 7

---

PHASE 3 — PROJECT FOUNDATION

Step 7 — Repository and Project Setup

Objective

Create the initial project structure and establish a reproducible development baseline.

Entry Condition

Steps 1–6 are complete.

Actions

1. Create or select the project repository.
2. Define project structure.
3. Initialize application.
4. Configure dependencies.
5. Configure environment handling.
6. Create initial documentation.
7. Create initial tests.
8. Run the project.
9. Verify the baseline.
10. Commit the working baseline.

Auto Execute

YES

User Decision Required

Only if repository ownership, repository choice, licensing, or another strategic project-level decision is unresolved.

Exit Criteria

- repository exists
- project structure exists
- application starts
- dependencies resolve
- baseline test runs
- repository state is clean and documented
- initial commit exists

Evidence Required

- repository state
- successful application startup
- successful baseline test
- commit

Next Step

Step 8

---

PHASE 4 — DATA FOUNDATION

Step 8 — Lead Data Model

Objective

Define the internal representation of a lead and its processing state.

Actions

- define lead schema
- define normalized fields
- define nullable fields
- define processing status
- define validation rules
- create model tests

Auto Execute

YES

User Decision Required

Only if the data model reveals a significant business ambiguity that cannot be resolved technically.

Exit Criteria

Lead data model is implemented and validated.

Evidence Required

Schema tests and representative examples.

Next Step

Step 9

---

Step 9 — Input and Normalization Layer

Objective

Convert raw lead input into a consistent internal format.

Actions

- define input format
- normalize values
- handle missing fields
- validate input
- handle malformed input
- create tests

Auto Execute

YES

Exit Criteria

Valid and invalid inputs are handled predictably.

Evidence Required

Automated tests.

Next Step

Step 10

---

PHASE 5 — AI PROCESSING

Step 10 — AI Extraction Layer

Objective

Use an LLM to interpret unstructured lead information and produce structured data.

Expected Output

Examples include:

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

Rules

- never invent missing information
- represent unavailable information as null
- use structured output
- validate output against schema
- isolate provider-specific code

Auto Execute

YES

User Decision Required

Only if provider, cost, privacy, or another strategic constraint requires a user decision.

Exit Criteria

Representative inputs produce valid structured outputs.

Evidence Required

Automated validation and representative test cases.

Next Step

Step 11

---

Step 11 — AI Output Validation

Objective

Ensure AI-generated data cannot directly corrupt downstream processing.

Actions

- schema validation
- type validation
- required-field validation
- invalid-output handling
- retry/failure strategy where appropriate

Auto Execute

YES

Exit Criteria

Invalid AI output is detected and handled safely.

Evidence Required

Positive and negative tests.

Next Step

Step 12

---

PHASE 6 — BUSINESS LOGIC

Step 12 — Qualification Engine

Objective

Apply deterministic business rules to classify and prioritize leads.

Principle

AI extracts information.

Rules determine qualification.

Initial Example

- clear business need: +20
- budget known: +20
- timeline clear: +20
- significant volume: +15
- decision maker identified: +15
- information-only inquiry: -20
- unclear need: -20

Initial classification:

- 80–100: HOT
- 50–79: WARM
- 0–49: COLD

These values are a V1 simulation and must not be treated as universal business rules.

Auto Execute

YES

User Decision Required

Only if business rules require a strategic business judgment.

Exit Criteria

Given the same input, the qualification engine produces deterministic results.

Evidence Required

Unit tests covering scoring boundaries and edge cases.

Next Step

Step 13

---

Step 13 — Duplicate Detection

Objective

Detect potentially duplicated leads before creating conflicting records.

Actions

- define duplicate signals
- implement matching logic
- distinguish exact and potential duplicates
- test false-positive scenarios

Auto Execute

YES

Exit Criteria

Duplicate detection behaves predictably on representative cases.

Evidence Required

Automated tests.

Next Step

Step 14

---

PHASE 7 — STATE AND HUMAN CONTROL

Step 14 — Stateful Processing

Objective

Track the lead through the processing lifecycle.

Example States

RECEIVED
→ NORMALIZED
→ ANALYZED
→ VALIDATED
→ QUALIFIED
→ ROUTED
→ APPROVAL_REQUIRED
→ APPROVED
→ COMPLETED

Failure states must also be represented.

Auto Execute

YES

Exit Criteria

State transitions are explicit, valid, and testable.

Evidence Required

State transition tests.

Next Step

Step 15

---

Step 15 — Human Approval

Objective

Allow human intervention when the system should not act automatically.

Actions

- identify approval conditions
- expose relevant information
- allow approval/rejection
- preserve decision history

Auto Execute

YES

User Decision Required

Only if an actual product-level approval policy is unresolved.

Exit Criteria

The system can pause processing, request approval, record the decision, and continue.

Evidence Required

Approval workflow test.

Next Step

Step 16

---

PHASE 8 — STORAGE AND AUDIT

Step 16 — Persistence

Objective

Persist leads, processing state, qualification results, and relevant metadata.

Auto Execute

YES

Exit Criteria

Data survives application restart and can be retrieved correctly.

Evidence Required

Persistence tests.

Next Step

Step 17

---

Step 17 — Audit Log

Objective

Record important processing events so the system can explain what happened.

Record Examples

- input received
- AI analysis performed
- validation result
- qualification result
- duplicate detection
- state transition
- human approval
- failure/retry

Auto Execute

YES

Exit Criteria

Important processing events are traceable.

Evidence Required

Audit-log test.

Next Step

Step 18

---

PHASE 9 — FAILURE HANDLING

Step 18 — Failure and Recovery

Objective

Make the system resilient to expected failures.

Cases

- invalid input
- invalid AI output
- API failure
- timeout
- rate limit
- duplicate
- database failure
- unexpected exception

Auto Execute

YES

Exit Criteria

Expected failures produce controlled behavior rather than silent corruption.

Evidence Required

Failure-path tests.

Next Step

Step 19

---

PHASE 10 — INTERFACE AND INTEGRATION

Step 19 — Application Interface

Objective

Provide a simple interface for submitting and reviewing leads.

Auto Execute

YES

Exit Criteria

A user can submit a lead and inspect the resulting processing information.

Evidence Required

Working end-to-end demonstration.

Next Step

Step 20

---

Step 20 — End-to-End Integration

Objective

Connect the complete pipeline.

Flow

Raw Lead
→ Normalize
→ AI Analysis
→ Validate
→ Qualify
→ Duplicate Check
→ Store
→ Route / Approval
→ Audit

Auto Execute

YES

Exit Criteria

The complete flow works with representative scenarios.

Evidence Required

End-to-end tests and demonstration.

Next Step

Step 21

---

PHASE 11 — VERIFICATION

Step 21 — System Testing

Objective

Verify the system as a whole.

Actions

- unit tests
- integration tests
- failure tests
- edge cases
- representative business scenarios

Auto Execute

YES

Exit Criteria

All defined acceptance criteria are satisfied or explicitly documented.

Evidence Required

Test results.

Next Step

Step 22

---

Step 22 — Portfolio Documentation

Objective

Document the project as evidence of engineering ability.

Documentation

- problem
- why it matters
- system architecture
- technical decisions
- implementation
- AI role
- deterministic logic
- human approval
- failure handling
- testing
- limitations
- future improvements

Auto Execute

YES

Exit Criteria

Another developer can understand the project and reproduce the core result.

Evidence Required

Complete repository documentation.

Next Step

Step 23

---

PHASE 12 — FINAL VERIFICATION

Step 23 — Target Verification

Objective

Determine whether the original project target has actually been achieved.

Verification

Check every target requirement from the beginning of this map.

Auto Execute

YES

Exit Criteria

All required capabilities are implemented, tested, verified, and documented.

Evidence Required

Final verification checklist and test results.

Result

If all criteria pass:

"COMPLETED"

Otherwise:

Return to the relevant step.

---

Decision Gate Rules

A Decision Gate may interrupt execution at any step when:

1. a strategic choice is required
2. two or more materially different valid paths exist
3. the choice changes architecture or project direction
4. required business information cannot be inferred safely
5. the decision is irreversible or expensive to reverse

The AI must not create a Decision Gate merely because a technical choice exists.

---

Completion Criteria

The project is complete only when:

- core functionality works
- AI extraction works
- AI output is validated
- deterministic qualification works
- duplicate handling works
- state management works
- human approval works
- persistence works
- audit logging works
- expected failures are handled
- end-to-end processing works
- tests provide evidence
- documentation explains the system
- portfolio evidence is reproducible
