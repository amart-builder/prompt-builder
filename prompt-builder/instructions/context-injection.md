# Context Injection

When generating the prompt, automatically weave in relevant context. Don't dump raw context — synthesize it naturally.

## Sources to Check

| Source | File | When |
|---|---|---|
| Current focus | `memory/working/current_focus.md` | Always |
| Today's notes | `memory/YYYY-MM-DD.md` | Always |
| Project entities | `memories/projects.md` | When task involves a project |
| People entities | `memories/people.md` | When task involves a person |
| Lessons | `memory/semantic/lessons.jsonl` | When relevant past mistakes exist |
| Prompt library | `references/prompt-library/` | Search before generating from scratch |

## Semantic Sweep
Before manual reads, run: `qmd search "[task keywords]" -c atlas-brain -n 5 --json` (if qmd installed).

qmd finds unexpected context; manual reads capture structured state.

## Prompt Library Check
Before generating any prompt, search the library: `qmd search "[task keywords]" -c prompt-library -n 3`.

Start from your best prior work, not from a blank template.
