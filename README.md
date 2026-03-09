# Obelisk Framework

_A clarity-first collaboration system for long-lived AI-assisted software._

Obelisk equips AI with durable, structured project knowledge so models can execute reliably over time.

**Designed for:** long-lived systems where architecture, invariants, and decisions must persist. **Not designed for:** throwaway prototypes, experimentation, or replacing manual testing.

---

## Core Philosophy

AI errors over time rarely come from weak reasoning. They happen because intent becomes unclear, scope drifts silently, decisions are forgotten, and architectural context is lost.

Obelisk solves this through two pillars:

**Discovery** — The model fully understands the task before implementation. It checks contracts and history, surfaces assumptions, and produces a task summary for user confirmation.

**Archive** — Completed work is recorded into structured files so future tasks start with correct context.

Between discovery and archive, the model works freely.

---

## Knowledge Layers

**Contracts** — Business invariants that must hold regardless of implementation. Stored as an ordered event log (ADD / UPDATE / REMOVE). The log is the source of truth — no derived summary exists.

**History** — Chronological record of tasks, decisions, and outcomes. Decisions only — no implementation detail, no contracts.

Both files are append-only. Chat history is temporary and has no authority.

---

## Repository Structure

```
/obelisk-core/                  # Framework prompts
├── commands/
│   ├── init-project.md
│   ├── new-task.md
│   ├── archive-task.md
│   ├── ask-project.md
│   ├── suggest-task.md
│   └── help.md
└── guidelines/
    └── ai-engineering.md

/obelisk/                       # Project state (local, per-project)
├── contracts/
│   └── contracts-log.md        # Ordered contract event log (source of truth)
└── history/
    ├── history-log.md          # Chronological record of tasks and decisions
    └── completed/              # Detailed file per completed task
```

---

## AI Reading Order

When working on a task, read files in this order:

1. `/obelisk/history/history-log.md`
2. `/obelisk/contracts/contracts-log.md`
3. `/obelisk-core/guidelines/ai-engineering.md`

History provides task and decision context. Contracts log provides active invariants.

---

## Source of Truth

`history-log.md` records every task and decision chronologically. Entries are high-level — what was done and why. No code, no implementation detail.

`contracts-log.md` records every contract change as a typed event (ADD / UPDATE / REMOVE). Active contracts are determined by replaying the log in order. No regeneration or maintenance required.

History entries record the user request and agreed decisions — not implementation details.

---

## Workflow

### 1 — `@init-project`

Conversational discovery of system identity, core contracts, and foundational design decisions. Initializes `contracts-log.md` and `history-log.md`.

### 2 — `@new-task`

Focused discovery conversation. The model reads history and contracts, surfaces assumptions, asks clarifying questions, and presents a Task Summary. User confirms with `implement`. Scope changes during implementation trigger a mini-discovery before proceeding.

### 3 — `@archive-task`

User-triggered after implementation. The model writes a detailed task file under `/history/completed/`, appends a concise entry to `history-log.md`, and appends typed contract change events to `contracts-log.md` if contracts changed.


---

## Commands

| Command                   | Purpose                                     |
| ------------------------- | ------------------------------------------- |
| `@init-project`           | Initialize project knowledge                |
| `@new-task [description]` | Discover, confirm, and implement a task     |
| `@archive-task`           | Archive completed work and update knowledge |
| `@ask-project`            | Query project knowledge                     |
| `@suggest-task`           | Suggest next high-impact tasks              |
| `@help`                   | Show available commands                     |

---

Obelisk ensures important decisions outlive chat sessions, model resets, and time. It gives AI the freedom to execute — while ensuring that what matters persists.