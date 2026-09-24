AI Execution Protocol

Purpose

This file defines how the AI must execute the project.

The AI's objective is to move the project toward the defined target while minimizing unnecessary user interaction.

---

1. Start of Every Run

Before taking any project action, the AI must:

1. Read "PROJECT_STATE.md".
2. Read "EXECUTION_MAP.md".
3. Read "PROJECT_ARCHITECTURE.md" if it exists.
4. Read "DECISIONS.md" if it exists.
5. Inspect the actual repository state when necessary.

The AI must not assume the current project state from conversation memory alone.

---

2. Determine Current Position

The AI must identify:

- current phase
- current step
- current objective
- current status
- completed work
- unresolved problems
- next valid action

If the documented state conflicts with the actual repository state, enter "CONFLICT" handling instead of silently choosing one.

---

3. Autonomous Execution

The AI should execute automatically whenever:

- the next action is already defined
- no strategic user decision is required
- the action is reversible or routine
- required information is available
- the action can be verified

The AI should continue through multiple steps in one run.

There is no arbitrary step limit.

---

4. Decision Gates

The AI must stop only when a genuine user decision is required.

Examples:

- choosing between materially different architectures
- changing an established project direction
- accepting a significant tradeoff
- making an irreversible decision
- deciding something that cannot reasonably be determined from technical evidence

Before stopping:

1. Complete all work that does not depend on the decision.
2. Verify completed work.
3. Update "PROJECT_STATE.md".
4. Record the required decision.
5. Clearly state the available options and their consequences.

---

5. Routine Technical Decisions

The AI may make routine technical decisions autonomously when they do not materially change the project's direction.

The AI should prefer:

- simpler solutions
- maintainable solutions
- reversible decisions
- solutions consistent with the existing architecture
- evidence-based choices

The AI must not turn every technical choice into a user decision.

---

6. Evidence Gate

A task must not be marked "DONE" merely because implementation exists.

The expected progression is:

"IMPLEMENTED → TESTED → VERIFIED → DONE"

Evidence may include:

- successful tests
- validated output
- working integration
- reproducible behavior
- documented verification

---

7. Blocked State

If progress cannot continue because of:

- missing access
- missing required information
- unavailable dependency
- external failure
- unresolved technical conflict

the AI must:

1. finish all independent work possible
2. update "PROJECT_STATE.md"
3. mark the relevant step "BLOCKED"
4. explain the exact blocker
5. stop

---

8. Conflict Handling

If project documentation conflicts with actual code, architecture, or repository state:

- do not silently overwrite either source
- identify the conflict
- determine whether it can be resolved from existing decisions
- if not, create a Decision Gate

The actual repository state is evidence of what currently exists.
Project documentation describes the intended state.

---

9. State Updates

After meaningful progress, the AI must keep "PROJECT_STATE.md" synchronized with reality.

Before stopping, the state must accurately describe:

- where the project is
- what was completed
- what remains
- why execution stopped
- what action should happen next

---

10. Completion

The AI may mark the project "COMPLETED" only when all target completion criteria in "EXECUTION_MAP.md" are satisfied and verified.

Never claim completion based solely on implementation.

---

11. User Interaction

The user should primarily be involved in:

- strategic decisions
- important tradeoffs
- irreversible choices
- final acceptance

The AI should handle routine execution, implementation, testing, debugging, documentation, and verification whenever possible.
