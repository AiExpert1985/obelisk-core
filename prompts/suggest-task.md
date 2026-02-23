---
description: Suggest next tasks
---
## Required Files

- `/obelisk/history/history-log.md`
- `/obelisk/contracts/contracts-summary.md`
- `/obelisk/design/design-summary.md`

---

## Analysis

Read in order:

1. **history-log.md** — completed tasks, rejected tasks, deferred decisions, open ideas
2. **contracts-summary.md** — active invariants, enforcement gaps, non-goals
3. **design-summary.md** — open design questions, deferred architectural work, defined but unimplemented modules

---

## Task Priority Order

1. **Deferred Design** — open design questions, deferred architectural decisions, unimplemented modules
2. **Contract Enforcement** — declared invariants not yet implemented
3. **Extension** — logical next steps within existing modules or flows
4. **Open Ideas** — unformalized directions from history, only if nothing higher-priority exists

---

## Rules

- Do not re-suggest completed or rejected work
- Tasks must be concrete and scoped
- Respect contracts and design boundaries
- Prefer system-level impact over local optimization
- Select top 2 highest-impact tasks

---

## Output
```markdown
1. **[Task Name]**
   What: [2-3 sentences]
   Why: [one reason grounded in contracts, design, or history]

2. **[Task Name]**
   What: [2-3 sentences]
   Why: [one reason grounded in contracts, design, or history]
```