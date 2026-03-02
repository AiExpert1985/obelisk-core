---
description: Archives a completed Obelisk task
---
Read the full conversation from this session.
Extract all relevant information to produce a complete, accurate archive.

---
## Guard

Verify the conversation contains a completed implementation before proceeding.
If no implementation is found → STOP. Output:
⛔ Nothing to archive. Complete implementation before running `@archive-task`.

---

## Recording Rules

**Contract:** Business invariant that must hold regardless of implementation — even after a full rebuild.
**Design:** How the system is built — tech, schema, architecture, patterns.
**History:** Intent and key decisions that shaped the task outcome.

Only record long-term, global decisions that shape the system broadly.
Skip anything local, obvious, or recoverable by reading the code.
A good entry answers "why" or "what was decided" — not "how it was implemented."

Ask:
- Would this decision matter if the system were rebuilt from scratch?
- Would a developer miss this by reading the code alone?

If no to both — skip it.

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

Append to `/obelisk/history/history-log.md`:

```markdown
## YYYYMMDD-HHMM | [Task Name] | TASK

[Concise summary of intent, key decisions, and outcomes]

---
```

---

## 3 — Update Contracts

If new or changed contracts exist, append to `contracts-summary.md → ## Unprocessed`:

```markdown
## YYYYMMDD-HHMM | [Task Name]

[Consolidated contract changes]

---
```

---

## 4 — Update Design

If new or changed design decisions exist, append to `design-summary.md → ## Unprocessed`:

```markdown
## YYYYMMDD-HHMM | [Task Name]

[Consolidated design decisions]

---
```
---

## 5 — Auto-Maintain Check

If `## Unprocessed` in either summary exceeds 50 lines:
Run `/obelisk-core/maintain-project.md`

---

Output:

✅ TASK ARCHIVED
/obelisk/history/completed/YYYYMMDD-HHMM-[task-name].md