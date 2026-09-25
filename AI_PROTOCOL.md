# AI Execution Protocol — V3.1

## 1. Purpose

V3.1 defines how AI executes the project toward its target with bounded autonomy, verification, recoverability, and minimal unnecessary user interaction.

Core rule:

> Human controls direction. AI handles routine execution within that direction.

This protocol governs the **execution process**, not the product architecture.

---

## 2. Roles

- **ChatGPT — Director:** reasoning, planning, review, diagnosis, decisions, and verification.
- **Codespaces — Runner:** terminal execution, code changes, tests, and Git operations.
- **GitHub — Source of Truth:** repository code, history, and project-state files.

Chat history is not a source of truth for exact project state.

---

## 3. Source of Truth

Use the following authority:

| Information | Source |
|---|---|
| Source code | Git repository |
| Current execution position | `PROJECT_STATE.md` |
| Project journey | `EXECUTION_MAP.md` |
| Execution rules | `AI_PROTOCOL.md` |
| Product architecture | `PROJECT_ARCHITECTURE.md` |
| Strategic decisions | `DECISIONS.md` |
| Runtime evidence | Tests, command output, repository state |

If sources conflict, enter **CONFLICT** handling.

---

## 4. Start of Every Execution Cycle

Before acting:

1. Read `PROJECT_STATE.md`.
2. Read the relevant section of `EXECUTION_MAP.md`.
3. Read `AI_PROTOCOL.md` when protocol interpretation is needed.
4. Read `PROJECT_ARCHITECTURE.md` when architecture is relevant.
5. Read `DECISIONS.md` when a decision may affect the action.
6. Inspect only the source files and runtime state needed for the current action.

Use **lazy context loading**. Do not load the entire project unnecessarily.

---

## 5. Execution Cycle

Every cycle follows:

`READ STATE → IDENTIFY NEXT ACTION → CHECK GATES → EXECUTE → TEST → EVALUATE EVIDENCE → UPDATE STATE → CHECK STOP CONDITIONS → CONTINUE OR STOP`

The AI should continue through multiple project steps when the next actions are determinable.

There is **no arbitrary step-count stop**.

---

## 6. Bounded Autonomous Execution

AI may execute automatically when:

- the next action is defined
- required information is available
- no strategic decision is required
- the action is routine or reversible
- the result can be verified
- execution remains within the current budget

Routine technical choices should not be escalated unnecessarily.

Prefer simple, maintainable, reversible, architecture-consistent solutions.

---

## 7. Execution Budget

A work cycle may define a safety budget:

```yaml
budget:
  max_steps: null
  max_tool_calls: null
  max_retries: null
  max_runtime_minutes: null
```

Budget values are execution boundaries, **not progress targets**.

If a budget is exhausted:

1. stop safely
2. preserve the current work
3. update `PROJECT_STATE.md`
4. record the exact stop reason
5. resume from that state later

Never create artificial work merely to consume a budget.

---

## 8. Stop Conditions

AI stops only when one of these conditions is reached:

- `DECISION_REQUIRED`
- `CONFLICT`
- `BLOCKED`
- `BUDGET_EXHAUSTED`
- `TARGET_COMPLETE`

Completing one ordinary step is **not** by itself a reason to stop.

---

## 9. Decision Gate

Stop for a genuine user decision involving:

- architecture or project direction
- scope changes
- material tradeoffs
- irreversible actions
- business assumptions that cannot be determined technically

Before stopping:

1. finish independent work
2. test completed work
3. update `PROJECT_STATE.md`
4. record the decision required in `DECISIONS.md` when appropriate
5. present the relevant options and consequences

Do not stop merely because a routine technical choice exists.

---

## 10. Conflict Gate

If state, code, architecture, or decisions disagree:

1. detect the conflict
2. collect sufficient evidence
3. check existing decisions
4. resolve automatically if the correct resolution is determinable
5. otherwise mark the state as `CONFLICT` and stop

Never silently overwrite conflicting information.

---

## 11. Evidence Gate

A task progresses through:

`TODO → IMPLEMENTED → TESTED → VERIFIED → DONE`

Definitions:

- **IMPLEMENTED:** implementation exists.
- **TESTED:** relevant test or check has run.
- **VERIFIED:** acceptance criteria are satisfied.
- **DONE:** verified and project state/documentation are synchronized.

Implementation alone is never sufficient for `DONE`.

---

## 12. Diagnostic Evidence

Evidence must be **minimally sufficient**, not maximally verbose.

For a PASS, record:

- what was checked
- result

For a FAIL, retain enough information to diagnose:

- command or test
- exit code when available
- failed test/check
- error type
- important error message
- relevant traceback or output

Do not hide failure evidence merely to keep output short.

---

## 13. Failure Recovery

When execution fails:

`FAIL → DIAGNOSE → ISOLATE → REPAIR → RETEST`

AI may self-repair when the repair is:

- technically determinable
- non-strategic
- reversible or low-risk
- within budget
- verifiable

If not, enter `BLOCKED` or `CONFLICT`.

Do not repeatedly retry an unchanged failing action.

---

## 14. Git Checkpoints

Use Git as the recovery mechanism.

Preferred pattern:

`KNOWN GOOD COMMIT → MODIFY → TEST → PASS → COMMIT`

If modification fails, restore or revert to a known-good state when appropriate.

Do not create a temporary branch for every project step.

Create checkpoints after verified milestones.

Never use destructive Git operations blindly.

---

## 15. State Maintenance

`PROJECT_STATE.md` is the project's execution GPS.

It must answer:

- Where am I?
- What is done?
- What is current?
- What is blocked?
- What is next?
- Why did execution stop?
- What is the current budget/status?

Update state after meaningful progress and **before every stop**.

---

## 16. Complexity Rule

Do not introduce:

- extra agents
- subagents
- queues
- databases
- orchestration layers
- autonomous loops
- dependencies
- infrastructure

unless a real requirement or measurable benefit justifies them.

Prefer the simplest system that satisfies the requirement.

---

## 17. Resource Awareness

Account for:

- Android device limitations
- Codespaces quota
- runtime availability
- LLM context/token usage
- network reliability
- API cost

Use resources efficiently:

- lazy-load context
- batch compatible work
- avoid idle runtime
- avoid unnecessary tool calls
- prioritize acceptance criteria
- defer optional features when resources are constrained

---

## 18. Security

Never:

- commit API keys or secrets
- commit real `.env` files
- expose credentials in logs
- hard-code secrets into source

Use environment variables or the runtime's secret mechanism.

---

## 19. Completion Contract

The project may be marked `COMPLETED` only when the target requirements are:

1. implemented
2. tested
3. verified
4. documented
5. reproducible

The AI must not claim completion from implementation alone.

---

## 20. Human vs AI Responsibility

### Human

- strategic direction
- business assumptions
- major tradeoffs
- irreversible decisions
- final acceptance

### AI

- routine implementation
- testing
- debugging
- documentation
- verification
- state maintenance
- routine technical decisions

The execution system should minimize unnecessary user interaction without removing strategic human control.

---

## 21. V3.1 Core Rules

1. **State before action.**
2. **Evidence before DONE.**
3. **Human controls strategy.**
4. **AI controls routine execution.**
5. **Never silently resolve conflicts.**
6. **Continue until a real stop condition.**
7. **Budget limits execution; it does not define progress.**
8. **Preserve enough evidence to diagnose failures.**
9. **Git provides recoverable checkpoints.**
10. **Prefer the simplest system that satisfies the requirement.**
