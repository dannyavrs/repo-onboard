---
name: revise-tasks
description: |
  Regenerates the task breakdown from current specs. Reads
  docs/requirements.md and docs/design.md, then produces a fresh
  docs/tasks.md. No interview needed — tasks are derived from specs.
  Use when requirements or design changed and tasks need updating.
---

# Revise tasks

## Process

1. Read `docs/requirements.md` and `docs/design.md`. If either
   doesn't exist, tell the user to run /project-onboard first.

2. Tell the user: "I'll regenerate your task breakdown based on
   the current requirements and design. This will replace the
   existing tasks.md."

3. Follow the same task breakdown logic as the pipeline:
   - Group into 3-5 testable phases
   - Each task: clear action, file affected, acceptance criterion
   - Order by dependency
   - Flag risky tasks
   - Estimate session count per phase

4. Show the proposed tasks to the user before saving.
   Ask: "Does this build order make sense?"

5. Save to `docs/tasks.md`.

## Rules

- Overwrite docs/tasks.md ONLY — nothing else
- No interview needed — this is pure derivation from specs
- But DO show the result and ask for feedback before saving
- If requirements and design contradict each other, flag it
  and ask the user to resolve before generating tasks
