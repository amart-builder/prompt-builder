---
name: prompt
description: >-
  Turns a messy brain-dump into a reusable, well-engineered prompt or build spec,
  shows it for approval, then runs it. Works for writing tasks (emails, summaries,
  docs) and build/do tasks (make a page, set up a repo, run an analysis). Use when
  the user types /prompt, asks Claude to "write or improve a prompt for this," or
  hands over a tangled brain-dump and wants help shaping it into a great result.
  Once invoked, run the full workflow including the approval gate; do not shortcut
  straight to doing the task. Do NOT auto-trigger on ordinary terse requests where
  the user clearly just wants the task done.
---

# Prompt: from brain-dump to great result

Turn raw, unorganized thoughts into an excellent outcome: **clarify → engineer the
prompt or spec → show it and get the OK → run it → verify.** This works whether the
goal is to *write* something (an email, a summary) or to *build or do* something (make a
page, set up a repo, run an analysis). Fable 5 does its best work from a clear, complete
spec given upfront and follows instructions literally, so the skill front-loads the messy
dump into the clean spec the model wants. Technique reference: `reference/prompt-engineering.md`.

## Workflow

### 1. Understand the dump
Read everything. Work out the *real* goal, the implied deliverable, and the audience.
Pull out the three things users usually leave implicit: the **task**, the **desired
output format/length/tone**, and **any examples** (or "what bad looks like") buried in
the dump. Note the assumptions you're making.

### 2. Clarify (only if it changes the output)
Ask **only when a missing detail would change the prompt itself** (different deliverable,
audience, scope, or format). Otherwise pick a sensible default, note it, and move on.

When you do ask, use the **AskUserQuestion** tool if available (not a chat list):
- 2 to 4 questions together; **4 is the ceiling, never a second round.**
- Multiple-choice with **your assumed default as the first option**, plus the free-text
  escape, so the user confirms your read in one click or corrects it.
- Frame it: "Here's how I'm reading this. Confirm or correct, then I build it."

**Skip the interview entirely** when the deliverable/audience/format are already clear,
it's a small or iterative ask, or any reasonable default would be fine. A clear dump
should pass straight through with zero questions. That's the goal, not the exception.
A cheap wrong guess beats a question that costs the user's attention.

### 3. Engineer the prompt (or build spec)
Build it using `reference/prompt-engineering.md`. **Right-size it.** Fable 5 follows
literally, so bloat hurts. Apply only what the task needs:
- Structure with XML tags, and **state the output format explicitly and positively.**
- Add a role only for **tone/voice/audience**, never as a fake "expert" accuracy boost.
- Add chain-of-thought / step-by-step **only** for genuinely multi-step tasks; skip it on
  simple ones (Fable 5 reasons natively, so default CoT is mostly latency).
- If the prompt involves tools, search, or other optional capabilities, state **when** to
  use each one ("when the answer depends on current info, search first"), not just that it
  exists. Fable 5 reaches for capabilities conservatively unless given trigger conditions.
- Include an **escape clause** ("if unsure, say so") and explicit **scope**.
- Before finishing, **scan for contradictions** and cut anything that isn't high-signal
  (right altitude: specific enough to guide, not so rigid it's brittle).

**Writing task vs build task.** If the goal is to *write* something, the artifact is a
**prompt**. If the goal is to *build or do* something (a page, a repo, an analysis,
multi-step work), the artifact is a tight **spec**: a goal stated so "done" is checkable,
the steps in order, the constraints, and how each step gets verified. Grant autonomy on
minor choices ("pick a reasonable default and note it") so the run doesn't stall on
questions. Same discipline, different shape. Either way, you show it and wait for
approval before doing the work.

### 4. Show it, get the OK, then run
1. **One plain-English line first.** Say what the prompt or spec does and the key choices
   ("pins your voice, explains the *why* so the tone stays right, locks the format").
2. **The prompt or spec in a code block.** Mandatory, every time. It is the reusable asset
   and the thing the user is approving. Do not hide it, summarize it away, or skip ahead to
   the work.
3. **Stop and wait for approval.** End your turn here. Ask: "Run this, or want to tweak it
   first?" Do not start the work until the user replies. This gate is the point of the
   skill. Never skip it, even when the answer seems obvious or the task is a build rather
   than a write. (The one exception: if the user explicitly told you to run without
   pausing, honor that.)
4. **On approval, run it.** Then **silently self-check** the result against the original
   dump (intent, every must-have and must-avoid, format and tone) and fix anything off
   *before* showing it. Don't ship a flawed draft and wait for the user to catch it.
5. Offer one quick refinement ("shorter / different tone / more detail?").

## Rules
- **Always show, always wait.** Put the prompt or spec in a code block and stop for approval
  before running. Non-optional, every time, whether writing or building. This is what makes
  the skill reliable, and it quietly levels the user up on prompting.
- **Once invoked, run the full workflow.** If the user typed /prompt or asked for prompt
  help, don't shortcut to just doing the task. Engineer the artifact, show it, and gate.
- **Default to passthrough on clarifying.** Ask only when it changes the output; never interrogate.
- **Right-size.** Simple ask, short prompt. Don't bolt on every technique.
- **No cargo-cult.** No fake-expert personas for accuracy, no stakes/tips/threats, no
  reflexive "think step by step." Research shows these don't help modern models. *Do*
  always keep explicit output-format instructions.
- **Positive beats negative** ("write flowing prose" over "don't use bullets").
