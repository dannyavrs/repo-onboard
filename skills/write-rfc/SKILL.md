---
name: write-rfc
description: |
  Produces a technical decision document (RFC) that captures what
  was decided, what alternatives were considered, and why. Use when
  the user makes an architecture decision, chooses between approaches,
  needs to document a tradeoff, or says "we need to decide between
  X and Y."
disable-model-invocation: true
---

# Write RFC

You are documenting a technical decision. An RFC (Request for Comments)
captures the decision, the context, the alternatives, and the reasoning
so that future developers understand WHY things are the way they are.

## Process

1. Ask the user: "What decision do you need to document?"
   If they've already described it, proceed.

2. Ask: "What alternatives did you consider? Why did you reject them?"

3. Ask: "What are the risks of the chosen approach?"

4. Produce the RFC using the structure below.

## Output structure

```markdown
# RFC: [decision title]

- **Status**: proposed / accepted / superseded
- **Date**: [today]
- **Author**: [user's name if known]

## Context
[Why this decision needs to be made. What problem or opportunity
triggered it. 2-3 sentences.]

## Decision
[What was decided. Be specific — name the technology, pattern,
or approach. One paragraph.]

## Alternatives considered

### [Alternative A]
- Description: [what it is]
- Pros: [why it was attractive]
- Cons: [why it was rejected]

### [Alternative B]
- Description: [what it is]
- Pros: [why it was attractive]
- Cons: [why it was rejected]

## Consequences

### Positive
[What this decision enables. What gets easier.]

### Negative
[What this decision makes harder. What tradeoffs were accepted.]

### Risks
[What could go wrong. What would trigger revisiting this decision.]

## References
[Links to relevant docs, specs, or discussions. If none, omit.]
```

## Rules

- Read-only: do NOT modify any code
- Be specific: "We chose PostgreSQL over MongoDB because our data
  is relational" — not "we picked a database"
- Always include at least 2 alternatives (even if one is "do nothing")
- The Consequences section must include BOTH positive AND negative
- If the user can't articulate why they rejected alternatives,
  push back — "you must have had a reason, what was it?"
- Save the RFC where the user specifies, or suggest `docs/rfcs/`
