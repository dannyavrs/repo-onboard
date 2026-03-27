---
name: revise-requirements
description: |
  Re-interviews the user to update an existing requirements spec.
  Reads the current docs/requirements.md, shows what exists, asks
  what changed, and rewrites that file only. Use when the user says
  their requirements changed, they want to update the spec, or they
  realized something is wrong with the requirements.
---

# Revise requirements

## Process

1. Read `docs/requirements.md`. If it doesn't exist, tell the user
   to run /project-onboard first.

2. Show the user a summary of current requirements:
   "Here's what your current requirements say: [brief summary of
   each section]. What do you want to change?"

3. Based on their answer, re-ask ONLY the relevant questions from
   the requirements interview phases. Do not re-interview from scratch
   unless they ask for it.

4. Rewrite `docs/requirements.md` with the updated content.
   Preserve sections that didn't change.

5. Tell the user: "Requirements updated. Note: design.md and tasks.md
   were NOT updated. If your changes affect the design, run
   /revise-design next."

## Rules

- Overwrite docs/requirements.md ONLY — nothing else
- No cascading updates to design or tasks
- Push back on vague changes just like the original interview
- Update confidence scores if the revision adds clarity
- If the change contradicts the existing design, flag it but
  do NOT modify design.md
