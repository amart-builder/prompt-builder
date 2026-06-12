# Claude Prompt-Engineering Reference (Fable 5)

Distilled from Anthropic's prompting guidance + current (2026) prompt-engineering research, tuned for Claude Fable 5. Most of this also applies to recent Opus models (4.6+), which share Fable 5's instruction-following character. Use this to construct prompts in the `/prompt` skill. **Apply what fits, not all of it.**

**Contents:** Core techniques · Fable 5 specifics · What NOT to generate · Complexity gate · Prompt skeleton · Build-spec skeleton · Worked example

## Core techniques (apply what fits)
1. **Be clear and direct.** Spell out the output, format, and constraints. Treat Claude as a brilliant new hire with zero context. *Golden rule: if a colleague with no context would be confused, so will Claude.* Want "above and beyond"? Ask explicitly.
2. **Add context / motivation, the *why*.** Claude generalizes from the reason ("read aloud by TTS, so no ellipses" beats "never use ellipses").
3. **Use examples (multishot).** 3 to 5 in `<example>` tags; relevant, diverse, structured. If the user supplies examples, upgrade them to show the reasoning (input → reasoning → output), not just input → output.
4. **Structure with XML tags.** Separate the parts: `<instructions>`, `<context>`, `<input>`, `<examples>`, `<output_format>`.
5. **Role for tone only.** A one-line role sharpens voice/register, *not* factual accuracy (see debunked list).
6. **Output format: explicit + positive.** Removing format instructions reliably hurts quality; "write flowing prose" > "no bullets."
7. **Escape clause.** Tell the model what to do when unsure ("if you don't know, say so"). Prevents confident wrong answers.
8. **Long inputs at the top, the question at the bottom** (can lift quality ~30%). Wrap docs in XML; for long docs, ask it to quote the relevant parts first.
9. **Self-check.** "Before finishing, verify against [criteria]."

## Fable 5 specifics
- **Literal, precise follower.** It does what the prompt says, not what it guesses you meant. State scope explicitly ("every section, not just the first"); it won't silently generalize one instruction to a neighboring case.
- **Loves upfront specification.** A complete spec in one shot beats a vague ask dripped over turns; from a clear goal it plans better and finishes long tasks more efficiently. *(The reason this skill exists.)*
- **Reasons natively → CoT is conditional, not default.** On a model with built-in thinking, "think step by step" adds latency for ~+3% on hard reasoning. Add CoT only when the task is genuinely multi-step OR the user needs the reasoning *shown*.
- **Conservative about optional capabilities.** It won't reach for tools, search, or subagents unless reasonably sure they're needed. If the prompt involves a capability, state *when* to use it ("when the answer depends on current information, search before answering"), not just that it exists. Trigger conditions give measurable lift.
- **Deliberate; asks more than older models.** For prompts or specs meant to run without back-and-forth, grant autonomy on the small stuff: "For minor choices (naming, defaults, equivalent approaches), pick a reasonable option and note it rather than asking." Keep the ask-first rule for scope changes and destructive actions.
- **Calibrates verbosity to task complexity, and narrates its work more by default.** Say so if you need a specific length, or a quiet final-answer-only response.
- **Action vs. suggestion.** "Write/Change this" makes it act; "can you suggest" makes it only advise.
- **Normal register, not caps.** "Use X when…" beats "CRITICAL: you MUST." Over-forceful prompts over-trigger.
- **No prefill.** Prefilled assistant responses error on Fable 5 and every model since 4.6; use explicit instructions or structured outputs instead.

## What NOT to generate (debunked by 2025-26 research)
- **Fake-expert personas for accuracy.** "You are a world-class physicist" gives no reliable accuracy gain (Wharton R4); mismatched personas can *hurt*. Roles are for tone/audience only.
- **Stakes / tips / threats.** "This is CRITICAL," "I'll tip you $200," "or I'll be fired": no benchmark effect (Wharton R3). Cargo cult.
- **Reflexive chain-of-thought** on reasoning models (Wharton R2). See above.
- **ALL-CAPS urgency.** Over-triggers on modern Claude.
- **Contradictions.** Conflicting directives cost reasoning models more than older models. Scan the draft and resolve them.
- **Over-inflation.** More instructions ≠ better. Aim for the *smallest high-signal set* ("right altitude": specific enough to guide, flexible enough not to be brittle).

## Complexity gate (decide first)
- **Simple / lookup / quick edit** → a lean prompt: `<instructions>` + `<output_format>`. Stop there.
- **Complex / multi-step / compositional** → the fuller skeleton below; for long-horizon tasks, break into ordered sub-steps (decomposition) rather than one CoT blob.

## Prompt skeleton (fill in only what's needed)
```xml
<role>One line: tone/voice/audience (optional).</role>
<context>Why this matters · the situation · the audience.</context>
<instructions>
The task, stated clearly. Numbered steps if order matters. Explicit scope.
If unsure about anything, say so rather than guessing.
</instructions>
<input>The user's material / data, cleaned up. (Long data goes here, near the top.)</input>
<examples><example>…3 to 5 only if format/tone matters…</example></examples>
<output_format>Exactly what the output should look like (format, length, tone), stated positively.</output_format>
The actual request / question goes last.
Before finishing, verify: [success criteria].
```
A simple ask needs only `<instructions>` + `<output_format>`. Mark reusable swap-points (e.g. `{{topic}}`) so the prompt can be re-run later.

## Build-spec skeleton (for build/do tasks)
```
Goal: what "done" looks like, stated so it can be checked
      ("a CSV with a numeric price column per SKU", not "good data").
Steps: in order, each with how it gets verified.
Constraints: what's in scope, what's off-limits, what must not change.
Autonomy: for minor choices, pick a reasonable default and note it;
          ask only on scope changes or destructive actions.
```
A checkable "done" gives Fable 5 a target to work toward instead of guessing when to stop.

## Worked example
**Brain-dump in:**
> "ugh i need to email the investor who passed, the guy from Sequoia, keep the door open but not desperate, we just closed two big customers"

**Engineered prompt out:**
```xml
<role>You are Alex Martin writing a brief, self-assured founder update.</role>
<context>An investor passed earlier. Since then we closed two major customers,
proof the thesis is working. Goal: keep the relationship warm for a future round
without looking needy.</context>
<instructions>Write a 4 to 6 sentence email. Lead with the customer wins as news, not
a pitch. No explicit ask. Warm, confident, brief.</instructions>
<output_format>Plain email, no subject line. Flowing sentences, no bullets.</output_format>
Before finishing, verify: no desperation, no direct ask, wins stated as fact.
```
**Key choices:** role fixes voice; context explains the *why* (keeps it non-needy); positive format instruction.
