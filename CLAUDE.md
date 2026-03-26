# repo-onboard

A Claude Code plugin that takes developers from "I have an idea" to a
structured project foundation through guided spec interviews.

See @docs/requirements.md for the full product spec.

## Plugin structure

```
repo-onboard/
├── .claude-plugin/
│   ├── plugin.json                          # Plugin metadata
│   └── marketplace.json                     # Marketplace listing
│
├── skills/
│   │
│   │ ── THE PIPELINE (one skill, progressive disclosure) ──
│   │
│   ├── project-onboard/                 # The main skill
│   │   ├── SKILL.md                     # Orchestrates the full pipeline
│   │   ├── references/
│   │   │   ├── requirements-phase.md    # How to run requirements interview
│   │   │   ├── review-phase.md          # How to review for gaps
│   │   │   ├── design-phase.md          # How to run design interview
│   │   │   ├── tasks-phase.md           # How to break into tasks
│   │   │   └── claude-md-phase.md       # How to generate CLAUDE.md
│   │   ├── assets/
│   │   │   ├── requirements-template.md # Output template for requirements
│   │   │   ├── design-template.md       # Output template for design
│   │   │   ├── tasks-template.md        # Output template for tasks
│   │   │   └── claude-md-template.md    # Output template for CLAUDE.md
│   │   └── examples/
│   │       └── repo-onboard.md          # Dogfooded: this project's own output
│   │
│   │ ── REVISE SKILLS (one per spec file) ──
│   │
│   ├── revise-requirements/
│   │   └── SKILL.md                     # Reads existing, asks what changed
│   ├── revise-design/
│   │   └── SKILL.md                     # Reads reqs + design, re-interviews
│   ├── revise-tasks/
│   │   └── SKILL.md                     # Reads reqs + design, regenerates
│   │
│   │ ── SUPPORTING SKILLS (auto-discovered by Claude) ──
│   │
│   ├── explore-system/
│   │   ├── SKILL.md
│   │   └── assets/
│   ├── investigate-bug/
│   │   ├── SKILL.md
│   │   └── assets/
│   ├── stakeholder-brief/
│   │   ├── SKILL.md
│   │   └── assets/
│   └── write-rfc/
│       ├── SKILL.md
│       └── assets/
│
├── CLAUDE.md
├── README.md
└── docs/
    └── requirements.md
```

## How the three types work

### project-onboard skill (the pipeline)

The single skill that runs the full onboarding process.
User invokes it with /project-onboard.

The SKILL.md contains the pipeline orchestration logic.
Each phase is a reference file loaded progressively:

1. Read references/requirements-phase.md → interview → save docs/requirements.md
2. Read references/review-phase.md → check for gaps → loop back if needed
3. Read references/design-phase.md → interview → save docs/design.md
4. Read references/tasks-phase.md → generate → save docs/tasks.md
5. Read references/claude-md-phase.md → generate → save CLAUDE.md

The SKILL.md tells Claude WHEN to load each reference:
"After saving requirements.md, read references/review-phase.md"
"After review passes, read references/design-phase.md"

Output templates live in assets/ — loaded when writing each file.

### Revise skills (separate, one per spec)

Each revise skill is its own directory because the revise workflow
differs from the pipeline:

- /revise-requirements: reads existing, asks what changed, rewrites ONE file
- /revise-design: reads reqs + design, re-interviews design only
- /revise-tasks: reads reqs + design, regenerates tasks (no interview)

No cascading. Revising requirements does NOT touch design or tasks.

### Supporting skills (auto-discovered)

Claude loads these on demand during normal development.
They produce read-only documents, never modify code.
No disable-model-invocation — Claude auto-triggers when relevant.

## Skill description rule

Every description must answer:
1. What does the skill do?
2. When should Claude use it?

## Output rules

- NEVER delete or overwrite files without asking
- CLAUDE.md: append if exists, create if not
- Revise skills overwrite ONLY their single target file

## Interview rules (for pipeline and revise)

- One question at a time, wait for full answer
- Push back on vague answers ("all of the above" → "pick one")
- Stay in lane (requirements phase doesn't discuss architecture)
- Flag uncertainty with confidence: high / medium / low

## What NOT to do

- Do NOT generate application code — only specs and docs
- Do NOT scan existing code (v1 is new projects only)
- Do NOT cascade: revising requirements does NOT auto-update design
- Do NOT assume — ask or flag with low confidence
