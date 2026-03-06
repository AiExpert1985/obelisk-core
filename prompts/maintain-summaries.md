---
description: Compact log and regenerate contracts summary
---
## Required Files

- `/obelisk/history/history-log.md`
- `/obelisk/contracts/contracts-summary.md`
- `/obelisk/design/design-summary.md`

If any file is missing → STOP. Output: Use `@init-project` to initialize the project.

---

## Source of Truth

`history-log.md` is the sole source of truth.
Entries are ordered oldest → newest. Later entries may add, refine, or replace earlier ones.
Read the entire file before generating summaries.
Only **Design** and **Contracts** fields are used for summaries.

---

## Regenerate Contracts Summary

Extract all **Contracts** fields from history-log entries.

- Keep only active invariants — if a later entry updates a rule, keep the latest version
- Merge contracts expressing the same invariant without altering meaning
- If a contract is declared but not enforced in code → mark "Active but unenforced"
- If conflict is unclear → keep both and flag
- Do NOT invent, expand, or reinterpret contracts

Overwrite `/obelisk/contracts/contracts-summary.md`:
```markdown
# Contracts Summary

Generated: YYYY-MM-DD

[Concise list of active business invariants.]

## New
```

Contracts must be implementation-independent, durable across rebuilds, and free of code or UI detail.
Keep concise — under 1500 tokens. `## New` must remain present and empty after maintain.

---

## Regenerate Design Summary

Extract all **Design** fields from history-log entries.

- Keep only architectural or feature-level decisions
- Skip UI tweaks, layout details, and implementation specifics
- If a later entry revises an earlier decision, keep the latest version
- Merge related decisions describing the same architectural element
- If design contradicts a contract → trust the contract, flag in Open Design Questions
- If conflict is unclear → flag in Open Design Questions
- Do NOT invent, expand, or reinterpret decisions
- Do NOT infer design from code

Overwrite `/obelisk/design/design-summary.md`:
```markdown
# Design Summary

Generated: YYYY-MM-DD

[Concise list of active architectural decisions.]

## Open Design Questions
[Unresolved decisions or detected conflicts — omit if none]
```

Design must be system-level or feature-level, high-level, and implementation-agnostic.
Keep concise — under 2000 tokens.

---

Output:

✅ MAINTAIN COMPLETE
Contracts and design summaries regenerated.