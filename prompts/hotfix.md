---
description: Run small mechanical fix without full task flow
---

## Assessment

**A task qualifies as hotfix if:**
- Scope is narrow, low-risk and clearly defined
- Change is mechanical and localized
- No design or architectural decisions required
- No contract changes required

**Common examples (non-exhaustive):**
- Typo, formatting, or whitespace fix
- Simple rename (variable, function, file)
- Add missing import or dependency
- Trivial bug fix (null check, off-by-one)
- Pure UI changes

**If criteria is not met:**
- Output: 
  "The fix is not simple, it is better to run it as full task using new-task prompt."
  if you choose to continue, run "continue"
  
  wait for user input, if continue run below


## Execution

Perform exactly the mechanical change described.

Before applying:
- Identify the exact file(s) and line(s) to modify
- Confirm the change preserves existing behavior and contracts

Then:
- Apply only the minimal necessary modification
- Do not expand scope, refactor, rename, or touch code outside the direct fix
- If scope grows or uncertainty appears → STOP and report
- If anything unexpected appears → STOP

---

## Write History

Append the following block as the last entry within the section `## Unprocessed`
in `/obelisk/history/history-log.md`:

``` markdown
## YYYYMMDD-HHMM | [Hotfix Name] | HOTFIX

---

```
---

## Output
```
✅ HOTFIX APPLIED
Recorded in history-log.md
```

STOP.