---
description: Apply small mechanical fix directly
---

## Assessment

**Qualifies as hotfix if:**
- Scope is narrow, low-risk, and clearly defined
- Change is mechanical and localized
- No design, architectural, or contract changes required

**If criteria not met:**
Output: "This looks like a full task. Run /define-task for proper scoping.
Type `continue` to proceed as hotfix anyway."
Wait for user input. If `continue` → proceed.

---

## Execution

Before applying:
- Identify exact file(s) and line(s) to modify
- Confirm change preserves existing behavior and contracts

Then:
- Apply only the minimal necessary modification
- Do not expand scope, refactor, or touch code outside the direct fix
- If scope grows or uncertainty appears → STOP and report

---

## Write History

Append to `/obelisk/history/history-log.md` under `## Unprocessed`:
```markdown
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