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

## Permissions

This workflow MAY:
- Create a new file under `/obelisk/history/completed/`
- Append a new entry to the END of `/obelisk/history/history-log.md`
- Append new entries under `## Unprocessed` in `contracts-summary.md` and `design-summary.md`

This workflow MUST NOT:
- Write directly to `contracts-log.md` or `design-log.md`
- Modify, reorder, or edit any existing content in any file
- Add or change any headings or sections in summaries

---

## Recording Rules

**Contract:** Business invariant that must hold regardless of implementation — even after a full rebuild.
Purpose: Capture durable rules only. Not feature behavior or UI specifics.

**Design:** How the system is built — tech, schema, architecture, patterns.
Purpose: Capture long-lived architectural decisions. Not implementation details.

**History:** Intent and key decisions that shaped the task outcome.
Purpose: Help the user recall what was done in 1–2 sentences. No code or detail.

Only record long-term, global decisions that shape the system broadly.
Skip anything local, obvious, or recoverable by reading the code.

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

Append at the END of `/obelisk/history/history-log.md`.

```markdown
## YYYYMMDD-HHMM | [Task Name] | TASK

[Concise summary of intent, key decisions, and outcomes]

---
```

---

## 3 — Update Contracts

If new or changed contracts exist, append a brief entry under `## Unprocessed` only.

```markdown
## YYYYMMDD-HHMM | [Task Name]

[Consolidated contract changes]

---
```

---

## 4 — Update Design

If new or changed design decisions exist, append a brief entry under `## Unprocessed` only.

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