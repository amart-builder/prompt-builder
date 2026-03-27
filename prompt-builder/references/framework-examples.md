# Prompt Builder Reference: Framework Examples and Quality Heuristics

Use this file when you need concrete examples of generated prompts or stronger quality escalation language.

## Examples

### Example 1: Coding Task

**the user says:** "/prompt add better error handling to my scraper"

**Generated prompt:**

Task type: Coding | Framework: Specification-Driven Development

```
## Task
Add robust error handling to the X daily scraper (scripts/x-daily-scrape.py).

## Context
- Project: Atlas brain — X/Twitter daily intelligence pipeline
- File: scripts/x-daily-scrape.py
- Current behavior: Script runs via cron at 6:30am PT. When API calls fail or rate limits hit, the script crashes silently and no intelligence report is generated.
- Desired behavior: Script handles all failure modes gracefully, retries transient errors, and always produces at least a partial report or a clear failure notification.

## Requirements
1. Wrap all API calls in try/except with specific exception types (not bare except)
2. Implement exponential backoff retry (3 attempts) for rate limits (429) and server errors (5xx)
3. If all retries fail for a search term, log it and continue with remaining terms
4. At the end, if any searches failed, include a "Gaps" section in the output noting what was missed
5. If ALL searches fail (total API outage), send the user an iMessage: "X scraper failed completely — [error details]"
6. Add a timeout (30s) to each API request to prevent hanging

## Constraints
- Keep the existing output format for x-intelligence-latest.md
- Don't add new dependencies — use stdlib (urllib, time) for retry logic
- Match the existing code style

## Verification
1. Test with a valid run — output should be identical to current behavior
2. Simulate a 429 by temporarily using an invalid API key — should retry then report failure gracefully
3. Check that the cron job still works end-to-end
```

### Example 2: Research Task

**the user says:** "/prompt look into whether we should use langchain"

**Generated prompt:**

Task type: Research & Analysis | Framework: Structured Analytical Framework

```
## Research Question
Should we use LangChain in the Atlas system, or is our current direct-API approach better for our use case?

## Context
- Atlas is an AI life management system running on OpenClaw (Mac mini)
- Current approach: direct Anthropic API calls, custom scripts, OpenClaw skills
- We're not building a product — this is a personal AI system with specific integrations
- Decision timeline: Low urgency, but good to know for future architecture decisions

## Scope
- Evaluate: LangChain, LangGraph, and "no framework" (current approach)
- Also briefly consider: LlamaIndex, CrewAI, AutoGen as alternatives
- Depth: Moderate — enough to decide, not a PhD thesis
- Focus on: our specific use case (personal AI assistant with tool use, memory, multi-step tasks)

## Analysis Framework
For each option, assess:
1. Technical fit — does it solve problems we actually have?
2. Complexity cost — how much overhead does it add vs direct API calls?
3. Flexibility — can we still do custom things easily?
4. Maintenance burden — dependency updates, breaking changes, abstraction leakage
5. Community and longevity — will this exist and be maintained in 2 years?

## Output Format
1. Executive summary (recommend or not, in 3 sentences)
2. What LangChain actually gives us (concrete benefits for OUR setup)
3. What it costs us (concrete downsides for OUR setup)
4. Comparison matrix: LangChain vs LangGraph vs direct API vs one alternative
5. Bottom line recommendation with confidence level

## Success Criteria
the user finishes reading and knows whether to adopt LangChain, keep current approach, or explore a specific alternative.
```

### Example 3: Planning Task

**the user says:** "/prompt help me think through the edge fund pitch strategy"

**Generated prompt:**

Task type: Planning & Strategy | Framework: Decision Architecture

```
## Decision
Define the optimal pitch strategy for Example Company's next fundraising round — who to pitch, how to position, and in what sequence.

## Current Situation
- Example Company is the user's quantitative prediction markets fund
- Status: [Atlas reads from projects.md and fills in current AUM, track record, stage]
- What's working: [from context — e.g., Gravity bot performance, unique angle on prediction markets]
- What's not: [from context — e.g., small track record, niche market perception]
- Resources: the user (solo GP), Atlas (AI system for research/ops), existing investor network in Attio CRM

## Goals & Constraints
- Primary goal: Raise [target amount] from sophisticated investors who understand quantitative + prediction market strategies
- Secondary goals: Build relationships for future rounds, establish credibility in the space
- Hard constraints: Must be SEC compliant, the user is a solo GP (no team to show off), limited time for meetings
- Soft constraints: Prefer investors who add strategic value, not just capital

## Analysis Request
1. Investor segmentation: Who are the ideal targets? (type, size, thesis fit)
2. Positioning: How to frame Example Company's unique value prop for each segment
3. Pitch sequence: Who to approach first (warm intros vs cold, small checks vs anchors)
4. Materials needed: What pitch assets to prepare (deck, one-pager, data room)
5. Objection handling: Top 5 likely objections and how to address each
6. Timeline: Realistic fundraising timeline with milestones

## Output Format
1. Strategic assessment (1 paragraph — honest take on where we stand)
2. Target investor profiles (3-4 segments with examples)
3. Positioning strategy per segment
4. Recommended sequence and timeline
5. Action items: the first 5 concrete things to do this week
6. Risk factors and contingency plans

## Success Criteria
the user finishes reading with a clear, actionable fundraising playbook — not vague advice, but specific names, sequences, and talking points he can execute on.
```

## Meta-Principles Applied in Every Prompt

1. **Specificity over length** — every sentence earns its place
2. **Context injection** — relevant system state is woven in, not dumped
3. **Clear success criteria** — Atlas knows when it's done
4. **Output format specified** — no ambiguity about what the deliverable looks like
5. **Edge cases anticipated** — common failure modes addressed upfront
6. **Assumptions stated** — nothing hidden, everything auditable
7. **Autonomy-enabling** — the prompt is complete enough that Atlas never needs to ask follow-up questions
8. **Plan before execute** — for any 3+ step task, the prompt should include a plan-first step
9. **Minimal footprint** — changes touch only what's necessary; no opportunistic scope creep
10. **Demand elegance** — prompts should set a quality bar, not just a correctness bar

## Power Phrases (Include When Relevant)

- "Would a staff engineer be proud of this?" — use in coding/debugging Verification sections
- "Knowing everything you know now, implement the elegant solution." — use when the task has risk of hacky shortcuts
- "Prove to me this works." — use in Verification when correctness is critical
- "Find the root cause. No band-aids." — use in debugging prompts
- "If something goes sideways, STOP and re-plan — don't keep pushing." — use in complex multi-step coding tasks
