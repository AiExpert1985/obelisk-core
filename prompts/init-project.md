---
description: Initialize new Obelisk project
---
## Guard

Check that none of these exist:
- `/obelisk/contracts/contracts-summary.md`
- `/obelisk/contracts/contracts-log.md`
- `/obelisk/design/design-summary.md`
- `/obelisk/design/design-log.md`
- `/obelisk/history/history-log.md`

If any exist → STOP. Output:
⛔ Project already initialized. Remove existing obelisk state before re-initializing.

---

## Contract vs. Design Boundary

**Contract:** Business invariant that must hold regardless of implementation — even after a full rebuild.
**Design:** How the system is built — tech, schema, architecture, patterns.

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

```markdown
Project Summary

What it is: [description]
What it is NOT: [explicit boundaries]
Users: [who and how]
Core Contracts: [invariants that must always hold]
Design Decisions: [long-lived architectural choices]
Non-Goals: [explicit exclusions]
Open Questions: [unresolved items — treated as task-level concerns]

Type `initialize` to create project files, or correct anything above.
```

---

## INITIALIZATION

Triggered by user entering `initialize`.

Use ONLY information established during discovery. Do not infer or expand.
If discovery was skipped or cut short, populate only what was explicitly established.

### 1 — Create contracts-summary.md

Create `/obelisk/contracts/contracts-summary.md`:

```markdown
# Contracts Summary

Generated: YYYY-MM-DD

## System Identity
_(empty — populated after first maintenance)_

## Active Contracts
_(empty — populated after first maintenance)_

## Non-Goals
_(empty — populated after first maintenance)_

## New

[All contracts and invariants established during discovery]
```

### 2 — Create design-summary.md

Create `/obelisk/design/design-summary.md`:

```markdown
# Design Summary

Generated: YYYY-MM-DD

## System Architecture
_(empty — populated after first maintenance)_

## Data Model
_(empty — populated after first maintenance)_

## Core Design Principles
_(empty — populated after first maintenance)_

## Modules
_(empty — populated after first maintenance)_

## Open Design Questions
_(empty — populated after first maintenance)_

## New

[All design decisions established during discovery]
```

### 3 — Create history-log.md

Create `/obelisk/history/history-log.md`:

```markdown
# History Log

## YYYYMMDD-HHMM | Project Initialization | INIT

## Vision
[What the system is and why it exists]

## Users
[Who uses it and how]

## Screens & Flows (Initial)
[Initial screen and flow descriptions]

## Core Functionality (Initial)
[Initial feature descriptions]

## UX & Design Philosophy
[Interaction and design principles]

## UI & Screen Notes (Initial)
[Layout, style, component notes]

## Open Ideas
[Unformalized directions — append only]

## Notes
[Anything else discussed during init]

---
```

Output:

```
✅ PROJECT INITIALIZED
```