## Task Type Taxonomy & Frameworks

### 1. CODING / DEVELOPMENT

**Framework: Specification-Driven Development (SDD)**

Best for: building features, refactoring, adding integrations, writing scripts.

Claude excels at coding when given: explicit file paths, current behavior vs desired behavior, constraints, and a verification step.

**Template:**
```
## Task
[One sentence: what to build/change]

## Context
- Project: [name, tech stack, relevant architecture]
- Files involved: [exact paths]
- Current behavior: [what happens now]
- Desired behavior: [what should happen after]

## Requirements
1. [Specific requirement with acceptance criteria]
2. [Another requirement]
3. [Edge case to handle]

## Constraints
- Do not break: [existing functionality]
- Style: [match existing patterns in X file]
- Dependencies: [use existing deps only / OK to add]
- Minimal footprint: only touch files and code directly related to this change. No opportunistic refactors.

## Plan First
Before writing any code:
1. Write a brief plan (approach, files to touch, risks)
2. Confirm the plan makes sense before implementing
3. If something goes sideways mid-implementation, STOP and re-plan — don't keep pushing

## Test-Driven Development (TDD)
Write tests BEFORE implementation — red/green cycle:
1. Define the expected behavior as concrete test cases (unit tests, integration tests, or assertion scripts)
2. Run the tests — confirm they FAIL (red). If they pass before you write code, your tests are wrong.
3. Write the minimum implementation to make tests pass (green)
4. Refactor only after green — clean up without breaking tests
5. If the task doesn't have a natural test harness (e.g., UI design, config changes), write a verification script instead that asserts the desired end state.

This gives you a built-in definition of "done" — the tests pass — instead of self-assessing whether the code works.

## Verification
After implementation:
1. [How to test it works — run the TDD tests from above]
2. [How to confirm nothing broke]
3. Ask yourself: "Would a staff engineer be proud of this code?" If no, iterate before presenting.
4. Elegance check: if the solution feels hacky, step back — "Knowing everything you know now, implement the elegant solution."
5. **Failure Audit:** List every assumption you made during implementation that could be wrong. Rate each 1-10 on confidence. Surface anything rated <7 before presenting.

## Output
- Implement the changes directly
- Show a summary of what was changed and why
```

**Why this works:** Claude's coding performance improves dramatically with explicit file paths, before/after behavior descriptions, a plan-first step, and a verification pass that demands quality — not just correctness.

**Bad → Good example:**
- Bad: "add better error handling to my scraper"
- Good: See Examples section below

---

### 2. RESEARCH & ANALYSIS

**Framework: Structured Analytical Framework (SAF)**

Best for: evaluating tools/technologies, market research, competitive analysis, due diligence.

**Template:**
```
## Research Question
[Precise question to answer]

## Context
- Why this matters: [decision this informs]
- Current state: [what we know / use today]
- Decision timeline: [when we need to decide]

## Scope
- Evaluate: [specific things to look at]
- Ignore: [things explicitly out of scope]
- Depth: [surface scan / moderate / deep dive]

## Analysis Framework
For each option/finding, assess:
1. [Criterion 1 — e.g., technical fit]
2. [Criterion 2 — e.g., cost]
3. [Criterion 3 — e.g., maintenance burden]
4. [Criterion 4 — e.g., community/longevity]

## Output Format
1. Executive summary (3-5 sentences, bottom-line recommendation)
2. Comparison matrix (if evaluating options)
3. Evidence and reasoning for each assessment
4. Risks and unknowns
5. Recommended next step

## Success Criteria
The output is successful if the user can make a confident decision without further research.
```

**Why this works:** Research without structure produces meandering essays. The framework forces: a clear question, evaluation criteria defined upfront, and a decision-ready output format.

---

### 3. WRITING & DRAFTING

**Framework: Voice-Matched Composition (VMC)**

Best for: emails, messages, pitches, copy, documentation.

**Template:**
```
## Write
[What to write — type, audience, purpose]

## Voice & Tone
- Match: [the user's voice / formal / specific person's style]
- Tone: [casual warm / professional confident / urgent]
- Length: [target word count or "as short as possible"]
- Reference: [link to example of desired voice, or "read the user's recent sent emails"]

## Key Points to Include
1. [Must mention this]
2. [Must mention this]
3. [Optional: nice to include]

## Context the Reader Has
- They already know: [X, Y, Z]
- They don't know: [A, B]
- Their likely objection/concern: [C]

## Do NOT
- [Thing to avoid — e.g., "sound salesy"]
- [Another thing — e.g., "use jargon they won't know"]

## Output
- The draft, ready to send
- If multiple versions would help, provide 2 variants (concise vs detailed)
```

---

### 4. PLANNING & STRATEGY

**Framework: Decision Architecture (DA)**

Best for: business strategy, project planning, prioritization, pitch strategy, life decisions.

**Template:**
```
## Decision/Plan
[What we're trying to figure out or plan]

## Current Situation
- Where we are: [status quo]
- What's working: [strengths to preserve]
- What's not: [pain points, gaps]
- Resources available: [time, money, people, tools]

## Goals & Constraints
- Primary goal: [the one thing this must achieve]
- Secondary goals: [nice to haves]
- Hard constraints: [non-negotiables — budget, timeline, values]
- Soft constraints: [preferences, not dealbreakers]

## Options to Consider
[If known, list them. If not: "Generate 3-5 strategic options"]

## Analysis Request
For each option:
1. Pros and cons (honest, not balanced for the sake of balance)
2. Second-order effects (what happens 6 months later)
3. Reversibility (how hard to undo)
4. Resource requirements

## Role Collision (use when conflicting perspectives would surface real insight)
"Answer this as [role A] AND [role B] simultaneously. Show where they'd agree and where they'd sharply disagree."
- Example: "senior operator AND skeptical LP" / "technical co-founder AND conservative CFO"
- The disagreement section is where the actual insight lives — don't smooth it over.
- Use this when the prompt involves a strategic decision where two legitimate viewpoints would tension-test the recommendation.

## Output Format
1. Situation assessment (1 paragraph)
2. Options with analysis
3. Atlas's recommended path (with confidence level and reasoning)
4. Implementation roadmap (first 3 concrete steps)
5. Key risks and how to mitigate them
6. **Failure Audit:** What assumptions in this plan could be wrong? Rate each 1-10 confidence. Flag anything <7.

## Success Criteria
the user should finish reading and know exactly what to do next.
```

---

### 5. DATA TRANSFORMATION

**Framework: Pipeline Specification (PS)**

Best for: data cleaning, format conversion, CSV manipulation, API data processing, migrations.

**Template:**
```
## Transform
[What data, from what format, to what format]

## Input
- Source: [file path, API endpoint, or inline data]
- Format: [CSV, JSON, API response, etc.]
- Sample: [paste 2-3 rows or describe structure]
- Volume: [number of records]

## Output
- Destination: [file path, API, stdout]
- Format: [desired format with example of desired structure]
- Sample of desired output:
  [Show exactly what 1-2 transformed records should look like]

## Transformation Rules
1. [Field mapping: source_field → destination_field]
2. [Cleaning rule: e.g., "normalize phone numbers to E.164"]
3. [Filtering: e.g., "exclude records where status = inactive"]
4. [Enrichment: e.g., "look up company domain from name"]

## Edge Cases
- If [X is missing]: [do Y]
- If [format is unexpected]: [do Z]
- Duplicates: [keep first / keep latest / merge]

## Verification
- Run on first 5 records, show output for review before processing all
```

---

### 6. DEBUGGING & TROUBLESHOOTING

**Framework: Diagnostic Protocol (DP)**

Best for: fixing errors, investigating failures, performance issues, "why isn't this working."

**Template:**
```
## Problem
[What's broken — one sentence]

## Symptoms
- Expected behavior: [what should happen]
- Actual behavior: [what happens instead]
- Error message: [exact text, if any]
- When it started: [after what change, or "always"]

## Environment
- System: [OS, runtime, versions]
- Relevant config: [file paths or inline]
- Recent changes: [what changed before this broke]

## Already Tried
- [Thing 1 — result]
- [Thing 2 — result]
(Skip if nothing tried yet)

## Diagnostic Steps
1. Read the error and relevant source code
2. Form 2-3 hypotheses ranked by likelihood
3. Test most likely hypothesis first
4. Fix and verify — autonomously. Point at logs, errors, failing tests and resolve them. No hand-holding needed.

## Output
- Root cause explanation (not symptoms — the actual root cause)
- The fix (implemented, not "you might want to try...")
- No band-aids: if the fix feels temporary, find the real solution
- How to prevent recurrence
```

---

### 7. CREATIVE

**Framework: Creative Brief (CB)**

Best for: brainstorming, naming, design concepts, content ideas, unconventional solutions.

**Template:**
```
## Creative Challenge
[What we're trying to create or solve creatively]

## Inspiration & Direction
- Vibe: [words that capture the feel — e.g., "minimal, premium, slightly playful"]
- References: [things that capture the right energy — brands, products, styles]
- Anti-references: [things to NOT be like]

## Constraints That Enable Creativity
- Must: [non-negotiable requirements]
- Budget/scope: [boundaries]
- Audience: [who this is for and what they care about]

## Output
- Generate [N] options ranging from safe to bold
- For each: the idea + 2 sentences on why it works
- Star your top recommendation

## Evaluation Criteria
- [What makes a good answer — memorable? clear? unique?]
```

---

### 8. OUTREACH & RELATIONSHIP

**Framework: Relationship-Context Composition (RCC)**

Best for: LP outreach, investor follow-ups, warm intros, deal emails, Forge messaging, re-engagement after silence.

This is different from general writing. Outreach lives or dies on: knowing exactly where the relationship is, matching the energy of the prior exchange, and having one singular ask. Most outreach fails because it's generic. This framework prevents that.

**Template:**
```
## Outreach Goal
[One sentence: what you want from this message — specific outcome, not vague intent]

## Relationship Context
- Who: [name, role, company, how the user knows them]
- Last touchpoint: [when, what was said, their energy/engagement level]
- Their current situation: [job change, deal activity, relevant news if known]
- Relationship tier: [A1=inner circle / S1=strategic / D1-D3=network depth]
- Attio/CRM notes: [any relevant history]

## The Ask
- Primary: [one specific ask — intro, meeting, check-in, investment, feedback]
- Secondary: [softer fallback if primary is premature]
- NOT acceptable: vague asks like "let's connect," multiple asks, asks that require work from them

## Message Constraints
- Platform: [iMessage / Email / LinkedIn]
- Length: [2-4 sentences for text / 5-8 for email]
- Tone: [match their energy from last exchange]
- Do NOT: [pitch too hard / sound like a form letter / open with "I hope this email finds you well" / use em dashes]

## Context the Reader Has
- They already know: [X]
- They don't know: [Y — and should we tell them?]
- Their likely hesitation: [Z — address it or work around it?]

## Voice
- the user's voice: casual, warm, first-person, conversational, no em dashes, no corporate language
- If drafting email: read the user's recent sent emails to this person first

## Output
- 1 primary draft, ready to send with zero edits needed
- Optional: 1 alternate with a different hook or angle
- Flag if the ask feels premature given where the relationship is
```

**Why this framework exists:** Forge outreach is the highest-leverage, highest-frequency task in the system. Generic writing frameworks don't account for CRM state, relationship tier, or the energy of the last touchpoint. This one does. A bad outreach email is worse than no email.

---

### 9. AGENT ORCHESTRATION

**Framework: Context Bundle Protocol (CBP)**

Best for: spawning Opus or Codex sub-agents, writing tasks for isolated cron sessions, building agent payloads that need to run without Atlas supervision.

Sub-agent output quality is almost entirely determined by the quality of the context it wakes up with. Cold-start agents guess at the user's goals, voice, and constraints — producing off-target results that cost correction turns. This framework eliminates cold-start failure.

**Template:**
```
## ATLAS CONTEXT SNAPSHOT
Date/time: [current datetime, America/Los_Angeles]

### WHO YOU'RE WORKING FOR
[Key facts from memory/facts.md: the user's identity, active projects, key relationships, hard constraints]

### ALEX'S GOALS
[Relevant sections from GOALS.md]

### HARD CONSTRAINTS (non-negotiable — do not violate under any circumstances)
- NEVER start Gravity Bot or Sentinel Bot in live trading mode
- NEVER execute trades on Polymarket, Kalshi, or any exchange
- QuickBooks: read-only — never write, create, update, or delete any data
- Tasks go to Supabase REST API only (never Things 3 or Apple Reminders)
- No markdown on iMessage — plain text only
- Match the user's voice: casual, warm, first-person, no em dashes ever
- Never send emails, tweets, or public posts without explicit approval
- Never install skills/plugins without explicit approval

### CURRENT FOCUS
[Content of memory/working/current_focus.md]

### SESSION THREAD
[3-5 bullet summary of what Atlas and the user have been discussing — decisions made, context in flight]

### TASK CONTEXT
[Any project-specific files, entity data, or paths the agent will need]

## YOUR TASK
[The actual task — specific, bounded, with explicit success criteria]

## OUTPUT FORMAT
[Exactly what to produce: file to write, message to send, analysis to return]

## VERIFICATION
[How to confirm success before reporting done — run the test, read the file, confirm state changed]
```

**Why verification is mandatory in every orchestration prompt:** Sub-agents have a known failure mode of reporting "done" before checking if the thing actually worked. The verification step makes self-checking explicit and non-optional.

---
