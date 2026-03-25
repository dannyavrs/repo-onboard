# Task breakdown — phase reference

You are generating a phased task list. Read both docs/requirements.md
and docs/design.md first. This phase does NOT require a user interview —
tasks are derived from the specs.

## How to break down tasks

### Step 1: Identify phases

Group work into 3-5 phases. Each phase should produce something
testable. The user should be able to stop after any phase and
have a working (if incomplete) project.

Typical phasing:
- Phase 1: Foundation (project setup, core data model, basic I/O)
- Phase 2: Core feature (the main thing the tool does)
- Phase 3: Edge cases + error handling
- Phase 4: Polish (UX, documentation, packaging)

### Step 2: Break each phase into tasks

Each task must have:
- A clear action ("Create", "Implement", "Add", "Write")
- What file or component it affects
- An acceptance criterion (how to know it's done)
- Estimated complexity: small / medium / large

### Step 3: Order by dependency

Within each phase, tasks are ordered so each builds on the previous.
If task B depends on task A, A comes first. No circular dependencies.

### Step 4: Flag the risky tasks

Mark any task that involves:
- Technology the user hasn't used before
- External API integration
- The riskiest technical part identified in design
- Complex business logic

These should be tackled early in the phase, not saved for last.

## Rules

- Tasks should be completable in one Claude Code session (~30-60 min)
- If a task is "large", it should be split
- Never combine unrelated work in one task
- Each task should be independently testable
- The first task in Phase 1 should result in a runnable (even if empty) project
- Include a "Verify" step at the end of each phase

## Show the user before saving

Present the task breakdown and ask:
"Here's the proposed build order. Does this sequence make sense?
Anything you'd reorder or split differently?"

Incorporate their feedback, then save to docs/tasks.md.
