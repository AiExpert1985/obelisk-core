# Obelisk Framework

_A clarity-first collaboration system for long-lived AI-assisted software._

Obelisk equips AI with durable, structured project knowledge so models can execute reliably over time.

**Designed for:** long-lived systems where architecture, invariants, and decisions must persist.
**Not designed for:** throwaway prototypes, experimentation, or replacing manual testing.

---

## Core Philosophy

AI errors over time rarely come from weak reasoning. They happen because intent becomes unclear, scope drifts silently, decisions are forgotten, and architectural context is lost.

Obelisk solves this through two pillars:

**Discovery** — The model fully understands the task before implementation. It checks contracts and design, surfaces assumptions, and produces a task summary for user confirmation.

**Archive** — Completed work is recorded into structured files so future tasks start with correct context.

Between discovery and archive, the model works freely.

---

## Knowledge Layers

**Contracts** — Business invariants that must hold regardless of implementation.
**Design** — Long-lived architectural decisions that shape how the system is built.
**History** — Chronological record of tasks, decisions, and outcomes.

History is the **single source of truth**.
Contracts and Design summaries are **derived projections** generated from it.
Chat history is temporary and has no authority.

---

## Repository Structure
```
/obelisk-core/                  # Framework prompts (shared, git submodule)
├── prompts/
│   ├── init-project.md
│   ├── new-task.md
│   ├── archive-task.md
│   ├── ask-project.md
│   ├── suggest-task.md
│   ├── maintain-summaries.md
│   └── help.md
└── guidelines/
    └── ai-engineering.md

/obelisk/                       # Project state (local, per-project)
├── contracts/
│   └── contracts-summary.md    # Active projection (derived from history)
├── design/
│   └── design-summary.md       # Active projection (derived from history)
└── history/
    ├── history-log.md          # Canonical record of all tasks and decisions
    └── completed/              # Detailed file per completed task
```

---

## AI Reading Order

When working on a task, read files in this order:

1. `/obelisk/contracts/contracts-summary.md`
2. `/obelisk/design/design-summary.md`
3. `/obelisk-core/guidelines/ai-engineering.md`
4. `/obelisk/history/history-log.md` — only when running `@maintain-summaries`

Summaries provide current system state. History preserves how the system evolved.

---

## Source of Truth

`history-log.md` records every task and decision chronologically. Each entry contains a task summary, design decisions (if any), and contract changes (if any). Later entries may refine or replace earlier ones.

Summaries represent the current system state. History records the decisions that produced that state.
History entries record the user request and agreed decisions — not implementation details.

---

## Workflow

### 1 — `@init-project`
Conversational discovery of system identity, core contracts, and foundational design decisions. Initializes summaries and history log.

### 2 — `@new-task`
Focused discovery conversation. The model reads summaries and engineering guidelines, surfaces assumptions, asks clarifying questions, and presents a Task Summary. User confirms with `implement`. Scope changes during implementation trigger a mini-discovery before proceeding.

### 3 — `@archive-task`
User-triggered after implementation. The model writes a detailed task file under `/history/completed/`, appends a structured entry to `history-log.md`, and appends new contracts or design decisions to summaries under `## New`.

### 4 — `@maintain-summaries`
User-triggered periodic maintenance. The model reads the entire `history-log.md`, extracts all Contracts and Design entries, keeps only the latest active decisions, and regenerates clean summaries.

---

## Commands

| Command | Purpose |
|---|---|
| `@init-project` | Initialize project knowledge |
| `@new-task [description]` | Discover, confirm, and implement a task |
| `@archive-task` | Archive completed work and update knowledge |
| `@maintain-summaries` | Regenerate contracts and design summaries |
| `@ask-project` | Query project knowledge |
| `@suggest-task` | Suggest next high-impact tasks |
| `@help` | Show available commands |

---

Obelisk ensures important decisions outlive chat sessions, model resets, and time. It gives AI the freedom to execute — while ensuring that what matters persists.