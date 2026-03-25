# [project name] — design

Designed against: @docs/requirements.md

## Architecture (confidence: ___)

### Approach
[What architecture pattern and why. Reference the delivery format
and user journey from requirements.]

### Tradeoffs
[What this approach gives up. What alternatives were considered.]

## Data model (confidence: ___)

### Core entities
[List each data object with its fields and types.
Note which fields are required vs optional.]

### Data flow
[Where data comes from → how it's processed → where it goes.
Include persistence strategy if any.]

## Interfaces (confidence: ___)

### User-facing interface
[CLI flags, web routes, chat commands — whatever the user sees.]

### External dependencies
[APIs, services, databases. Include error handling strategy for each.]

### Internal communication
[How components talk to each other, if applicable.]

## Tech stack (confidence: ___)

- Language/runtime: [choice + why]
- Framework: [choice + why, or "none — too simple to need one"]
- Key dependencies: [list with purpose of each]
- Dev tools: [build, test, lint if relevant]

## Risks (confidence: ___)

### Technical risks
[The hardest parts. What could go wrong. Ordered by severity.]

### Mitigation
[For each risk: what's the fallback plan?]

### If time runs out
[Which feature gets cut first? Reference the priorities from requirements.]

## Contradictions with requirements

[List any design decisions that differ from or aren't covered by
the requirements. Each needs a resolution before implementation.]

- None found / [Specific contradiction + recommended resolution]
