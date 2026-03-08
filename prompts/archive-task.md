---
description: Archives a completed Obelisk task
---
## Guard

Verify before proceeding that the conversation contains a completed task, which is:
- User described a task
- User requested implementation
- Implementation was performed in this session

If any of the above is missing → STOP. Output:
⛔ Nothing to archive. Complete implementation before running `@archive-task`.

---

## 1 — Write Task File

Create `/obelisk/history/completed/YYYYMMDD-HHMM-[task-name].md`:

```markdown
# Task: [One-line descriptive name]

## Summary
[What was done and why — 2-4 sentences]

## Scope
✓ Included: [list]
✗ Excluded: [list]

## Design Decisions
[Approach and technical choices made during discovery and implementation]

## New or Changed Contracts
[Contracts added or modified, or "None"]

## Constraints
[Limits that were respected during implementation]

## Risks & Notes
[What was noted or discovered during implementation]
```

---

## 2 — Update History

Append at the END of `/obelisk/history/history-log.md`.


```markdown
## YYYYMMDD-HHMM | [Task Name] | TASK

**Task:** [Concise summary of user request and the agreed goal after discovery. what was done and why. No code, no implementation detail]

**Rejected:** [Concise summary of Approaches, contracts, or design decisions explicitly rejected during discovery and why.Omit if none.]

---
```

### Rules

- Be concise — one to three sentences per field maximum
- **High-level only** — no code, UI details, pixel values, method names, or implementation specifics recoverable from reading the code.
- No repetition — capture each decision once, in the most relevant field
- Omit fields that do not apply — do not leave blank fields
- Rejected Capture explicitly discarded approaches and the reason — prevents revisiting dead ends.

---

## 3 — Update Contracts Log

If contract changes exist, append to END of `/obelisk/contracts/contracts-log.md`:

```markdown
YYYYMMDD-HHMM | [Task Name] | ADD
Rule: [exact rule text as approved in discovery]

YYYYMMDD-HHMM | [Task Name] | UPDATE
Old: "[exact previous rule text]"
New: [exact updated rule text]

YYYYMMDD-HHMM | [Task Name] | REMOVE
Rule: "[exact rule text removed]"
```

Rules:
- Copy rule text verbatim from the approved Contract Change block. Never paraphrase.
- Business rules or invariants introduced or changed. Must hold regardless of implementation.
- Skip if there is no contract change

---



Output:

✅ TASK ARCHIVED
/obelisk/history/completed/YYYYMMDD-HHMM-[task-name].md