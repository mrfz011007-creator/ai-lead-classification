# Execution Map — AI Lead/Data Classification Automation

## Target

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

# V3.1 Execution Contract

## Execution Cycle

The AI follows:

`READ STATE → IDENTIFY NEXT ACTION → CHECK GATES → EXECUTE → TEST → EVALUATE EVIDENCE → UPDATE STATE → CHECK STOP CONDITIONS → CONTINUE OR STOP`

The AI may execute multiple steps in one cycle.

There is no arbitrary step-count stop.

## Lazy Context Loading

Default context:

1. `PROJECT_STATE.md`
2. relevant section of this map
3. relevant `AI_PROTOCOL.md` rules
4. `PROJECT_ARCHITECTURE.md` when architecture is relevant
5. `DECISIONS.md` when decisions are relevant
6. only the source files required for the current action

Expand context when evidence reveals a conflict or missing information.

## Stop Conditions

Execution stops only at:

- `DECISION_REQUIRED`
- `CONFLICT`
- `BLOCKED`
- `BUDGET_EXHAUSTED`
- `TARGET_COMPLETE`

Completing an ordinary step is not itself a stop condition.

## Evidence Gate

Every step follows:

`TODO → IMPLEMENTED → TESTED → VERIFIED → DONE`

A step is DONE only when its implementation, relevant tests/checks, acceptance criteria, and state documentation are verified.

## Decision Gate

A Decision Gate is required only for:

- strategic direction
- architecture or scope changes
- material tradeoffs
- irreversible actions
- business information that cannot safely be inferred

Before stopping, complete independent work, verify it, update state, and record the required decision.

## Conflict Gate

If state, repository, architecture, or decisions disagree:

1. detect
2. collect evidence
3. check existing decisions
4. resolve automatically when determinable
5. otherwise stop as `CONFLICT`

Never silently choose between conflicting sources.

## Execution Budget

Execution may be bounded by:

```yaml
budget:
  max_steps: null
  max_tool_calls: null
  max_retries: null
  max_runtime_minutes: null
```

Budget is a safety boundary, not a progress target.

When exhausted, preserve work, update `PROJECT_STATE.md`, record the exact stop reason, and stop.

## Git Checkpoint

Preferred cycle:

`KNOWN GOOD COMMIT → MODIFY → TEST → PASS → COMMIT`

Use recoverable checkpoints after verified milestones. Do not create a branch for every step.

---

# PHASE 1 — DISCOVERY

## Step 1 — Select Real Problem

**Objective**

Identify a concrete business problem from LinkedIn suitable for a portfolio project.

**Status**

DONE

**Result**

Selected problem:

Unstructured lead information requires repetitive manual interpretation, qualification, prioritization, routing, and storage.

**Evidence**

LinkedIn problem research and documented problem pattern.

**Next Step**

Step 2

---

## Step 2 — Problem Definition

**Objective**

Define the problem precisely enough to build against it.

**Status**

DONE

**Exit Criteria**

- problem clearly defined
- affected workflow identified
- repetitive work identified
- expected value identified

**Next Step**

Step 3

---

## Step 3 — Business Simulation

**Objective**

Create a realistic business context for the project.

**Status**

DONE

**Result**

A B2B software/automation agency receives prospective client inquiries and needs to process and qualify them efficiently.

**Next Step**

Step 4

---

# PHASE 2 — SYSTEM DESIGN

## Step 4 — System Requirements

**Objective**

Define what the system must do.

**Status**

DONE

**Core Requirements**

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

**Next Step**

Step 5

---

## Step 5 — Architecture Selection

**Objective**

Choose the system architecture.

**Status**

DONE

**Selected Architecture**

Stateful Workflow + AI + Deterministic Rules + Human Approval + Audit Log

**Principle**

AI interprets unstructured information.

Deterministic logic controls predictable business rules.

Human approval handles uncertain or important decisions.

The system maintains state and an audit trail.

**Next Step**

Step 6

---

## Step 6 — Technology Stack

**Objective**

Select the initial implementation stack.

**Status**

DONE

**Initial Stack**

- Python
- FastAPI
- Pydantic
- LLM API through an abstraction layer
- SQLite initially
- SQLAlchemy
- Pytest
- HTML/CSS/JavaScript for a simple interface
- Git/GitHub

**Design Principle**

The AI provider must be replaceable without rewriting application logic.

**Next Step**

Step 7

---

# PHASE 3 — PROJECT FOUNDATION

## Step 7 — Repository and Project Setup

**Objective**

Create the initial project structure and establish a reproducible development baseline.

**Status**

DONE

**Entry Condition**

Steps 1–6 complete.

**Actions**

1. create or select the project repository
2. define project structure
3. initialize application foundation
4. configure dependency declarations
5. configure environment handling
6. create initial documentation
7. create initial tests
8. establish Git history
9. synchronize the repository with GitHub
10. verify the repository baseline

**Auto Execute**

YES

**User Decision Required**

Only if repository ownership, licensing, or another strategic project-level decision is unresolved.

**Exit Criteria**

- repository exists
- project structure exists
- application foundation exists
- dependency declarations exist
- environment template exists
- baseline test exists
- Git history exists
- repository is synchronized
- project state is documented

Runtime execution of the full Python stack is verified separately in the appropriate Linux/Codespaces environment.

**Evidence**

- repository: `mrfz011007-creator/ai-lead-classification`
- initial project foundation commit exists
- V3.1 protocol committed
- `PROJECT_STATE.md` updated
- GitHub repository synchronized

**Next Step**

Step 8

---

# PHASE 4 — DATA FOUNDATION

## Step 8 — Lead Data Model

**Objective**

Define the internal representation of a lead and its processing state.

**Status**

TODO

**Actions**

- define lead schema
- define normalized fields
- define nullable fields
- define processing status
- define validation rules
- create model tests

**Auto Execute**

YES

**User Decision Required**

Only if the data model reveals a significant business ambiguity that cannot be resolved technically.

**Exit Criteria**

Lead data model is implemented, tested, and validated against representative examples.

**Evidence Required**

Schema tests and representative examples.

**Next Step**

Step 9

---

## Step 9 — Input and Normalization Layer

**Objective**

Convert raw lead input into a consistent internal format.

**Actions**

- define input format
- normalize values
- handle missing fields
- validate input
- handle malformed input
- create tests

**Auto Execute**

YES

**Exit Criteria**

Valid and invalid inputs are handled predictably.

**Evidence Required**

Automated tests.

**Next Step**

Step 10

---

# PHASE 5 — AI PROCESSING

## Step 10 — AI Extraction Layer

**Objective**

Use an LLM to interpret unstructured lead information and produce structured data.

**Expected Output**

Examples:

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

**Rules**

- never invent missing information
- represent unavailable information as null
- use structured output
- validate output against schema
- isolate provider-specific code

**Auto Execute**

YES

**User Decision Required**

Only if provider, cost, privacy, or another strategic constraint requires a user decision.

**Exit Criteria**

Representative inputs produce valid structured outputs.

**Evidence Required**

Automated validation and representative test cases.

**Next Step**

Step 11

---

## Step 11 — AI Output Validation

**Objective**

Ensure AI-generated data cannot directly corrupt downstream processing.

**Actions**

- schema validation
- type validation
- required-field validation
- invalid-output handling
- retry/failure strategy where appropriate

**Auto Execute**

YES

**Exit Criteria**

Invalid AI output is detected and handled safely.

**Evidence Required**

Positive and negative tests.

**Next Step**

Step 12

---

# PHASE 6 — BUSINESS LOGIC

## Step 12 — Qualification Engine

**Objective**

Apply deterministic business rules to classify and prioritize leads.

**Principle**

AI extracts information.

Rules determine qualification.

**Initial Example**

- clear business need: +20
- budget known: +20
- timeline clear: +20
- significant volume: +15
- decision maker identified: +15
- information-only inquiry: -20
- unclear need: -20

**Initial Classification**

- 80–100: HOT
- 50–79: WARM
- 0–49: COLD

These values are a V1 simulation and are not universal business rules.

**Auto Execute**

YES

**User Decision Required**

Only if business rules require strategic business judgment.

**Exit Criteria**

Given the same input, the qualification engine produces deterministic results.

**Evidence Required**

Unit tests covering scoring boundaries and edge cases.

**Next Step**

Step 13

---

## Step 13 — Duplicate Detection

**Objective**

Detect potentially duplicated leads before creating conflicting records.

**Actions**

- define duplicate signals
- implement matching logic
- distinguish exact and potential duplicates
- test false-positive scenarios

**Auto Execute**

YES

**Exit Criteria**

Duplicate detection behaves predictably on representative cases.

**Evidence Required**

Automated tests.

**Next Step**

Step 14

---

# PHASE 7 — STATE AND HUMAN CONTROL

## Step 14 — Stateful Processing

**Objective**

Track the lead through the processing lifecycle.

**Example States**

`RECEIVED → NORMALIZED → ANALYZED → VALIDATED → QUALIFIED → ROUTED → APPROVAL_REQUIRED → APPROVED → COMPLETED`

Failure states must also be represented.

**Auto Execute**

YES

**Exit Criteria**

State transitions are explicit, valid, and testable.

**Evidence Required**

State transition tests.

**Next Step**

Step 15

---

## Step 15 — Human Approval

**Objective**

Allow human intervention when the system should not act automatically.

**Actions**

- identify approval conditions
- expose relevant information
- allow approval/rejection
- preserve decision history

**Auto Execute**

YES

**User Decision Required**

Only if an actual product-level approval policy is unresolved.

**Exit Criteria**

The system can pause processing, request approval, record the decision, and continue.

**Evidence Required**

Approval workflow test.

**Next Step**

Step 16

---

# PHASE 8 — STORAGE AND AUDIT

## Step 16 — Persistence

**Objective**

Persist leads, processing state, qualification results, and relevant metadata.

**Auto Execute**

YES

**Exit Criteria**

Data survives application restart and can be retrieved correctly.

**Evidence Required**

Persistence tests.

**Next Step**

Step 17

---

## Step 17 — Audit Log

**Objective**

Record important processing events so the system can explain what happened.

**Record Examples**

- input received
- AI analysis performed
- validation result
- qualification result
- duplicate detection
- state transition
- human approval
- failure/retry

**Auto Execute**

YES

**Exit Criteria**

Important processing events are traceable.

**Evidence Required**

Audit-log test.

**Next Step**

Step 18

---

# PHASE 9 — FAILURE HANDLING

## Step 18 — Failure and Recovery

**Objective**

Make the system resilient to expected failures.

**Cases**

- invalid input
- invalid AI output
- API failure
- timeout
- rate limit
- duplicate
- database failure
- unexpected exception

**Auto Execute**

YES

**Exit Criteria**

Expected failures produce controlled behavior rather than silent corruption.

**Evidence Required**

Failure-path tests.

**Next Step**

Step 19

---

# PHASE 10 — INTERFACE AND INTEGRATION

## Step 19 — Application Interface

**Objective**

Provide a simple interface for submitting and reviewing leads.

**Auto Execute**

YES

**Exit Criteria**

A user can submit a lead and inspect the resulting processing information.

**Evidence Required**

Working end-to-end demonstration.

**Next Step**

Step 20

---

## Step 20 — End-to-End Integration

**Objective**

Connect the complete pipeline.

**Flow**

`Raw Lead → Normalize → AI Analysis → Validate → Qualify → Duplicate Check → Store → Route / Approval → Audit`

**Auto Execute**

YES

**Exit Criteria**

The complete flow works with representative scenarios.

**Evidence Required**

End-to-end tests and demonstration.

**Next Step**

Step 21

---

# PHASE 11 — VERIFICATION

## Step 21 — System Testing

**Objective**

Verify the system as a whole.

**Actions**

- unit tests
- integration tests
- failure tests
- edge cases
- representative business scenarios

**Auto Execute**

YES

**Exit Criteria**

All defined acceptance criteria are satisfied or explicitly documented.

**Evidence Required**

Test results.

**Next Step**

Step 22

---

## Step 22 — Portfolio Documentation

**Objective**

Document the project as evidence of engineering ability.

**Documentation**

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

**Auto Execute**

YES

**Exit Criteria**

Another developer can understand the project and reproduce the core result.

**Evidence Required**

Complete repository documentation.

**Next Step**

Step 23

---

# PHASE 12 — FINAL VERIFICATION

## Step 23 — Target Verification

**Objective**

Determine whether the original project target has actually been achieved.

**Verification**

Check every target requirement from the beginning of this map.

**Auto Execute**

YES

**Exit Criteria**

All required capabilities are implemented, tested, verified, and documented.

**Evidence Required**

Final verification checklist and test results.

**Result**

If all criteria pass:

`COMPLETED`

Otherwise:

Return to the relevant step.

---

# Completion Contract

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

The final state must be reproducible from the GitHub repository.

