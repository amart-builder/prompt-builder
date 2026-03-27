---
name: prompt-builder
description: >
  Transform rough, incomplete requests into execution-ready prompts with the right framework,
  context injection, and explicit success criteria. Use when the user says "/prompt [request]",
  "write me a prompt", "help me prompt this", or asks to turn an idea into a structured prompt.
  Outputs a complete prompt Atlas can execute with minimal follow-up. NOT for: answering the
  original task directly when the user wants execution instead of prompt drafting.
---

# Prompt Builder

> Transform a rough request into a masterfully structured prompt that gets the best out of Atlas.

## Reference Files

| File | Contains |
|---|---|
| `instructions/procedure.md` | The 10-step generation process (classify → soul → framework → generate → evaluate) |
| `instructions/taxonomy.md` | 9 task types and their matching frameworks |
| `instructions/context-injection.md` | How to load and weave in system context |
| `templates/output-format.md` | Presentation format and outcome logging schema |
| `references/framework-templates.md` | Full template for each of the 9 frameworks |
| `references/framework-examples.md` | Concrete examples of generated prompts |
| `references/soul-library.md` | 20+ expert identities + dynamic generation template |
| `references/prompt-outcomes.jsonl` | Track record data for distribution anchoring |
| `references/prompt-library/` | Saved successful prompts for reuse |

## Workflow

### Step 1: Classify
Read `instructions/taxonomy.md`. Classify the task into one of 9 types.

### Step 2: Load Context
Read `instructions/context-injection.md`. Search prompt library first, then load system state.

### Step 3: Generate
Read `instructions/procedure.md` and follow all 10 steps in order. This includes:
- Soul selection from `references/soul-library.md`
- Contrarian framing (anti-default constraints)
- Framework selection from `references/framework-templates.md`
- EmotionPrompt calibration
- Track record injection from `references/prompt-outcomes.jsonl`
- Self-evaluation checklist

### Step 4: Present
Read `templates/output-format.md`. Present the prompt with metadata and offer to execute.

### Step 5: Log Outcome
After execution, log result to `references/prompt-outcomes.jsonl` per the schema in `templates/output-format.md`.
