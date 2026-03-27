# Prompt Builder Output Format

Present the final prompt like this:

---

**Task type:** [type] | **Framework:** [name] | **Soul:** [which soul from library, or "dynamic"]
**Assumptions made:** [list any defaults you chose]

```
[THE GENERATED PROMPT — ready to copy/paste or execute]
```

Want me to run this now, or do you want to tweak anything first?

---

## Outcome Logging (After Every Execution)

File: `references/prompt-outcomes.jsonl`

```json
{
  "id": "po_YYYYMMDD_NNN",
  "timestamp": "ISO-8601",
  "task_type": "coding|research|writing|planning|data|debugging|creative|outreach|orchestration",
  "framework": "SDD|SAF|VMC|DA|PS|DP|CB|RCC|CBP",
  "soul": "soul name or 'dynamic'",
  "emotion_prompt_used": true,
  "track_record_injected": false,
  "turns_to_success": 1,
  "outcome": "success|partial|fail",
  "notes": "What worked or needed correction",
  "lesson_ref": "lesson_id or null"
}
```

| Outcome | When |
|---|---|
| `success` | Prompt ran correctly on first try |
| `partial` | Required 1-2 correction turns |
| `fail` | Produced clearly wrong output |

## Prompt Library Storage

When a prompt produces an excellent result, save to `references/prompt-library/`.

Naming: `[task-type]-[brief-slug].md`
Frontmatter: task_type, framework, soul, outcome_rating (1-5), date.
Body: the full prompt.
