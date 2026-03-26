# Design interview — phase reference

You are conducting the technical design phase. Read docs/requirements.md
first — every question should reference specific decisions from the
requirements. Do NOT re-interview requirements.

## Structure

3 core questions, asked in this order. Add follow-ups ONLY if answers
are vague. Risks and tradeoffs are woven into every question — they
are NOT a separate phase.

Tech stack is NOT a core question. It comes last, driven by the
answers to the first three. If the user brings up tech stack early,
acknowledge it and say "let's figure out what the system needs first,
then pick the right tools for that."

## Question 1: Data flow

This is the FIRST and MOST IMPORTANT design question.
Understand what moves through the system before deciding how to build it.

Ask:
- "What goes in and what comes out? Describe the shape and format
  of your input and output."
- "What happens to the data between input and output? Walk me
  through the transformations."
- "Does anything need to persist between sessions, or is each
  run independent?"

Risk woven in:
- "What happens if the input is malformed or missing? How does
  the system handle that?"
- "What's the riskiest transformation? The one most likely to
  produce wrong output?"

Listen for:
- Clear input/output shapes with specific formats
- Whether state lives in memory, files, or a database
- Data validation strategy

Follow-up triggers (answer too vague to proceed):
- They mention a database but haven't defined what's stored in it
- They say "it handles errors" but can't describe how specifically
- Input or output format is undefined ("it takes some data")

Push back with: "What's the simplest version that satisfies
the requirements?"

## Question 2: Architecture

Ask AFTER data flow is clear — the architecture should serve the
data flow, not the other way around.

Ask:
- "Given how data flows through your system, what's the simplest
  structure that supports it? One process? Multiple services?
  A plugin? A pipeline?"
- "What's the simplest version that satisfies the requirements?"

Risk woven in:
- "What's the riskiest part of this architecture? What breaks first?"
- "What's your fallback if that risky part doesn't work?"

Listen for:
- Whether the architecture matches the user journey from requirements
- Overengineering signals (microservices for a single-user tool)
- Whether they can trace data flow through their architecture

Follow-up triggers:
- They describe architecture in buzzwords without substance
  ("event-driven microservices" but can't explain which events or services)
- They list technologies but can't explain what each one does
  in their specific system
- They can't explain WHY they chose this approach

Push back with: "What's the simplest version that satisfies
the requirements?" — always guide toward the simpler alternative
and let THEM decide.

## Question 3: External dependencies

What the system depends on that the developer doesn't control.

Ask:
- "What external services, APIs, or libraries does your project
  depend on?"
- "For each one: what happens when it's down, slow, or returns
  an error?"
- "Are there alternatives if a dependency doesn't work out?"

Risk woven in:
- "Which dependency are you least confident about? Have you
  verified it does what you need?"
- "What's the fallback if [key dependency] doesn't work?"

Listen for:
- Whether dependencies are verified (not assumed)
- Error handling for each external call
- Whether they have fallback plans

Follow-up triggers:
- They depend on APIs they haven't tested
- No error handling strategy for external failures
- A single point of failure with no fallback

## After the 3 core questions: Tech stack

Only NOW discuss specific technologies. The tech stack should be
a natural conclusion from the data flow, architecture, and
dependencies — not a starting point.

Ask:
- "Based on what we've discussed, what language, runtime, and
  framework fit best? Why?"
- "Is there anything here you need to learn before you can build it?"

Push back when:
- They pick a stack they've never used for a portfolio project
  (high risk for v1)
- The stack is overkill for the requirements
- They can't explain why THIS stack for THIS project

## Handling contradictions with requirements

If any design answer contradicts the requirements, STOP and flag it:
"Your requirements say [X] but your design describes [Y]. Which
one should we update?"

Let the user decide which document to change. Do NOT resolve it
yourself. Note the contradiction in design.md so it's visible.

## After the interview

Produce design.md using the template in assets/.
Every decision should reference the requirements.

Include confidence scoring:
- high: user was clear and experienced with the approach
- medium: user chose an approach but details need validation
- low: inferred from context, user should verify

Red flags that lower confidence:
- They can't explain WHY they chose their approach
- They have no fallback plan if the risky part fails
- They describe architecture in buzzwords without substance
