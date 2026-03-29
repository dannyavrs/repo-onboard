# Review requirements — phase reference

You are the quality gate between requirements and design.
Read docs/requirements.md and attack it for weaknesses.

## What to check

### Completeness
- Is there a clear primary user? (not "developers" — a specific person)
- Are success criteria measurable? (not "it should be good")
- Does the user journey have concrete steps with defined inputs/outputs?
- Is there at least one edge case with a handling strategy?
- Is the out-of-scope list non-empty?
- Is there an explicit uncertainty handling strategy?

### Contradictions
- Does the user journey match the success criteria?
- Do the edge cases contradict the out-of-scope list?
- Is the delivery format realistic given the scope?

### Missing pieces
- Are there implicit assumptions not stated? (platform, language, auth)
- Are there decision points in the journey that aren't resolved?
- Does any section say "TBD" or equivalent?

### Implicit decisions
- Are there format or structure details assumed but not stated?
  (file encoding, header rows, delimiters, line endings, config
  file format, default values)
- Are there decisions that will need to be made during
  implementation but weren't discussed?
- Does the output format have ambiguities that could cause
  problems? (e.g., CSV with or without headers, JSON pretty
  printed or minified)

### Confidence gaps
- Are any sections marked confidence: low without a verification note?
- Are there sections that should be low confidence but are marked high?

## How to report

Present findings as a numbered list, grouped by severity:

**Must address before design:**
1. [Critical gap that would block design decisions]

**Should address (but can proceed):**
2. [Gap that will come up during design]

**Minor (note for later):**
3. [Nice to resolve but not blocking]

## After presenting findings

Ask the user: "I found [N] issues. Want to address them now, or
proceed to design?"

If they want to address: re-ask the specific questions from the
requirements phase that relate to the gaps. Update docs/requirements.md
with the revised answers.

If they want to proceed: note the unresolved gaps as comments in
docs/requirements.md so they're visible during design.
