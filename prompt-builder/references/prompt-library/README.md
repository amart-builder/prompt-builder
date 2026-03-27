# Prompt Library

Saved prompts that produced excellent results. Use as starting points — don't start from a blank template when a proven one exists.

## How to Search
```bash
qmd search "[task keywords]" -c prompt-library -n 3
```
(Run `qmd collection add /path/to/prompt-library --name prompt-library` once to index.)

## File Format

Each saved prompt is a markdown file with frontmatter:

```markdown
---
task_type: coding|research|writing|planning|data|debugging|creative|outreach|orchestration
framework: SDD|SAF|VMC|DA|PS|DP|CB|RCC|CBP
soul: soul name or dynamic
outcome_rating: 1-5
date: YYYY-MM-DD
context: one-line description of what this was originally used for
---

[Full prompt text here]
```

## Naming Convention
`[task-type]-[brief-slug].md`

Examples:
- `outreach-lp-warm-reintro.md`
- `coding-supabase-schema-migration.md`
- `research-competitor-due-diligence.md`
- `planning-spv-deal-strategy.md`

## Usage Rule
Before building any prompt from scratch, search this library. If a match scores > 0.7 similarity, adapt it rather than rebuilding. Note the original in the outcome log.
