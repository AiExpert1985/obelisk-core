---
description: Suggest next tasks
---
## Required Files

- `/obelisk/contracts/contracts-summary.md`
- `/obelisk/design/design-summary.md`

**If any file is missing:**
- STOP and report missing file
- OUTPUT: Use `@init-project` to initialize the project.

---

## Analysis

### Primary Sources (Read First)

**From contracts-summary.md:**
- Active invariants
- Enforcement requirements
- System boundaries
- Explicit non-goals

**From design-summary.md:**
- Active system architecture
- Defined modules and their status
- Core design principles
- Open design questions
- Deferred architectural work

### Secondary Source (Optional)

**From `/obelisk/project/project-initial-description.md`:**
Load only after primary sources.
Use only to surface open ideas not yet formalized into tasks.
If conflicts with contracts or design → ignore.

### Reference Source (Optional)

**From `/obelisk/history/history-log.md`:**
Load only to avoid re-suggesting completed or rejected tasks.

---

## Task Categories (Priority Order)

1. **Deferred Design**
   - Open design questions requiring resolution
   - Deferred architectural decisions
   - Defined but unimplemented modules

2. **Contract Enforcement**
   - Declared invariants not yet implemented
   - Newly introduced constraints requiring integration

3. **Extension**
   - Logical next steps within existing modules
   - Structural refinements strengthening architecture
   - Completing partially implemented flows

4. **Open Ideas** (lowest priority)
   - Unformalized directions from project-initial-description.md
   - Only if no higher-priority tasks exist

---

## Rules

- Respect contracts and design boundaries
- Avoid speculative features outside declared architecture
- Do not re-suggest completed or rejected work
- Tasks must be concrete and scoped
- Prefer system-level impact over local optimization
- If design has many open questions, prioritize architectural clarity first

Select the **top 2 highest-impact tasks**.

---

## Output
```markdown
Here are suggested next tasks based on current system state:

1. **[Task Name]**
   What: [2-3 sentences on what the task involves and what it delivers]
   Why: [one short reason grounded in contracts or design]

2. **[Task Name]**
   What: [2-3 sentences on what the task involves and what it delivers]
   Why: [one short reason grounded in contracts or design]
```