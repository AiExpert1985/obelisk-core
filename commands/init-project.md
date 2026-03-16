---
description: Initialize new Obelisk project
---
## Guard

Check that none of these exist:
- `/obelisk/contracts/contracts-log.md`
- `/obelisk/history/history-log.md`

If any exist → STOP. Output:
⛔ Project already initialized. Remove existing obelisk state before re-initializing.

---

## PROJECT INPUT

Ask the user exactly this before proceeding:
"Describe your project, or provide a path to a design document."

If a path is provided → read the document silently, extract what's relevant, acknowledge what was understood, then ask only about what the document does not cover.
If a description is provided → proceed to discovery questions directly.

---

## DISCOVERY

Have a natural conversation to understand the project. Keep it focused and brief —
ask only the most important questions, group related ones together, and stop as soon
as sufficient understanding is reached. User can type `initialize` at any point to
skip remaining questions and initialize with what has been collected so far
(not recommended — more context produces better contracts and design).

Ask only what matters for long-lived contracts and design:
- System identity and boundaries
- Core business invariants
- Global constraints or safety risks
- Long-lived architectural or UX intent

Do NOT ask about:
- Implementation details
- Edge cases or speculative features
- Anything deferrable to task-level work

Provide recommendations when the user faces a choice:

```
Recommendation: [option] — [brief reason]
```

When understanding is sufficient, or user enters `initialize`, present a summary for review:

**Format:**

Project Summary

What it is: [description]
What it is NOT: [explicit boundaries]
Users: [who and how]
Core Contracts: [invariants that must always hold]
Design Decisions: [long-lived architectural choices]
Non-Goals: [explicit exclusions]
Open Questions: [unresolved items — treated as task-level concerns]

Type `initialize` to create project files, or correct anything above.


---

## INITIALIZATION

Triggered by user entering `initialize`.

Use ONLY information established during discovery. Do not infer or expand.
If discovery was skipped or cut short, populate only what was explicitly established.

### 1 — Create contracts-log.md

**Contract:** Business invariant that must hold regardless of implementation — even after a full 

Create `/obelisk/contracts/contracts-log.md`:

```markdown
# Contracts Log

## YYYYMMDD-HHMM | Project Initialization | INIT

[All contracts established during discovery, using format:]

YYYYMMDD-HHMM | Project Initialization | ADD
Rule: [contract rule]
```

### 2 — Create history-log.md

Create `/obelisk/history/history-log.md`:

```markdown
# History Log

## YYYYMMDD-HHMM | Project Initialization | INIT


Project Summary

What it is: [description]
What it is NOT: [explicit boundaries]
Users: [who and how]
Core Functionality: [what the system does]
Screens & Flows: [initial screen and flow descriptions]
UX & Design Philosophy: [interaction and design principles]
Core Contracts: [invariants that must always hold]
Design Decisions: [long-lived architectural choices]
Non-Goals: [explicit exclusions]
Open Ideas: [unformalized directions]
Open Questions: [unresolved items — treated as task-level concerns]

---
```

Output:

```
✅ PROJECT INITIALIZED
```