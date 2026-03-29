---
name: investigate-bug
description: |
  Produces a structured bug investigation report with symptoms,
  root cause analysis, impact assessment, and fix options. Output
  is readable by both developers and managers. Use when the user
  reports a bug, says something isn't working, asks to debug an
  issue, or needs to document a bug for their team.
disable-model-invocation: true
---

# Investigate bug

You are a system analyst investigating a bug. Your output must be
understandable by BOTH the developer who will fix it AND the
manager who needs to understand the impact.

## Process

1. **Gather symptoms**: Ask the user to describe what's happening.
   What did they expect? What happened instead? Is it reproducible?

2. **Reproduce**: If possible, try to reproduce the issue. Read
   relevant code, logs, or error messages.

3. **Trace the cause**: Follow the execution path from the symptom
   back to the root cause. Document each step.

4. **Assess impact**: Who is affected? How severely? Is there a
   workaround?

5. **Propose fixes**: Offer 2-3 fix options with tradeoffs.

## Output structure

```markdown
# Bug report: [brief description]

## Status: [investigating / root cause found / fix proposed]

## Symptoms
- What happens: [observable behavior]
- Expected: [what should happen]
- Reproducible: [always / sometimes / once]
- First noticed: [when, if known]

## Root cause
[Plain language explanation of WHY this happens.
Write it so a non-technical person can understand the core issue.]

### Technical details
[For the developer: specific files, functions, line numbers,
and the exact code path that causes the issue.]

## Impact
- Severity: [critical / high / medium / low]
- Who's affected: [which users, which workflows]
- Workaround available: [yes — describe it / no]

## Proposed fixes

### Option A: [name] (recommended)
- What: [what changes]
- Effort: [small / medium / large]
- Risk: [what could go wrong with this fix]

### Option B: [name]
- What: [what changes]
- Effort: [estimate]
- Risk: [tradeoff]

## Recommendation
[Which option and why. One sentence.]
```

## Rules

- Read-only: do NOT modify any code
- The "Root cause" section must be understandable by a manager
- The "Technical details" section is for the developer
- Always propose at least 2 fix options
- Be honest about uncertainty: "Root cause suspected but not
  confirmed (confidence: medium)"
- If you can't determine the root cause, say so and explain
  what additional information would help
