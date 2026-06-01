---
name: prompt
description: >-
  Turns a messy brain-dump into a reusable, well-engineered prompt, then runs it.
  Use when the user explicitly types /prompt, asks Claude to "write or improve a
  prompt for this," or hands over a large tangled brain-dump and explicitly wants
  help shaping it into a great result. This is a meta-tool that adds a clarify-then-
  engineer step in front of the work. Do NOT use it for ordinary requests that
  happen to be casual or terse — if the user clearly wants the task done directly,
  just do the task. Prefer it only when prompt-craft itself is the point.
---

# Prompt — brain-dump → great result

Turn raw, unorganized thoughts into an excellent outcome: **clarify → engineer the
prompt → run it → verify.** Opus 4.8 does its best work from a clear, complete spec
given upfront, and follows instructions literally — so this skill front-loads the messy
dump into the clean spec the model wants. Technique reference: `reference/prompt-engineering.md`.

## Workflow

### 1. Understand the dump
Read everything. Work out the *real* goal, the implied deliverable, and the audience.
Pull out the three things users usually leave implicit: the **task**, the **desired
output format/length/tone**, and **any examples** (or "what bad looks like") buried in
the dump. Note the assumptions you're making.

### 2. Clarify — only if it changes the output
Ask **only when a missing detail would change the prompt itself** (different deliverable,
audience, scope, or format). Otherwise pick a sensible default, note it, and move on.

When you do ask, use the **AskUserQuestion** tool if available (not a chat list):
- 2–4 questions together; **4 is the ceiling, never a second round.**
- Multiple-choice with **your assumed default as the first option**, plus the free-text
  escape — so the user confirms your read in one click or corrects it.
- Frame it: "Here's how I'm reading this — confirm or correct, then I build it."

**Skip the interview entirely** when the deliverable/audience/format are already clear,
it's a small or iterative ask, or any reasonable default would be fine. A clear dump
should pass straight through with zero questions — that's the goal, not the exception.
A cheap wrong guess beats a question that costs the user's attention.

### 3. Engineer the prompt
Build it using `reference/prompt-engineering.md`. **Right-size it** — Opus 4.8 follows
literally, so bloat hurts. Apply only what the task needs:
- Structure with XML tags; **state the output format explicitly and positively.**
- Add a role only for **tone/voice/audience** — never as a fake "expert" accuracy boost.
- Add chain-of-thought / step-by-step **only** for genuinely multi-step tasks; skip it on
  simple ones (Opus 4.8 reasons natively — default CoT is mostly latency).
- Include an **escape clause** ("if unsure, say so") and explicit **scope**.
- Before finishing, **scan the prompt for contradictions** and cut anything that isn't
  high-signal ("right altitude" — specific enough to guide, not so rigid it's brittle).

### 4. Show, run, and verify
1. **One plain-English line first** — what the prompt does and the key choices ("pins your
   voice, explains the *why* so the tone stays right, locks the format").
2. **The prompt in a code block** — the reusable asset. Frame it opt-in: "glance if you
   want, or just let me run it." Don't make it feel like homework.
3. **Run it.** Then **silently self-check** the result against the original dump — intent,
   every must-have/must-avoid, format/tone — and fix anything off *before* showing it.
   Don't ship a flawed draft and wait for the user to catch it.
4. Offer one quick refinement ("shorter / different tone / more detail?").

## Rules
- **Default to passthrough.** Clarify only when it changes the output; never interrogate.
- **Right-size.** Simple ask → short prompt. Don't bolt on every technique.
- **No cargo-cult.** No fake-expert personas for accuracy, no stakes/tips/threats, no
  reflexive "think step by step" — research shows these don't help modern models. *Do*
  always keep explicit output-format instructions.
- **Positive beats negative** ("write flowing prose" > "don't use bullets").
- **Surface the prompt** (plain-English first) — it quietly levels the user up on prompting.
