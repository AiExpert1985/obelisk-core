---
description: Creates a new Obelisk task
---
## Entry Point Detection

**If user provided description:**

- Extract task_description from input

**If no description:** Output exactly: "Describe your task" STOP. Wait for response. Set task_description = [response]


---

## Required Files

- `/obelisk/contracts/contracts-summary.md`
- `/obelisk/design/design-summary.md`
- `/obelisk/guidelines/ai-engineering.md`

**If any file is missing:** STOP and output: Use `init-project` to initialize the project.

---

## Code Reconnaissance (Optional, Bounded)

- Read only what is necessary to understand scope and locate affected files.
- Note observations as you go — reuse them during planning without re-reading.
- Do NOT reason about how to implement.

---

## Contract vs. Design Boundary

- **Contract:** A business invariant that must remain true regardless of implementation. If violated, business correctness or historical data integrity breaks.

- **Design:** How the system is built (tech stack, schema, architecture, modules, UI, patterns).

- **Boundary test:**
  - Must stay true even if the system is rebuilt differently → Contract
  - Describes structure, schema, tech, or implementation detail → Design

---

## Discovery Questions

### Question Rules

**Ask ONLY questions affecting:**

- Task definition or intent
- Scope boundaries
- Feasibility or approach
- Required constraints

**Do NOT ask about:**

- Information already stated in contracts-summary, design-summary, task description, or prior answers

Keep questions high-impact. Skip obvious or low-value questions.

---

### Providing Recommendations


Provide a brief recommendation ONLY when one option is objectively preferable based on existing contracts, design constraints, or technical realities.

If preference depends on user taste, unclear trade-offs, or speculation → do not recommend.

Place recommendation immediately after the question.


**Format:**

```markdown
[Question]

Recommendation: [Option] — [brief reason].
```

---

### Clarification Questions (MANDATORY)

Always ask at least one clarification question.

**📌 Questions:**
- What, why, for whom
- Scope boundaries (what's in/out)
- Key constraints or dependencies (including required or preferred external libraries, if any)

**After Clarification Questions:**
> "Answers helps model fully understand current task."

→ If no clarification gaps remain AND no contract require user input:
   - State: "No further questions are needed."
   - Proceed to Task Freeze

→ Otherwise: Continue to Refinement Questions

---

### Refinement Questions (If Needed)

Resolve remaining issues in organized groups. Skip each group if no issues detected.

---

**📌 Group 1: Clarification** (if gaps remain)

- Resolve ambiguities from clarification Questions
- Important edge cases needing user input
- Approach selection when multiple valid options
- Flag if task should be split

*Skip if no clarification needed.*

---

**📋 Group 2: Contracts**

Check task against all loaded contracts.

**If conflict found:**

```
⚠️ Contract Conflict

Task: [specific step that conflicts]
Conflicts with: "[exact contract text]"

Options:
1. Update task — [what changes]
2. Update contract — [what exception needed]

Recommendation: [Option] because [reason]

Choose: 1/2
```

**If new contract needed** (ONLY for business-critical rules):

```
📋 Contract Addition

Task introduces: [critical functionality]
Rule: [why contract-worthy]

Add? yes/no
```

*Skip if no contract issues.*

---

# TASK FREEZE

## Clean Workspace

Delete all files in `/obelisk/workspace/` before proceeding.

---

## Create `/obelisk/workspace/task.md`

```markdown

# Task: [One-line descriptive name]

## Goal
[What must be achieved and why]

## Scope
✓ Included: [list]
✗ Excluded: [list]

## Constraints
- **Contract: [Name]** — [specific applicability]
- **Design: [Principle]** — [specific applicability]
- [Technical/business limit]

## Execution Strategy
[3–5 concise sentences]

## Affected Area
- **Module / Feature:** [name]
- **Entry points:** [e.g., "UserProfile screen", "billing service"]
- **Notes:** [contract-sensitive spots or "None"]

## Open Questions
- [or "None"]

---

## Contract-Changes
**Date:** YYYY-MM-DD
**Action:** update | create
**Change:**
- [exact text]

## Design-Changes
**Date:** YYYY-MM-DD
- [decisions]

## Discovery Summary
**Intent:** [1 short paragraph]
**Key Decisions:** [bullets]
**Rejected / Deferred:** [bullets or omit]

```


### Rules
All sections must be concise and focused. Omit any section that has no content.

#### Constraints
- Prefix each entry with Contract:, Design:, or leave unprefixed for technical/business limits
- Reference contracts and design by name plus specific applicability only — do not copy full text

#### Affected Area
- High-level only — modules, features, entry points
- Do not list exact file paths
- Note contract-sensitive spots if any

#### Contract-Changes
- Covers both new contracts and updates to existing ones
- Only include changes explicitly approved by the user during discovery
- A rule is contract-worthy only if violating it risks system integrity, business correctness, or irreversible damage
- Copy approved wording exactly — do not paraphrase

#### Design-Changes
- Covers both new design decisions and updates to existing ones
- Long-lived system-level decisions only
- No implementation details, cosmetic choices, or speculative decisions
- Be concise (under 100 words)

#### Discovery Summary
- Informational only — never authoritative
- Be concise (under 120 words total)
- Omit Rejected/Deferred if none

---

## OUTPUT

Output EXACTLY this block. No additions.

```
Obelisk: Task Ready

Task frozen: /obelisk/workspace/task.md

Review task.md.
If you have corrections, describe them now.
Otherwise:

To implement the task, call the implement-task prompt.
```

---

## Post-Freeze Corrections

If the user provides corrections:

1. Classify the correction first:
   - **Mechanical** — wording or clarification only, no change to scope, intent, constraints, or contract impact
   - **Substantive** — changes scope, goal, constraints, or contract interactions

2. If Mechanical:
   - Update `task.md` and/or `plan.md`
   - Output: `Task updated.`
   - Repeat TERMINAL STATE

3. If Substantive:
   - Output: `Correction changes scope or constraints. Restarting discovery.`
   - Restart from ## Refinement Questions using existing task description and previous questions & answers as context

If no corrections → wait for `/implement-task`