---
description: Creates and implements an Obelisk task
---

## Context

Read before starting:
- `/obelisk/contracts/contracts-summary.md`
- `/obelisk/design/design-summary.md`
- `/obelisk-core/guidelines/ai-engineering.md`

If any missing → STOP. Output: Use `/init-project` to initialize the project.

---

## DISCOVERY — Mandatory

You MUST surface your assumptions and ask clarifying questions 
before presenting the task summary. Discovery is never skippable.

Inference from contracts, design, and existing patterns is allowed.
All non-trivial assumptions must be stated and confirmed.

Your goal: make intent, scope, design decisions, and implementation 
approach unambiguous before proceeding.

Ask only what matters:
- Unclear intent, scope, or approach
- Decisions you cannot make unilaterally
- Risks or constraints that would change execution
- Anything that conflicts with existing contracts or design

Do NOT ask about:
- Anything inferable from context, contracts, or design
- Implementation details you can decide yourself
- Low-impact edge cases

Provide a recommendation whenever the user faces a choice:

```markdown
Recommendation: [option] — [brief reason]
```

If a contract conflict is detected:

```markdown
⚠️ Contract Conflict
Conflicts with: "[exact contract text]"
Options:
1. Adjust task to comply
2. Update contract — [what exception is needed]
Recommendation: [option + reason]
Choose: 1/2
```

If the task introduces a new business-critical rule:

```markdown
📋 New Contract
Rule: [what it is and why it matters]
Add? yes/no
```

When nothing important remains unclear, present a clear task summary:

```markdown
Task Summary

Goal: [what and why]
Scope: ✓ [included] / ✗ [excluded]
Approach: [key design decisions]
Contracts: [new or changed, or "None"]
Constraints: [limits implementation must respect]
Risks: [known risks or "None"]

Ready to implement. Enter `implement` to proceed.
```

After presenting the task summary — STOP.
Do not proceed. Do not write code. Do not explain next steps.

Wait for the user to either:
- Correct or update the summary
- Enter `implement` to proceed

If the user provides corrections, update the summary and STOP again.
Only proceed when `implement` is received.

---

## IMPLEMENTATION

Implement the agreed task. During implementation:
- Follow the agreed task summary
- Follow `/obelisk-core/guidelines/ai-engineering.md`
- Respect `/obelisk/contracts/contracts-summary.md` and `/obelisk/design/design-summary.md`

For any follow-up request or scope change from the user:
- Treat it like a mini-discovery: understand the change, check it against contracts and design, surface conflicts if any, confirm understanding before proceeding
- Do not implement changes blindly

When done, output:

```markdown
Implementation complete. Enter `@archive-task` to archive.
```