---
description: Apply small mechanical fix directly
---
## Required Files

- `/obelisk/contracts/contracts-summary.md`

**If any file is missing:**
- STOP and report missing file
- OUTPUT: Use `@init-project` to initialize the project.

---


## Assessment

Load `/obelisk/contracts/contracts-summary.md`.  

**Qualifies as hotfix if ALL are true:**
- Change is mechanical, localized, and clearly defined
- No contract or design changes required
- For each contract whose domain overlaps the affected code, state:
  > **[Contract Name]:** [one sentence why this change does not affect it]
- All relevant contracts cleared. If any cannot be cleared → STOP.
  Output: "Contract risk detected. Run `/new-task`." No override allowed.

If no contracts are relevant → state: "No relevant contracts identified."

**If scope or intent is unclear:**
Output: "This looks like a full task. Run `/new-task`."
STOP.

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

Contracts scanned: [list]

---
```

## Output
```
✅ HOTFIX APPLIED
Recorded in history-log.md
```

STOP.