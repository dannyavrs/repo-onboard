# repo-onboard — requirements (final)

## Problem statement

Developers with a new idea jump straight into coding without
thinking through requirements, architecture, or scope. This
leads to spaghetti code, abandoned projects, and wasted time.
AI coding tools like Claude Code work best when they have
structured context — but most developers don't know how to
create that context before they start.

## Primary user

A developer with a project idea and no code yet. They want to
go from "I have an idea" to "I have a structured foundation
ready for Claude Code" — requirements, design, tasks, and
a best-practice CLAUDE.md — without knowing how to write
specs themselves.

## Success criteria

1. A developer who has never written a spec can run this tool
   and produce professional-grade requirements, design, and
   task documents through a guided interview process.

2. The generated CLAUDE.md follows best practices and gives
   Claude Code everything it needs to assist effectively
   from the first session.

3. When the tool is uncertain about something or the user's
   answers are vague, it pushes back and asks for specifics
   rather than guessing.

## User journey

### Step 1: Init
The developer runs:
```
npx repo-onboard new
```
No repo needed. No GitHub URL. Just an idea.

### Step 2: Guided interview
The tool walks them through a structured interview:
- Phase 1: Who and why (primary user, problem, motivation)
- Phase 2: Success criteria (what "good" looks like)
- Phase 3: User journey (step-by-step experience)
- Phase 4: Edge cases + uncertainty handling
- Phase 5: Out of scope

Between phases, a review step checks for gaps and
contradictions before proceeding.

The tool then interviews for technical design:
- Architecture approach and tradeoffs
- Key data structures / contracts
- API or interface design
- Risks and mitigations

Finally it breaks the design into phased, ordered tasks.

### Step 3: Output
The tool generates a project directory:
```
my-project/
├── docs/
│   ├── requirements.md
│   ├── design.md
│   └── tasks.md
├── .claude/
│   ├── CLAUDE.md
│   └── skills/
│       ├── explore-system/
│       ├── investigate-bug/
│       ├── stakeholder-brief/
│       └── write-rfc/
└── README.md
```

The developer opens the directory in Claude Code and starts
building with full context from day one.

## Edge cases handled in v1

- **Vague answers**: The tool pushes back. "All of the above"
  gets challenged with "if you could only pick one, which?"
  It does not proceed with ambiguous input.

- **Scope creep during interview**: Each phase has explicit
  boundaries. The tool redirects if the user starts describing
  implementation details during the requirements phase.

## Uncertainty handling

The tool flags its own uncertainty in generated documents.
When it cannot determine something from the interview
(e.g., the right architecture pattern), it marks it:

```
**Architecture**: Event-driven suggested
(confidence: medium — user described async workflows but
didn't specify message broker preference. Verify before
implementation.)
```

## Out of scope for v1

- Analyzing existing repositories
- Generating actual code or tests
- Web UI or dashboard
- Private/enterprise repo support
- Integration with project management tools
- Auto-updating docs when code changes

## Delivery format

CLI tool published to npm.
Usage: `npx repo-onboard new`

Also installable as a Claude Code plugin for users who
want the supporting skills without the CLI pipeline.
