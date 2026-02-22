---
description: Compact log and regenerate contracts summary
---
## Required Files

- `/obelisk/contracts/contracts-log.md`
- `/obelisk/contracts/contracts-summary.md`
- `/obelisk/design/design-log.md`
- `/obelisk/design/design-summary.md`

**If any file is missing:**
- STOP and report missing file
- OUTPUT: Use `@init-project` to initialize the project.

---

## MAINTAIN CONTRACTS

## Stage 1 — Process Unprocessed

1. Move all entries from `contracts-summary.md → ## Unprocessed` to `contracts-log.md` (append).
2. Clear `## Unprocessed` in summary.

---

## Stage 2 — Regenerate Summary

### Inputs (Read-Only)

- `/obelisk/contracts/contracts-log.md` (authoritative)
- `/obelisk/design/design-log.md` (evolution context)
- Codebase (enforcement context only)

Contracts-log defines declared intent.
Design-log provides context.
Code does NOT override contracts.

---

## Analysis Rules

### Supersession

A contract is superseded if a later log entry:
- Explicitly replaces it
- Introduces conflicting requirement in the same domain
- Removes the domain entirely

If uncertain → keep both and flag.

### Consolidation

Merge contracts expressing the same constraint without altering meaning.

Do NOT merge:
- Orthogonal constraints
- Different actors or contexts

If uncertain → do not merge.

### Enforcement Gaps

If a contract is declared but not enforced in code:
- Keep it active
- Mark as: "Active but unenforced"

Do NOT remove contracts due to missing enforcement.

---

## Write Summary

Overwrite `/obelisk/contracts/contracts-summary.md`:
```markdown
# Contracts Summary

Generated: YYYY-MM-DD

## System Identity
[Consolidated identity]

## Active Contracts
[Each active contract]
[Mark enforcement gaps if applicable]

## Non-Goals
[Consolidated non-goals]

## Unprocessed
```

## Constraints

- contracts-log.md is immutable and authoritative.
- Remove contracts only if explicitly superseded.
- Do NOT invent, expand, or narrow contracts.
- Keep summary concise (less than 1000 tokens).
- `## Unprocessed` must remain present and empty.

---

## MAINTAIN DESIGN

## Stage 1 — Process Unprocessed

1. Move all entries from `design-summary.md → ## Unprocessed` to `design-log.md` (append).
2. Clear `## Unprocessed`.

---

## Stage 2 — Regenerate Design Summary

### Inputs (Read-Only)

- `/obelisk/design/design-log.md` (authoritative design history)
- `/obelisk/contracts/contracts-log.md` (constraints context)

Authority:
- `design-log.md` defines declared design.
- `contracts-log.md` overrides on conflict.
- Code does NOT rewrite design.

---

## Consolidation Rules

**Supersession**
A decision is superseded if a later entry:
- Explicitly replaces it
- Clearly contradicts it in the same domain
- Removes the feature or module

Show current state only.
If uncertain → keep both and flag in Open Design Questions.

**Merging**
Consolidate decisions about the same architectural element without altering meaning.

Do NOT merge:
- Orthogonal design decisions
- Different modules
- Conflicting approaches (flag instead)

**Contract Conflicts**
If design contradicts a contract:
- Trust contract
- Reflect contract in summary
- Note inconsistency in Open Design Questions

---

## Write Summary

Overwrite `/obelisk/design/design-summary.md`:
```markdown
# Design Summary

Generated: YYYY-MM-DD

## System Architecture
[Current architectural principles]

## Data Model
[Current schema decisions]

## Core Design Principles
[High-level decisions]

## Modules
[Active modules with responsibilities]

## Open Design Questions
[Unresolved decisions or detected conflicts]

## Unprocessed
```

## Constraints

- Do NOT invent, expand, or reinterpret design decisions.
- Do NOT infer design changes from code.
- Keep concise (<2000 tokens).
- `## Unprocessed` must exist (empty after regeneration).