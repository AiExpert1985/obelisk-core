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

## Permissions

This workflow MAY:
- Create a new file under `/obelisk/history/completed/`
- Append a new entry to the END of `/obelisk/history/history-log.md`
- Append new entries to the end of in `/obelisk/contracts/contracts-summary.md` 
- Append new entries to the end of in `/obelisk/design/design-summary.md` 

This workflow MUST NOT:
- Modify, reorder, or edit any existing content in any file

---

## Definitions

**Contract:** Business invariant that must hold regardless of implementation — even after a full rebuild. Capture durable rules only — not feature behavior or UI specifics.

**Design:** Project-level or feature-level architectural decisions that shape how the system is built broadly. Skip UI tweaks, visual changes, single-screen fixes, library API details, or anything recoverable from code.

**History:** Concise summary of what was done and why. No code, no implementation detail.

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

**Task:** [Concise summary of user request and the agreed goal after discovery.]

**Design:** [Architectural or feature-level decisions agreed during discovery.
Record only decisions that would matter if the system were rebuilt. Omit if none.]

**Contracts:** [Business rules or invariants introduced or changed. Must hold regardless of implementation. Omit if none. Use the exact format below — copy rule text verbatim from the approved Contract Change block in discovery:]

Contract Change: ADD
Rule: [exact rule text]

Contract Change: UPDATE
Old: "[exact previous rule text]"
New: [exact updated rule text]

**Rejected:** [Approaches, contracts, or design decisions explicitly rejected during discovery and why.
Omit if none.]

---
```

### Rules

- Be concise — one to three sentences per field maximum
- High-level only — no code, UI details, pixel values, or method names
- No repetition — capture each decision once, in the most relevant field
- Omit fields that do not apply — do not leave blank fields
- Rejected Capture explicitly discarded approaches and the reason — prevents revisiting dead ends.
- Contracts must use the exact wording approved during discovery — no paraphrasing. Copy the rule text verbatim from the discovery Contract Change block.

---

## 3 — Update Contracts

If new or changed contracts exist, append to the end of `contracts-summary.md`:
```markdown
YYYYMMDD-HHMM | [Task Name] | [Copy contract entry from history-log — no rewording]
```

---

## 4 — Update Design

If new or changed design decisions exist, , append to the end of`## New` in `design-summary.md`:
```markdown
YYYYMMDD-HHMM | [Task Name] | [Copy design entry from history-log — no rewording]
```

---


Output:

✅ TASK ARCHIVED
/obelisk/history/completed/YYYYMMDD-HHMM-[task-name].md