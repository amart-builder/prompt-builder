# Prompt Builder Procedure

## Step 1: Read the Rough Request
Understand what the user actually wants, not just what he said.

## Step 2: Classify the Task Type
Use the taxonomy in `instructions/taxonomy.md` to pick one of 9 types.

## Step 3: Decide If Clarification Is Needed
Only ask if a missing detail would FUNDAMENTALLY change the prompt (different architecture, different scope, different output). Most of the time, make smart defaults and note your assumptions.

**When you DO ask** (1-3 questions max):
```
Before I generate this prompt, quick sanity check:

1. [Question]? (I'm assuming [default])
2. [Question]? (I'm assuming [default])

Say "go" to use my defaults, or correct anything.
```

## Step 4: Load Relevant Context
First run a semantic sweep: `qmd search "[task keywords]" -c atlas-brain -n 5 --json` (if qmd installed).
Then read: `memory/working/current_focus.md`, today's daily notes, relevant entity files.
Don't dump raw context — synthesize what's actually relevant.

## Step 5: Select a Soul
Read `references/soul-library.md` and pick the closest matching expert identity.

Options:
- **Pick from library:** Use closest soul and adapt to the specific task
- **Dynamic generation:** If nothing fits or stakes are high, use the Dynamic Soul Generation prompt
- **Multi-soul review:** For high-stakes, simulate 2-3 expert perspectives — disagreement is where real insight lives

Always include the soul's Decision Framework if one exists. A soul without a decision framework is a costume; a soul with one is a reasoning engine.

## Step 6: Contrarian Frame
Write one sentence describing what a zero-skill default LLM would produce. Identify the 2-3 most predictable patterns (structure, vocabulary, assumptions). Encode these as "Anti-default" constraints in the prompt body.

## Step 7: Select Framework
Read `references/framework-templates.md` and pick the framework matching the classified task type.

## Step 8: Generate the Prompt
Using the framework template, soul, contrarian constraints, and loaded context.

## Step 8.5: Apply EmotionPrompt Layer
Research shows emotional stakes language produces 8-115% improvement on accuracy benchmarks.

| Stakes | Language | When |
|---|---|---|
| High | "This task is critical to the user's business success and directly impacts his most important goals this year. Outstanding execution here will lead to real, meaningful outcomes." | Fundraising, strategy, critical builds, Forge outreach |
| Medium | "Getting this right matters. High-quality output will make a genuine difference to the project." | Analysis, research, planning, drafts |
| Low | Omit | Quick lookups, formatting, trivial edits |

Place as the final line of the system/role section, before the task body.

## Step 8.6: Inject Track Record Signal
Check `references/prompt-outcomes.jsonl` for past entries matching this task type + framework.

If 5+ entries exist: calculate success rate, inject "This framework has produced high-quality results on [N] of [M] similar [type] tasks."

If fewer than 5: skip. Invented track records are worse than none.

## Step 9: Self-Evaluate
Silently run this checklist:
- [ ] Can this be executed autonomously with zero follow-up questions?
- [ ] Does it specify the exact output format?
- [ ] Does it include success criteria?
- [ ] Does it anticipate the 2-3 most likely failure modes?
- [ ] Does it include all relevant file paths and references?
- [ ] Would a reasonably capable agent produce the right result on the first try?
- [ ] For coding tasks: plan-first step and elegance check included?
- [ ] Would a staff engineer be proud of the result?

If any answer is no, revise before presenting.

## Step 10: Present
Format per `templates/output-format.md`. Offer to run it immediately.
