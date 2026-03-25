# repo-onboard

**From idea to structured project — before writing any code.**

A Claude Code plugin that guides developers through a structured spec interview, producing professional requirements, design, tasks, and CLAUDE.md. Built for developers who have a project idea but no code yet.

## What it does

You run one command. It interviews you like a senior system analyst.
When it's done, you have:

- `docs/requirements.md` — what you're building and why
- `docs/design.md` — how you're building it
- `docs/tasks.md` — the order to build it
- `CLAUDE.md` — best-practice Claude Code configuration
- `.claude/skills/` — supporting tools for ongoing development

Open Claude Code. It reads CLAUDE.md automatically. Start building.

## Installation

### From GitHub (recommended)

```bash
claude plugin add https://github.com/dannyavrs/repo-onboard
```

This installs the plugin and all its skills into your Claude Code environment.

### Manual installation

1. Clone the repository:
   ```bash
   git clone https://github.com/dannyavrs/repo-onboard.git
   ```

2. Copy the `.claude/` directory into your Claude Code plugins folder:
   ```bash
   cp -r repo-onboard/.claude ~/.claude/plugins/repo-onboard
   ```

3. Or symlink it for development:
   ```bash
   ln -s "$(pwd)/repo-onboard/.claude" ~/.claude/plugins/repo-onboard
   ```

### Verify installation

Open Claude Code and type:
```
/project-onboard
```
If the skill loads and starts asking about your project idea, you're set.

## Usage

### Start a new project

```
/project-onboard
```

Runs the full 5-phase pipeline:

1. **Requirements interview** — who is this for, what problem does it solve, what does success look like
2. **Review** — checks your requirements for gaps and contradictions
3. **Design interview** — data flow, architecture, dependencies, tech stack
4. **Task breakdown** — phased, ordered tasks with acceptance criteria
5. **CLAUDE.md generation** — best-practice configuration for Claude Code

The interview asks **one question at a time** and pushes back on vague answers. It flags uncertainty with confidence scores instead of guessing.

### Revise specs later

```
/revise-requirements    # Re-interview requirements, update that file only
/revise-design          # Re-interview design, update that file only
/revise-tasks           # Regenerate tasks from current specs
```

Each revise command updates **only its target file**. Revising requirements does NOT auto-update design or tasks — that's intentional. You decide when to cascade changes.

### Supporting skills (installed automatically)

After running the pipeline, these skills are installed in your project and Claude uses them automatically when relevant:

| Skill | What it does | When Claude uses it |
|---|---|---|
| **explore-system** | Structured codebase overview | When you ask to understand a project |
| **investigate-bug** | Bug diagnosis readable by managers | When you report a bug or say "this isn't working" |
| **stakeholder-brief** | Translate tech decisions to business language | When you need to explain something to non-technical people |
| **write-rfc** | Document technical decisions with alternatives | When you're choosing between approaches |

## Plugin structure

```
repo-onboard/
├── .claude/
│   ├── plugin.json                          # Plugin metadata
│   ├── settings.json                        # Plugin settings
│   └── skills/
│       ├── project-onboard/                 # Main pipeline skill
│       │   ├── SKILL.md                     # Orchestrates the 5 phases
│       │   ├── references/
│       │   │   ├── requirements-phase.md    # How to run requirements interview
│       │   │   ├── review-phase.md          # How to review for gaps
│       │   │   ├── design-phase.md          # How to run design interview
│       │   │   ├── tasks-phase.md           # How to break into tasks
│       │   │   └── claude-md-phase.md       # How to generate CLAUDE.md
│       │   ├── assets/
│       │   │   ├── requirements-template.md # Output template for requirements
│       │   │   ├── design-template.md       # Output template for design
│       │   │   ├── tasks-template.md        # Output template for tasks
│       │   │   └── claude-md-template.md    # Output template for CLAUDE.md
│       │   └── examples/
│       │       └── repo-onboard.md          # Dogfooded: this project's own output
│       ├── revise-requirements/             # Revise requirements only
│       ├── revise-design/                   # Revise design only
│       ├── revise-tasks/                    # Revise tasks only
│       ├── explore-system/                  # Codebase overview skill
│       ├── investigate-bug/                 # Bug investigation skill
│       ├── stakeholder-brief/               # Non-technical briefing skill
│       └── write-rfc/                       # Technical decision document skill
├── docs/
│   └── requirements.md                      # This project's own requirements
├── CLAUDE.md                                # Claude Code instructions for this repo
├── README.md
└── LICENSE
```

## How it works

The plugin uses **progressive disclosure** — Claude never loads all phases into context at once. The main `SKILL.md` orchestrates the pipeline and tells Claude when to load each reference file:

```
/project-onboard invoked
  → SKILL.md loaded (orchestration logic)
    → Phase 1: loads requirements-phase.md → interviews → saves docs/requirements.md
    → Phase 2: loads review-phase.md → checks for gaps → loops back if needed
    → Phase 3: loads design-phase.md → interviews → saves docs/design.md
    → Phase 4: loads tasks-phase.md → generates → saves docs/tasks.md
    → Phase 5: loads claude-md-phase.md → generates → saves CLAUDE.md
    → Installs supporting skills into .claude/skills/
  → Done
```

Output templates in `assets/` ensure consistent document structure. Every line in the generated docs traces back to something the user said during the interview.

## Philosophy

Most developers skip straight from idea to code. This tool forces the questions that prevent spaghetti:

- **Who is this for?** Not "developers" — which developers, doing what?
- **What does success look like?** Not features — measurable outcomes.
- **What's out of scope?** The hardest question. The one that keeps v1 shippable.

The interview pushes back on vague answers. It flags uncertainty with confidence scores instead of guessing. It stays in its lane — requirements don't discuss architecture, design doesn't revisit user personas.

The tool's responsibility ends when the files are generated. What you build after that is up to you.

## Generated output example

After running `/project-onboard`, your project directory looks like:

```
my-project/
├── docs/
│   ├── requirements.md    # Problem, user, success criteria, journey, edge cases
│   ├── design.md          # Architecture, data model, interfaces, tech stack, risks
│   └── tasks.md           # Phased tasks with acceptance criteria and estimates
├── CLAUDE.md              # Project overview, commands, structure, code style, constraints
├── .claude/
│   └── skills/            # explore-system, investigate-bug, stakeholder-brief, write-rfc
└── README.md
```

Each document includes **confidence scores** (high/medium/low) on every section, so you know where to validate before building.

## Scope boundary

repo-onboard is a project initiation tool. It produces specs and configuration. It does NOT:

- Generate application code
- Analyze existing repositories (v1 is new projects only)
- Enforce specs during development
- Auto-update docs when code changes

## Built with

- Claude Code plugin system
- Progressive disclosure architecture
- No TypeScript, no build step, no API wrappers — just Markdown

## Dogfooding

This project's own specs were generated using this tool. See `docs/requirements.md` for the output.

## License

MIT
