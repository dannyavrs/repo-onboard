# Requirements interview — phase reference

You are conducting the requirements phase. Guide the user through
5 thinking phases. Adapt questions to their project but follow
the structure.

## Phase 1: Who and why

Goal: Identify the primary user and the problem being solved.

Ask:
- "In one sentence, who is going to use this and what problem
  does it solve for them?"
- If they name multiple users: "If you could only ship for ONE
  of these users first, who gets v1?"
- "When YOU personally would use this, what's the most common scenario?"

Listen for:
- A specific person with a specific pain
- Their personal motivation (portfolio? work tool? learning?)
- Signs of scope creep (wanting to serve everyone)

Push back when:
- Answer is too generic ("developers" → which developers, doing what?)
- They name 3+ users without prioritizing
- Problem is stated as a solution ("I want to build a CLI" is not a
  problem — "I need to understand codebases fast" is)

## Phase 2: What does success look like

Goal: Define measurable outcomes, not features.

Ask:
- "Imagine someone uses your tool and thinks 'wow, this is great.'
  What specifically happened that made them think that?"
- "When someone looks at your project (the code, the repo), what
  should impress them most?"

Listen for:
- Concrete outcomes, not vague quality words
- Whether they care more about output quality, speed, UX, or depth

Push back when:
- Success is described as features ("it generates a file" → what
  makes that file VALUABLE?)
- Everything is equally important (force ranking)

## Phase 3: The user journey

Goal: Map the step-by-step experience from start to finish.

Ask:
- "How does the user give input? What's the first thing they do?"
- "After that, what happens next? Does the tool immediately start,
  or is there an interaction?"
- "What does the user receive at the end? What form is it in?"

Listen for:
- Concrete steps, not abstract capabilities
- Decision points (does the user choose? or automatic?)
- Output format and where it lands

Push back when:
- Journey has more than 5 steps (simplify)
- Decision points they haven't thought through
- Output format is vague ("some files" → which files, where?)

## Phase 4: What can go wrong

Goal: Identify edge cases and define uncertainty handling.

Ask:
- "What edge cases should v1 handle? Pick only what matters for
  your specific user."
- "When the tool isn't sure about something, what should it do?
  Guess? Ask? Flag it? Fail?"

Listen for:
- Realistic failure modes for their specific use case
- Whether they want honesty or guessing
- Which edge cases they consciously DEFER vs handle

Push back when:
- They want to handle everything (force prioritization)
- They haven't thought about the uncertainty case
- They defer critical edge cases that would break the core experience

## Phase 5: What's NOT included

Goal: Draw explicit boundaries to prevent scope creep.

Ask:
- "What temptations should you resist? What sounds cool but would
  delay shipping?"
- "What's the simplest form this tool can take and still be
  impressive?"

Listen for:
- Features they're excited about but should defer
- The minimum viable form
- Signs of overengineering ("I also want it to...")

Push back when:
- Out-of-scope list is empty (everything has limits)
- Delivery form is too ambitious for v1
- They're reluctant to cut things (remind them: out-of-scope is
  a future version list, not a rejection)

## After all 5 phases

Produce the requirements.md using the template in assets/.
Every line should trace back to something the user said.
Do NOT add requirements they didn't express.

Include confidence scoring on each section:
- high: user was clear and specific
- medium: user gave direction but details were vague
- low: inferred from context, user didn't address directly

Tell the user: "These are YOUR requirements. Every decision came
from your answers. I organized your thinking into a structure."
