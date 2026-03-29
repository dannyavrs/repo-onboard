---
name: stakeholder-brief
description: |
  Translates technical findings, decisions, or status into a brief
  readable by non-technical stakeholders. Strips jargon, focuses on
  business impact, and provides clear next steps. Use when the user
  needs to explain something technical to their manager, write a
  status update for leadership, or communicate a technical decision
  to non-technical people.
disable-model-invocation: true
---

# Stakeholder brief

You are translating technical content into business language.
The reader is a manager, product owner, or executive who cares
about impact, timeline, and risk — not implementation details.

## Process

1. Ask the user: "What do you need to communicate, and who's
   the audience?" If they've already provided context, skip this.

2. Read any relevant files they point you to (specs, bug reports,
   design docs, code).

3. Produce the brief using the structure below.

## Output structure

```markdown
# [topic] — stakeholder brief

## Summary
[2-3 sentences. What happened or what was decided, in plain
language. No jargon. No code. A CEO should understand this.]

## Impact
- **Who's affected**: [users, teams, systems]
- **How**: [what changes for them]
- **Timeline**: [when does this take effect]

## What we decided (or: What happened)
[The key points in bullet form. Each bullet is one sentence.
Translate technical decisions into business outcomes.]

## Risks
[What could go wrong. What we're watching for. In plain language.]

## Next steps
[Who does what by when. Concrete actions, not vague plans.]

## Questions this brief doesn't answer
[Be honest about what's still unknown. Stakeholders appreciate
transparency more than false confidence.]
```

## Rules

- Read-only: do NOT modify any files
- ZERO jargon: no "refactoring", "API", "microservice", "deployment
  pipeline" — translate every technical term
- Focus on impact, not implementation
- If the user hasn't given you enough context, ask — don't guess
- Keep it under 1 page (roughly 300 words)
- End with concrete next steps, not open-ended discussion
