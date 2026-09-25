# Project Decisions

**Project:** AI Lead/Data Classification Automation

---

## Purpose

This file records decisions that affect architecture, direction, scope, or significant tradeoffs.

Routine technical choices do not need to be recorded unless they materially affect the project.

Strategic decisions belong here. Current execution position belongs in `PROJECT_STATE.md`.

---

## Decision 001 — Architecture

**Decision**

Use:

**Stateful Workflow + AI + Deterministic Rules + Human Approval + Audit Log**

**Reason**

AI is useful for interpretation and extraction, while important business logic should remain predictable, testable, and controllable.

Human approval is retained for uncertain or high-impact cases.

**Alternatives considered**

- Linear workflow
- Fully agentic architecture

**Status**

ACCEPTED

---

## Decision 002 — AI Responsibility

**Decision**

AI is primarily responsible for:

- interpretation
- information extraction
- classification
- summarization
- identifying uncertainty

Deterministic application logic is responsible for:

- validation
- qualification
- state transitions
- duplicate handling
- other reproducible business rules

**Reason**

Rules that should be reproducible should not depend unnecessarily on probabilistic AI behavior.

**Status**

ACCEPTED

---

## Decision 003 — Human Approval

**Decision**

The system must support human approval for uncertain or important cases.

**Reason**

The system should automate useful work without removing human control over meaningful business decisions.

**Status**

ACCEPTED

---

## Decision 004 — AI Provider Abstraction

**Decision**

The application communicates with AI through an internal provider interface rather than coupling application logic directly to one provider.

**Reason**

Provider changes should not require redesigning the application.

**Status**

ACCEPTED

---

## Decision 005 — Initial Database

**Decision**

Use SQLite with SQLAlchemy for the initial implementation.

**Reason**

The project is a prototype and portfolio system. A lightweight database avoids unnecessary infrastructure while preserving a migration path toward PostgreSQL if requirements justify it.

**Status**

ACCEPTED

---

## Decision 006 — Initial Technology Stack

**Decision**

Initial stack:

- Python
- FastAPI
- Pydantic
- SQLAlchemy
- SQLite
- Pytest
- Git
- GitHub
- HTML/CSS/JavaScript
- AI provider through an abstraction layer

**Reason**

The stack provides the capabilities required by the project while remaining manageable and testable.

**Status**

ACCEPTED

---

## Decision 007 — Evidence-Based Completion

**Decision**

A feature or project step is not complete merely because implementation exists.

Required progression:

**IMPLEMENTED → TESTED → VERIFIED → DONE**

**Reason**

The project must demonstrate engineering evidence, not merely source-code production.

**Status**

ACCEPTED

---

## Decision 008 — Complexity Policy

**Decision**

Do not introduce architectural complexity unless an actual requirement, technical limitation, or measurable benefit justifies it.

**Reason**

The project should demonstrate useful engineering rather than complexity for its own sake.

**Status**

ACCEPTED

---

## Decision 009 — Repository

**Decision**

Use the public GitHub repository:

`mrfz011007-creator/ai-lead-classification`

**Reason**

GitHub is the source of truth for source code, history, and project-state documents.

The repository was established and synchronized during Step 7.

**Status**

ACCEPTED

---

## Decision 010 — Execution Framework

**Decision**

Use the frozen V3.1 execution contract as the framework for building and verifying the project.

Core model:

```
ChatGPT — Director
Codespaces — Runner
GitHub — Source of Truth
```

**Reason**

The project benefits from bounded autonomous execution while keeping strategic decisions under human control.

The execution framework is separate from the product architecture.

**Status**

ACCEPTED

---

## Decision 011 — Runtime Environment

**Decision**

Use GitHub Codespaces as the primary Linux runtime for the Python/FastAPI project.

Termux remains useful for lightweight Android-side Git/file operations but is not treated as the required runtime for the full dependency stack.

**Reason**

The required Python dependency stack has Android/Termux compatibility constraints. A Linux development environment avoids forcing unsupported native builds on the phone.

**Status**

ACCEPTED

---

## Decision 012 — State and Execution Sources of Truth

**Decision**

Use the following separation:

- Git repository → actual source code and history
- `PROJECT_STATE.md` → current execution position
- `EXECUTION_MAP.md` → project journey and gates
- `AI_PROTOCOL.md` → execution rules
- `PROJECT_ARCHITECTURE.md` → intended product architecture
- `DECISIONS.md` → strategic decisions and rationale
- runtime/test output → execution evidence

**Reason**

Separating these responsibilities prevents chat history or one document from becoming an overloaded and unreliable source of truth.

**Status**

ACCEPTED

---

## Decision 013 — Bounded Autonomous Execution

**Decision**

The AI may continue through routine, reversible, technically determinable, and verifiable work without requesting permission at every step.

Execution stops only at:

- `DECISION_REQUIRED`
- `CONFLICT`
- `BLOCKED`
- `BUDGET_EXHAUSTED`
- `TARGET_COMPLETE`

**Reason**

Stopping after every step creates unnecessary interaction overhead. Unlimited execution without control gates creates unnecessary risk.

**Status**

ACCEPTED

---

## Decision Recording Rule

Add a decision here only when it:

- changes project direction
- selects between materially different approaches
- creates an important tradeoff
- is difficult to reverse
- significantly affects architecture or scope
- establishes an execution policy that should remain stable

Routine implementation details belong in code, tests, or technical documentation.

---

## Current Strategic Decisions

The following are currently fixed:

1. Product architecture: stateful workflow with AI, deterministic rules, human approval, and audit log.
2. AI is primarily an interpretation/extraction layer.
3. Important business logic remains deterministic.
4. Human approval remains available for meaningful uncertainty or impact.
5. AI provider access is abstracted.
6. Initial database is SQLite + SQLAlchemy.
7. Completion requires evidence.
8. Complexity requires justification.
9. GitHub repository is `mrfz011007-creator/ai-lead-classification`.
10. V3.1 is the frozen execution framework.
11. Codespaces is the primary Linux runtime.
12. GitHub and the five Markdown files have defined source-of-truth roles.
