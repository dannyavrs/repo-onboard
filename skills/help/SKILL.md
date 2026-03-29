---
name: help
description: |
  Shows all available repo-onboard skills with their slash commands
  and descriptions. Only invoke when the user explicitly types
  repo-onboard:help. Do NOT auto-trigger this skill.
---

# repo-onboard — available skills

Here are all the skills you can use:

## Pipeline

| Command | Description |
|---------|-------------|
| `repo-onboard:project-onboard` | Guided spec interview through 5 phases — requirements, review, design, tasks, and CLAUDE.md generation. Start here for new projects. |

## Revise

| Command | Description |
|---------|-------------|
| `repo-onboard:revise-requirements` | Re-interview and update docs/requirements.md only. |
| `repo-onboard:revise-design` | Re-interview and update docs/design.md only. |
| `repo-onboard:revise-tasks` | Regenerate docs/tasks.md from current specs. No interview needed. |

## Supporting tools

| Command | Description |
|---------|-------------|
| `repo-onboard:explore-system` | Structured codebase overview — understand a project in 15 minutes. |
| `repo-onboard:investigate-bug` | Bug investigation report with root cause, impact, and fix options. |
| `repo-onboard:stakeholder-brief` | Translate technical decisions into a non-technical stakeholder brief. |
| `repo-onboard:write-rfc` | Document a technical decision with alternatives and tradeoffs. |
| `repo-onboard:help` | Show this help message. |

Print this table to the user. Do not add anything else.
