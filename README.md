# repo-onboard

**repo-onboard turns your messy idea into structured specs. Claude Code's plan mode does the rest — and it does it 10x better with specs than without.**

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

### Option 1: Install as a marketplace plugin (recommended)

Inside Claude Code, run:

```
/plugin marketplace add dannyavrs/repo-onboard
```

Then install the plugin:

```
/plugin install repo-onboard@dannyavrs
```

You'll be prompted to choose the scope (user, project, or local).

### Option 2: Install from local directory

Clone the repo and point Claude Code at it:

```bash
git clone https://github.com/dannyavrs/repo-onboard.git
claude --plugin-dir ./repo-onboard
```

### Option 3: Manual copy

Clone and copy the skill files directly into your project:

```bash
git clone https://github.com/dannyavrs/repo-onboard.git
cp -r repo-onboard/.claude/skills/ your-project/.claude/skills/
```

### Verify installation

Open Claude Code and run `/reload-plugins`, then type:

```
repo-onboard:project-onboard
```

If the skill loads and starts asking about your project idea, you're set.

## Usage

Type `repo-onboard:help` to see all available commands.

### All commands

| Command | Description |
|---------|-------------|
| `repo-onboard:project-onboard` | Guided spec interview through 5 phases — requirements, review, design, tasks, and CLAUDE.md. Start here for new projects. |
| `repo-onboard:revise-requirements` | Re-interview and update docs/requirements.md only. |
| `repo-onboard:revise-design` | Re-interview and update docs/design.md only. |
| `repo-onboard:revise-tasks` | Regenerate docs/tasks.md from current specs. No interview needed. |
| `repo-onboard:explore-system` | Structured codebase overview — understand a project in 15 minutes. |
| `repo-onboard:investigate-bug` | Bug investigation report with root cause, impact, and fix options. |
| `repo-onboard:stakeholder-brief` | Translate technical decisions into a non-technical stakeholder brief. |
| `repo-onboard:write-rfc` | Document a technical decision with alternatives and tradeoffs. |
| `repo-onboard:help` | Show all available skills and how to call them. |

All skills are manually invoked — none auto-trigger. Each revise command updates **only its target file**. Revising requirements does NOT auto-update design or tasks — you decide when to cascade changes.

## Plugin structure

```
repo-onboard/
├── .claude-plugin/
│   ├── plugin.json                          # Plugin metadata
│   └── marketplace.json                     # Marketplace listing
├── skills/                                  # All plugin skills (root level)
│   ├── project-onboard/                     # Main pipeline skill
│   │   ├── SKILL.md                         # Orchestrates the 5 phases
│   │   ├── references/
│   │   │   ├── requirements-phase.md        # How to run requirements interview
│   │   │   ├── review-phase.md              # How to review for gaps
│   │   │   ├── design-phase.md              # How to run design interview
│   │   │   ├── tasks-phase.md               # How to break into tasks
│   │   │   └── claude-md-phase.md           # How to generate CLAUDE.md
│   │   ├── assets/
│   │   │   ├── requirements-template.md     # Output template for requirements
│   │   │   ├── design-template.md           # Output template for design
│   │   │   ├── tasks-template.md            # Output template for tasks
│   │   │   └── claude-md-template.md        # Output template for CLAUDE.md
│   │   └── examples/
│   │       └── repo-onboard.md              # Dogfooded: this project's own output
│   ├── revise-requirements/                 # Revise requirements only
│   ├── revise-design/                       # Revise design only
│   ├── revise-tasks/                        # Revise tasks only
│   ├── explore-system/                      # Codebase overview skill
│   ├── investigate-bug/                     # Bug investigation skill
│   ├── stakeholder-brief/                   # Non-technical briefing skill
│   ├── write-rfc/                           # Technical decision document skill
│   └── help/                                # Lists all available skills
├── docs/
│   └── requirements.md                      # This project's own requirements
├── CLAUDE.md                                # Claude Code instructions for this repo
├── README.md
└── LICENSE
```

## How it works

The plugin uses **progressive disclosure** — Claude never loads all phases into context at once. The main `SKILL.md` orchestrates the pipeline and tells Claude when to load each reference file:

```
repo-onboard:project-onboard invoked
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

After running `repo-onboard:project-onboard`, your project directory looks like:

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

repo-onboard is a project initiation tool. It produces specs
and configuration. It does NOT generate code, analyze existing
repos, enforce specs during development, or auto-update docs
when code changes. It gives you the best possible starting
point. What you build from there is up to you.

All skills are manually invoked — they never auto-trigger.
You invoke them explicitly when you need them.

## Built with

- Claude Code plugin system
- Progressive disclosure architecture
- No TypeScript, no build step, no API wrappers — just Markdown

## Dogfooding

This project's own specs were generated using this tool. See `docs/requirements.md` for the output.

## License

MIT
