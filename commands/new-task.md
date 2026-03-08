---
description: Creates and implements an Obelisk task
---


## Invocation Rule

If no task description is provided with this command:
**Output exactly:** "Describe your task"
**Do NOT** read files, run discovery, write code, or take any action.
**STOP**. Wait for user to provide task description before doing anything.


---

## Context

Read silently before asking for task description:
- `/obelisk/history/history-log.md`
- `/obelisk/contracts/contracts-log.md`
- `/obelisk-core/guidelines/ai-engineering.md`

If any missing → STOP. Output: Use `@init-project` to initialize the project.

---

## DISCOVERY — Mandatory

Discovery is never skippable. After receiving the full task description, you MUST present Questions before generating the Task Summary.

you MUST:
- Surface all non-trivial assumptions
- Ask clarifying questions on anything that would change execution

Do NOT ask about:
- Anything inferable from context, contracts, or design
- Implementation details you can decide yourself
- Low-impact edge cases

Inference from contracts, design, and existing patterns is allowed.
All non-trivial assumptions must be confirmed before proceeding.

If a contract change is detected:

``` markdown
📋 Contract Change

Type: ADD | UPDATE

Rule: [new contract rule]

If UPDATE:
Old: "[exact existing contract text]"

Reason: [why this rule is required]

Approve? yes/no
```

## Discovery Output Format

No narration. No thinking out loud. No filler.

```markdown
**Questions:**    
1. [question]    
   Recommendation: [option] — [reason]
```

If no questions exist: state **"No clarifications needed"** and list assumptions only.

If questions exist: **wait for answers before continuing**.

After answers — or if no questions exist — **generate the Task Summary**.

**Do NOT write code or analyze implementation during discovery.**

After the Task Summary → **STOP** and wait for `implement`.

---

## Task Summary

```markdown
Task Summary

Goal: [what and why]
Scope: ✓ [included] / ✗ [excluded]
Approach: [key design decisions]
Assumptions: [confirmed, or "None"]
Contracts: [new or changed, or "None"]
Constraints: [limits implementation must respect]
Risks: [known risks or "None"]
```

After presenting — STOP. You MUST NOT write code or modify files
Wait for corrections or `implement`.
If corrections received, update summary and STOP again.
Only proceed when `implement` is received.

---

## IMPLEMENTATION

Implement the agreed task. During implementation:
- Follow the agreed task summary
- Follow `/obelisk-core/guidelines/ai-engineering.md`
- Respect `/obelisk/contracts/contracts-log.md`

For any follow-up request or scope change:
- Treat it like a mini-discovery: understand the change, check against contracts and design, surface conflicts if any, confirm understanding before proceeding
- Do not implement changes blindly

When done, output:
```markdown
Implementation complete. Enter `@archive-task` to archive.
```