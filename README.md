# /prompt — turn a brain-dump into a great result

A Claude skill that takes your messy, unorganized thoughts and turns them into an
excellent outcome: **clarify → engineer the prompt → run it → verify.**

You don't write the perfect prompt. You brain-dump everything in your head — messy is
fine — and the skill builds the clean, complete prompt that modern Claude does its best
work from, then runs it for you.

## What it does

When you type `/prompt` and dump your thoughts, the skill:

1. **Reads the dump** and works out the real goal, the deliverable, and the audience.
2. **Clarifies only if it matters** — asks a question *only* when a missing detail would
   change the result. A clear dump passes straight through with zero questions.
3. **Engineers the prompt** using current prompt-engineering research — right-sized to the
   task, with explicit output format, the *why* behind the request, and an escape clause.
4. **Runs it and self-checks** the result against your original intent before showing you.

## Philosophy

This is the **anti-cargo-cult** version. Based on Anthropic's prompting guidance plus
2025–26 research (incl. Wharton's controlled studies), it deliberately *skips* the things
that don't actually help modern reasoning models:

- ❌ No fake "you are a world-class expert" personas (no reliable accuracy gain)
- ❌ No stakes / tips / threats / "this is CRITICAL" (no benchmark effect)
- ❌ No reflexive "think step by step" (adds latency on models that already reason)
- ✅ Always keeps explicit output-format instructions, context/motivation, and right-sizing

It defaults to the *smallest high-signal prompt* the task needs — not the longest.

## Install

### Claude Code / Claude Cowork

Paste this into a fresh chat and let Claude do it:

```
Install a custom skill called "prompt" from GitHub:

1. Clone https://github.com/amart-builder/prompt-builder into a temp folder.
2. Create the directory ~/.claude/skills/ if it doesn't exist.
3. Copy the repo's prompt/ folder to ~/.claude/skills/prompt
   (so the files end up at ~/.claude/skills/prompt/SKILL.md and
   ~/.claude/skills/prompt/reference/prompt-engineering.md).
4. Confirm both files are in place and tell me the skill is installed.

Then I'll restart the chat so /prompt shows up.
```

After it finishes, **start a new chat** so `/prompt` appears in autocomplete.

### OpenClaw

The same `SKILL.md` format works as an OpenClaw skill — copy the `prompt/` directory into
your OpenClaw skills folder.

## How to use it

You don't need it every time. Use it **when the output really matters.**

```
/prompt  then brain-dump everything in your head — messy is fine.
```

Example dump:

> "ugh i need to email the practice owner who went quiet after our call, keep it warm,
> remind her we have two other buyers interested but don't sound pushy"

The skill turns that into a clean, complete prompt and writes the email — checking it
against your intent before showing you.

## What's in here

```
prompt/
  SKILL.md                      the skill instructions (workflow + rules)
  reference/
    prompt-engineering.md       the technique reference it builds prompts from
```

---

Maintained by [@amart-builder](https://github.com/amart-builder). Built for the Martin
Healthcare Advisors team and anyone who wants higher-quality output from Claude.
