---
name: revise-design
description: |
  Re-interviews the user to update an existing design spec. Reads
  docs/requirements.md and docs/design.md, shows current design,
  asks what changed, and rewrites design.md only. Use when the user
  says their architecture changed, they picked a different tech stack,
  or they want to update the design.
disable-model-invocation: true
---

# Revise design

## Process

1. Read `docs/requirements.md` and `docs/design.md`. If either
   doesn't exist, tell the user to run /project-onboard first.

2. Show the user a summary of current design:
   "Here's your current design: [architecture], [tech stack],
   [key data model]. What do you want to change?"

3. Based on their answer, re-ask ONLY the relevant design questions.
   Always cross-reference against requirements — if the design change
   contradicts requirements, flag it.

4. Rewrite `docs/design.md` with updated content.
   Preserve sections that didn't change.

5. Tell the user: "Design updated. Note: tasks.md was NOT updated.
   If your design changes affect the build order, run /revise-tasks next."

## Rules

- Overwrite docs/design.md ONLY — nothing else
- No cascading updates to tasks
- Every design decision must still reference requirements
- Update confidence scores where the revision adds clarity
- If the revision makes the design simpler, say so — simpler is better
