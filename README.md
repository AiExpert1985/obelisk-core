# Obelisk Framework

_A contract-driven collaboration protocol for long-lived AI-assisted software systems._

Obelisk prevents silent drift by externalizing truth, intent, and history into structured files — not chat. It optimizes for long-term correctness, not short-term speed.

---

## Core Idea

AI fails over time not because it is weak, but because context is lost, decisions are forgotten, scope silently expands, and stable code is touched accidentally.

Obelisk separates four layers:

- **Contracts** — invariants that must always hold
- **Design** — long-lived architectural decisions
- **Tasks** — frozen intent and execution boundaries
- **History** — chronological memory of decisions and rationale

Contracts and Design are authoritative. History is informational. Tasks are temporary execution specifications.

---

## Designed For

Long-lived systems where correctness matters more than velocity, breaking changes damage trust, and AI is used continuously.

**Not designed for:** throwaway prototypes, maximum-speed experimentation, replacing manual testing.

---

## Repository Structure

```
/obelisk-core/                  # Framework prompts (shared, git submodule)
├── prompts/
│   ├── init-project.md
│   ├── new-task.md
│   ├── implement-task.md
│   ├── ask-project.md
│   ├── suggest-task.md
│   ├── hotfix.md
│   ├── maintain-project.md
│   └── help.md
└── guidelines/
    └── ai-engineering.md

/obelisk/                       # Project state (local, per-project)
├── contracts/
│   ├── contracts-log.md        # Canonical invariants (append-only)
│   └── contracts-summary.md    # Active projection (regenerated)
├── design/
│   ├── design-log.md           # Canonical design decisions (append-only)
│   └── design-summary.md       # Active projection (regenerated)
├── workspace/
│   └── task.md                 # Active task (cleared after archive)
└── history/
    ├── history-log.md          # Complete project memory
    ├── completed/              # One file per completed task
    └── rejected/               # One file per rejected task
```

No archive folder. Each task becomes one self-contained file in history.

---

## Authority Model

Highest → Lowest:

1. Contracts Log
2. Design Log
3. Active Task
4. AI Engineering Rules
5. History Log
6. Derived Summaries
7. Chat History

Summaries never override logs. History never overrides contracts or design.

---

## Task Lifecycle

### 1 — `/new-task`

Clarify intent, validate against contracts, freeze a single `task.md` containing:

- Goal, Scope, Constraints, Execution Strategy, Affected Area
- Archive Data: Contract-Changes, Design-Changes, Discovery Summary

No separate plan file.

### 2 — `/implement-task`

- Implement strictly according to task.md
- STOP if scope or constraints would be violated
- Append Implementation Notes and Review into task.md
- Extract and apply Contract-Changes and Design-Changes verbatim
- Append Discovery Summary to history-log.md
- Archive task to `/history/completed/` or `/history/rejected/`

No reinterpretation. No silent redesign.

---

## Constraints Model

Each task defines constraints that implement-task enforces strictly:

```markdown
## Constraints
- Contract: [Name] — [specific applicability]
- Design: [Principle] — [specific applicability]
- [Technical or business limits]
```

---

## History Model

`history-log.md` records every task outcome with its discovery summary:

```markdown
## YYYYMMDD-HHMM | Task Name | APPROVED / REJECTED

[Discovery Summary]

---
```

Each archived task file contains the full frozen task, implementation notes, review, and archive data. History is project memory — never authority.

---

## Hotfix

For small, mechanical, fully reversible fixes only. Requires mandatory contract scan before execution — if contract risk is detected, escalates to `/new-task`. Always recorded in history.

---

## Auto-Maintain

When contracts-summary or design-summary accumulate ≥ 10 unprocessed entries, run `/maintain-project` to compact logs and regenerate summaries.

---

## Commands

|Command|Purpose|
|---|---|
|`/init-project`|Initialize project structure|
|`/new-task [description]`|Discover intent, freeze task|
|`/implement-task`|Implement, review, archive|
|`/ask-project`|Query project knowledge|
|`/suggest-task`|Suggest next high-impact tasks|
|`/hotfix [description]`|Apply small mechanical fix|
|`/maintain-project`|Compact and regenerate summaries|
|`/help`|Show available commands|

---

Obelisk is not a productivity booster. It is a long-term stability system for AI-driven development.