---
description: Auto-execute task until the end
---
## Required Files

- `/obelisk/workspace/task.md`
- `/obelisk-core/guidelines/ai-engineering.md`

If any are missing → STOP and report path.

---

## IMPLEMENTATION PHASE

### Execution Rules

MUST:

- Implement strictly according to `task.md` (Goal, Scope, Execution Strategy)
- Respect all Constraints listed in task.md (contracts, design principles, technical limits)
- Stay within the Affected Area defined in task.md
- Log any divergence

MUST NOT:

- Reinterpret, redesign, or expand scope
- Silently correct or redesign errors in task.md
- Ask questions (use STOP instead)

---

### STOP Conditions

STOP immediately if:

- A requirement cannot be achieved without new decisions
- A change would violate a constraint listed in task.md
- Completing a step requires architectural or scope decisions not in task.md
- Continuing would risk irreversible or unsafe changes
- You are uncertain whether a change is mechanical

STOP is terminal. No further execution is allowed.

---

### Allowed Mechanical Adaptations (No STOP)

Proceed only if intent and observable behavior remain unchanged:

- Minor renames
- Import adjustments
- Formatting / whitespace
- Syntax or API alignment to actual code state
- Defensive checks consistent with existing patterns

Log any such adaptation.

---

### Implementation Notes

Append to `/obelisk/workspace/task.md` under `## Implementation Notes`:

```markdown
## Implementation Notes

### Execution Summary
[What was done. If exact match to plan, state so.]

### Divergences
- Specified: [X]
- Actual: [Y]
- Reason: [mechanically necessary because...]

(If none: "Implemented as specified. No divergences.")
```

---

## Review Phase

For every ✔ provide evidence: file path + function/class, code snippet, or precise observed logic. Vague statements are not evidence.

Append to `/obelisk/workspace/task.md` under `## Review-notes`:

```markdown
## Review

**Status:** APPROVED | REJECTED

1. Goal Achieved: ✔ | ✗ — [evidence]
2. Constraints Preserved: ✔ | ✗ — [evidence]
3. Scope Preserved: ✔ | ✗ — [evidence]

**Files Modified:** [list]
**Notes:** [mechanical divergences or observations only]
```

---

### Status Gate

**If REJECTED:**

1. Append to `/obelisk/history/history-log.md`:

```markdown
## YYYYMMDD-HHMM | [Task Name] | REJECTED

[Discovery Summary from task.md — copied exactly]

---
```

2. Copy `task.md` to `/obelisk/history/rejected/YYYYMMDD-HHMM-[task-name].md`
3. Clear `/obelisk/workspace/`

Output:

```
⚠️ TASK CLOSED — REJECTED
Archived: /obelisk/history/rejected/YYYYMMDD-HHMM-[task-name].md
```

STOP.

---

**If APPROVED:**

#### 1 — Write History

Append to `/obelisk/history/history-log.md`:

```markdown
## YYYYMMDD-HHMM | [Task Name] | APPROVED

[Discovery-Summary from task.md — copied exactly]

---
```

---

#### 2 — Apply Contract Changes

If `task.md` has `## Contract-Changes` section:

Append to `/obelisk/contracts/contracts-summary.md` → `## Unprocessed`:

```markdown
## YYYYMMDD-HHMM | [Task Name]

[Contract-Changes content — copied exactly, do not modify]

---
```

---

#### 3 — Apply Design Changes

If `task.md` has `## Design-Changes` section:

Append to `/obelisk/design/design-summary.md` → `## Unprocessed`:

```markdown
## YYYYMMDD-HHMM | [Task Name]

[Design-Changes content — copied exactly, do not modify]

---
```

---

#### 4 — Archive Task

Copy `task.md` to `/obelisk/history/completed/YYYYMMDD-HHMM-[task-name].md` Clear `/obelisk/workspace/`

---

## Auto-Maintain

If `contracts-summary.md → ## Unprocessed` contains ≥ 10 entries or `design-summary.md → ## Unprocessed` contains ≥ 10 entries

→ Run `/obelisk-core/prompts/maintain-project.md`

---

## Output

```
✅ TASK CLOSED — APPROVED
Archived: /obelisk/history/completed/YYYYMMDD-HHMM-[task-name].md
```

STOP.