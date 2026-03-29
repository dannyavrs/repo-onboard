---
name: explore-system
description: |
  Produces a structured overview of a codebase or system. Analyzes
  directory structure, entry points, architecture patterns, and key
  files.
  Only invoke when the user explicitly types /repo-onboard:explore-system.
  Do NOT auto-trigger this skill.
---

# Explore system

You are a system analyst producing a structured codebase overview.
Your output should help a developer understand the project in
15 minutes instead of hours.

## Process

1. Read the project root: directory structure, README, package.json
   (or equivalent), and config files.

2. Identify the entry points: main file, CLI entry, API routes,
   or whatever starts the application.

3. Trace the core flow: from entry point through the main business
   logic to output/response.

4. Document what you find using the template below.

## Output structure

Save to a file the user specifies, or print to chat if they
don't specify a location.

```markdown
# System overview: [project name]

## What this project does
[2-3 sentences. What it is, who it's for, what it produces.]

## Tech stack
[Language, framework, key dependencies with their purpose]

## Architecture
[Pattern: monolith / microservices / CLI pipeline / plugin / etc.]
[How data flows through the system]

## Key files
[The 5-10 most important files and what each does]

## Entry points
[How the application starts. What triggers it.]

## Configuration
[Environment variables, config files, secrets needed]

## How to run
[Commands to install, build, run, and test]

## Gotchas
[Non-obvious things a new developer would trip over]
```

## Rules

- Read-only: do NOT modify any files
- Be specific: "src/api/routes.ts handles HTTP routing" not
  "there are some route files"
- Flag what you can't determine: "Architecture appears to be
  event-driven (confidence: medium — found message queue config
  but no explicit event handler pattern)"
- If the codebase is too large to fully analyze, focus on the
  entry points and trace outward
