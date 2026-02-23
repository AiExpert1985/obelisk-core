---
description: Apply small mechanical fix directly
---
## Assessment

### A task qualifies as hotfix if:
- Scope is narrow, low-risk and clearly defined
- Change is mechanical and localized
- No design or architectural decisions required
- No contract changes required

### Common examples (non-exhaustive):
- Typo, formatting, or whitespace fix
- Simple rename (variable, function, file)
- Add missing import or dependency
- Trivial bug fix (null check, off-by-one)
- Pure UI changes

### If criteria is not met:

- Output:
  "The fix is not simple, it is better to run it as full task using new-task prompt."
  if you choose to continue, run "continue"
  wait for user input, if continue run below

---

## Execution

- Apply only the minimal necessary modification
- Do not expand scope, refactor, or touch code outside the direct fix
- MUST NOT modify contracts or design files
- If scope grows or uncertainty appears → STOP and report

---

## Write History

Append to `/obelisk/history/history-log.md` under `## Unprocessed`:
```markdown
## YYYYMMDD-HHMM | [Hotfix Name] | HOTFIX

---
```

## Output
```
✅ HOTFIX APPLIED
Recorded in history-log.md
```

STOP.