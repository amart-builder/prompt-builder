# Claude Prompt-Engineering Reference (Opus 4.8)

Distilled from Anthropic's prompting guidance + current (2026) prompt-engineering research. Use this to construct prompts in the `/prompt` skill. **Apply what fits — not all of it.**

**Contents:** Core techniques · Opus 4.8 specifics · What NOT to generate · Complexity gate · Prompt skeleton · Worked example

## Core techniques (apply what fits)
1. **Be clear and direct.** Spell out the output, format, and constraints. Treat Claude as a brilliant new hire with zero context. *Golden rule: if a colleague with no context would be confused, so will Claude.* Want "above and beyond"? Ask explicitly.
2. **Add context / motivation — the *why*.** Claude generalizes from the reason ("read aloud by TTS, so no ellipses" beats "never use ellipses").
3. **Use examples (multishot).** 3–5 in `<example>` tags; relevant, diverse, structured. If the user supplies examples, upgrade them to show the reasoning (input → reasoning → output), not just input → output.
4. **Structure with XML tags.** Separate the parts: `<instructions>`, `<context>`, `<input>`, `<examples>`, `<output_format>`.
5. **Role for tone only.** A one-line role sharpens voice/register — *not* factual accuracy (see debunked list).
6. **Output format: explicit + positive.** Removing format instructions reliably hurts quality; "write flowing prose" > "no bullets."
7. **Escape clause.** Tell the model what to do when unsure ("if you don't know, say so") — prevents confident wrong answers.
8. **Long inputs at the top, the question at the bottom** (can lift quality ~30%). Wrap docs in XML; for long docs, ask it to quote the relevant parts first.
9. **Self-check.** "Before finishing, verify against [criteria]."

## Opus 4.8 specifics
- **Literal follower** — state scope explicitly ("every section, not just the first").
- **Loves upfront specification** — a complete spec in one shot beats a vague ask dripped over turns. *(The reason this skill exists.)*
- **Reasons natively → CoT is conditional, not default.** On a model with built-in thinking, "think step by step" adds latency for ~+3% on hard reasoning. Add CoT only when the task is genuinely multi-step OR the user needs the reasoning *shown*.
- **Calibrates verbosity** to task complexity — say so if you need a specific length.
- **Action vs. suggestion** — "Write/Change this" makes it act; "can you suggest" makes it only advise.
- **Normal register, not caps** — "Use X when…" beats "CRITICAL: you MUST." Over-forceful prompts over-trigger.
- **No prefill** — prefilled assistant responses error on 4.6+; use explicit instruction or structured outputs instead.

## What NOT to generate (debunked by 2025–26 research)
- **Fake-expert personas for accuracy** — "you are a world-class physicist" gives no reliable accuracy gain (Wharton R4); mismatched personas can *hurt*. Roles are for tone/audience only.
- **Stakes / tips / threats** — "this is CRITICAL," "I'll tip you $200," "or I'll be fired" — no benchmark effect (Wharton R3). Cargo cult.
- **Reflexive chain-of-thought** on reasoning models (Wharton R2) — see above.
- **ALL-CAPS urgency** — over-triggers on 4.x.
- **Contradictions** — conflicting directives cost reasoning models more than older models. Scan the draft and resolve them.
- **Over-inflation** — more instructions ≠ better. Aim for the *smallest high-signal set* ("right altitude": specific enough to guide, flexible enough not to be brittle).

## Complexity gate (decide first)
- **Simple / lookup / quick edit** → a lean prompt: `<instructions>` + `<output_format>`. Stop there.
- **Complex / multi-step / compositional** → the fuller skeleton below; for long-horizon tasks, break into ordered sub-steps (decomposition) rather than one CoT blob.

## Prompt skeleton (fill in only what's needed)
```xml
<role>One line — tone/voice/audience (optional).</role>
<context>Why this matters · the situation · the audience.</context>
<instructions>
The task, stated clearly. Numbered steps if order matters. Explicit scope.
If unsure about anything, say so rather than guessing.
</instructions>
<input>The user's material / data, cleaned up. (Long data goes here, near the top.)</input>
<examples><example>…3–5 only if format/tone matters…</example></examples>
<output_format>Exactly what the output should look like — format, length, tone — stated positively.</output_format>
The actual request / question goes last.
Before finishing, verify: [success criteria].
```
A simple ask needs only `<instructions>` + `<output_format>`. Mark reusable swap-points (e.g. `{{topic}}`) so the prompt can be re-run later.

## Worked example
**Brain-dump in:**
> "ugh i need to email the investor who passed, the guy from Sequoia, keep the door open but not desperate, we just closed two big customers"

**Engineered prompt out:**
```xml
<role>You are Alex Martin writing a brief, self-assured founder update.</role>
<context>An investor passed earlier. Since then we closed two major customers —
proof the thesis is working. Goal: keep the relationship warm for a future round
without looking needy.</context>
<instructions>Write a 4–6 sentence email. Lead with the customer wins as news, not
a pitch. No explicit ask. Warm, confident, brief.</instructions>
<output_format>Plain email, no subject line. Flowing sentences, no bullets.</output_format>
Before finishing, verify: no desperation, no direct ask, wins stated as fact.
```
**Key choices:** role fixes voice; context explains the *why* (keeps it non-needy); positive format instruction.
