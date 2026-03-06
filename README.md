# Obelisk Framework

_A clarity-first collaboration system for long-lived AI-assisted software._

Obelisk does not constrain AI — it equips it with durable, structured knowledge so strong models can execute correctly over time.

**Designed for** long-lived systems with continuous AI-assisted development where invariants and architecture matter.

**Not designed for:** throwaway prototypes, pure experimentation, replacing manual testing.

---

## Core Philosophy

AI errors over time are rarely due to weak reasoning. They happen because intent was unclear, scope drifted silently, decisions were forgotten, and architectural context was lost.

Obelisk solves this through two pillars:

1. **Discovery** — model fully understands the task, checks it against contracts and design, gets explicit user confirmation before implementing
2. **Archive** — completed work is documented into structured files that future tasks read and respect

Between discovery and archive, the model works freely.

---

## Core Layers

- **Contracts** — business invariants that must hold even after a full rebuild
- **Design** — long-lived architectural decisions
- **History** — chronological memory of completed work
- **Tasks** — conversationally defined, archived after completion

Contracts and Design are authoritative. History is informational. Chat is temporary.

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
│   ├── contracts-log.md        # Canonical invariants (append-only)
│   └── contracts-summary.md    # Active projection (regenerated)
├── design/
│   ├── design-log.md           # Canonical design decisions (append-only)
│   └── design-summary.md       # Active projection (regenerated)
└── history/
    ├── history-log.md          # Complete project memory
    └── completed/              # One file per completed task
```

---

## Authority Model

Highest → Lowest:

1. Contracts Log
2. Design Log
3. Contracts Summary
4. Design Summary
5. History Log
6. Chat History

Logs are append-only and authoritative. Summaries are working projections.

---

## Workflow

### 1 — `@init-project`
Conversational discovery of system identity, core contracts, and long-lived design decisions. Creates summary files and initializes empty logs.

### 2 — `@new-task`
Focused discovery conversation. Model reads contracts, design, and engineering guidelines, clarifies intent and scope, surfaces conflicts, and presents a task summary. User confirms with `implement`. Model then implements freely — scope changes trigger a mini-discovery before proceeding. The conversation is the workspace.

### 3 — `@archive-task`
User-triggered. Model reads the full conversation and produces a canonical task file, updates history-log, contracts-summary, and design-summary.

---

## Auto-Maintain

Each archive adds new entries to contracts-summary and design-summary. Over time these grow stale and verbose. `@maintain-project` compacts the logs and regenerates clean summaries. Triggered automatically by `@archive-task` when either summary reaches ≥ 50 unprocessed line.

---

## Commands

| Command                   | Purpose                                             |
| ------------------------- | --------------------------------------------------- |
| `@init-project`           | Initialize project structure                        |
| `@new-task [description]` | Discover, confirm, and implement a task             |
| `@archive-task`           | Archive completed work and update project knowledge |
| `@ask-project`            | Query project knowledge                             |
| `@suggest-task`           | Suggest next high-impact tasks                      |
| `@hotfix [description]`   | Apply small mechanical fix                          |
| `@maintain-project`       | Compact and regenerate summaries                    |
| `@help`                   | Show available commands                             |

---

Obelisk is a clarity amplifier, a memory system, and a contract guardian. It gives strong AI models the freedom to execute — while ensuring that what matters persists.