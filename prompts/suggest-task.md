---
description: Suggest next tasks
---
## Read

- `/obelisk/history/history-log.md`
- `/obelisk/contracts/contracts-log.md`

to understand work done in this software project and the rules, and to be able to suggest next tasks

---


## Task Priority Order

1. **Contract Enforcement** — declared invariants not yet implemented
2. **Deferred Work** — approaches or ideas explicitly deferred in history, not rejected
3. **Extension** — logical next steps within existing flows
4. **Open Ideas** — only if nothing higher-priority exists

---

## Rules

- Do not re-suggest completed or rejected work
- Tasks must be concrete and scoped
- Prefer system-level impact over local optimization
- Select top 2 highest-impact tasks

---

## Output
```markdown
1. **[Task Name]**
   What: [2-3 sentences]
   Why: [one reason grounded in contracts or history]

2. **[Task Name]**
   What: [2-3 sentences]
   Why: [one reason grounded in contracts or history]
```