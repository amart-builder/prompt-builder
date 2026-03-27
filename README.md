# Prompt Builder — OpenClaw Skill

Turn 5 words into a 400-line execution-ready prompt.

This is an [OpenClaw](https://openclaw.ai) skill that transforms rough, incomplete requests into structured prompts with the right framework, context injection, and explicit success criteria.

## What It Does

You give it something vague like:
> "build me a landing page"

It outputs a complete prompt with:
- **Task classification** — coding, research, writing, planning, debugging, creative, outreach, orchestration, or data analysis
- **Expert identity** ("soul") — selects from 25+ expert personas backed by research on persona-based prompting
- **Framework template** — structured approach specific to the task type
- **Context injection** — pulls relevant system context automatically
- **Success criteria** — explicit, measurable, so you know when it's done
- **EmotionPrompt calibration** — adjusts intensity based on stakes

## Installation

### As an OpenClaw Skill

Copy the `prompt-builder/` directory into your OpenClaw skills folder:

```bash
# Clone this repo
git clone https://github.com/amart-builder/prompt-builder.git

# Copy into your OpenClaw workspace
cp -r prompt-builder/prompt-builder ~/.openclaw/workspace/skills/prompt-builder
```

Then use it in chat:
```
/prompt build a REST API for a todo app with auth
```

### Standalone

The skill files are plain markdown. You can use them with any AI assistant:

1. Feed `prompt-builder/SKILL.md` as system instructions
2. Feed the `instructions/` files for the full taxonomy and procedure
3. Feed `references/soul-library.md` for expert persona selection

## Skill Structure

```
prompt-builder/
├── SKILL.md                          # Entry point
├── instructions/
│   ├── procedure.md                  # 10-step generation process
│   ├── taxonomy.md                   # 9 task types with frameworks
│   └── context-injection.md          # How to load relevant context
├── references/
│   ├── soul-library.md               # 25+ expert identities
│   ├── framework-templates.md        # Structured templates per task type
│   ├── framework-examples.md         # 3 worked examples with commentary
│   └── prompt-library/
│       └── README.md                 # Saved prompt library structure
├── templates/
│   └── output-format.md              # Presentation format
└── evals/
    └── evals.json                    # 18 test cases
```

## Task Types

| Type | Code | Framework | Best For |
|------|------|-----------|----------|
| Coding | SDD | Structured Design Doc | Building features, debugging, refactoring |
| Research | SAF | Structured Analytical Framework | Deep dives, comparisons, evaluations |
| Writing | VMC | Voice-Matched Composition | Content, emails, copywriting |
| Planning | DA | Decision Architecture | Strategy, roadmaps, goal-setting |
| Data Analysis | PS | Pattern Synthesis | Data transforms, analysis, reporting |
| Debugging | DP | Diagnostic Protocol | Root cause analysis, troubleshooting |
| Creative | CB | Creative Brief | Design, brainstorming, ideation |
| Outreach | RCC | Relationship-Context Communication | Emails, DMs, introductions |
| Orchestration | CBP | Coordination Blueprint | Multi-agent, workflow, pipeline design |

## The Soul Library

The skill includes 25+ expert identities across 12 categories, backed by research from:
- Salewski et al. (2023) — "In-Context Impersonation"
- Li et al. (2023) — "EmotionPrompt"
- Wang et al. (2023) — "Persona-based Prompting"
- Reynolds & McDonell (2021) — "Prompt Programming for Large Language Models"
- Shanahan et al. (2023) — "Role play with large language models"

The soul selection isn't random — it uses a decision framework based on task complexity, domain depth, and creative requirements.

## Examples

**Input:** `build a scraper that handles rate limits gracefully`

**Output:** A complete SDD (Structured Design Doc) prompt with:
- Error handling soul selected (Systems Architect + Defensive Programming)
- Explicit rate limit patterns (exponential backoff, circuit breaker)
- Test scenarios for failure modes
- Success criteria: "handles 429s without data loss, resumes cleanly after outages"

See `references/framework-examples.md` for 3 full worked examples.

## License

MIT — use it however you want.

## Author

Built by [amart](https://x.com/amartAI) as part of the Atlas AI system.
