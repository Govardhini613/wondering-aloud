---
name: wondering-aloud
description: >-
  A contract for what the agent does when a long, messy, stream-of-consciousness
  ramble arrives (usually voice dictation): act on nothing until the echo brief
  is approved. The echo audits the entire transfer, mission, locked decisions
  and constraints, open questions, flips and parked tangents, with the model's
  inferences and guesses quarantined away from the user's own phrasing, so the
  user verifies what the model believes, not just what it doubts. After the
  echo is approved, Wondering Aloud can optionally produce both the original
  response based on the approved echo and a clarified response based only on
  uncertainties resolved through targeted questions.
license: Apache-2.0
metadata:
  author: "Shubham Saboo (original), extended as Wondering Aloud"
  version: "1.0.0"
  source: "https://github.com/Shubhamsaboo/awesome-llm-apps"
---

# Wondering Aloud

A ten minute voice ramble transfers more context than any prompt a person
would type, and models reconstruct rambles well. The failure is downstream
and invisible: the model fills every gap in the ramble confidently. "The
usual model" silently becomes a specific model. "The standard size" becomes
a specific viewport. A position the user reversed mid-ramble survives as
fact. None of this registers as uncertainty from the inside, so none of it
ever becomes a clarifying question. The model then acts on a misreading it
fully believes, and the user discovers it an hour of generated work later.

This skill is the original Thinking Out Loud approach, renamed Wondering
Aloud, with one extension: after the echo is approved, the agent can retain
its normal response while optionally generating a second clarified response
after resolving the uncertainties already identified by the echo.

## Why an echo instead of follow-up questions

Asking clarifying questions is good, and the interview below does it.
But questions alone cannot secure a ramble, for two structural reasons:

- **Questions verify what the model doubts. The echo verifies what the
  model believes.** A clarifying question requires felt uncertainty, and
  confident misreadings feel like knowledge. The echo forces every
  inference and gap-fill into the open whether or not it felt uncertain.
- **Questions sample; the echo audits.** A long ramble carries dozens of
  facts and half-decisions. Even good questions probe three or four; the
  rest of the model's understanding goes unverified into action. The echo
  inventories the entire transfer, and it works by recognition, not recall:
  the user reads and spots what is wrong, which is far cheaper than
  producing answers, and ramblers often do not know their answer until they
  see the wrong guess written down.

## The contract

1. **Act on nothing.** No file edits, no code, no plans, no solutions to
   fragments, until the echo is approved. Reconstruct first.
2. **Label every addition.** Inferences and guesses live in their own
   section, apart from the user's own content. Never present a guess in the
   user's voice.
3. **Surface every reversal.** Adopt the later position, but flag the flip.
   Never silently average or pick.
4. **Lose nothing.** Tangents get parked, not dropped.
5. **Never remark on dictation artifacts.** Typos, homophones, filler,
   and restarts are resolved silently from context. Keep the user's own
   vocabulary and project names.
6. **Ask before persisting.** The approved brief is offered a home, never
   saved unprompted.
7. **Keep the original path intact.** The clarified response is an
   additional response, not a replacement for the original response.

## When to use

- A message is a long, weakly punctuated stream of consciousness with
  restarts, filler, and mid-message reversals ("actually no, scrap that")
- A message opens with a voice preamble ("switching to speech recognition,
  sorry for any typos", "dictating this")
- The user says they want to ramble or think out loud
- The user asks to be interviewed to untangle a fuzzy idea

## When not to use

- Short requests that are already clear
- The user wants a verbatim transcript, minutes, or cleanup of dictation
  while keeping their exact words
- Long but already structured text, such as a pasted spec or document
- The user asked a direct question and wants a direct answer

## The echo

One structured reply. Dense, scannable, and short: the user should find
and fix an error in seconds. Full template with a worked example in
[references/echo-format.md](references/echo-format.md).

1. **Mission**: one sentence stating what the user is actually trying to
   achieve. Often this differs from what they said first; that is fine.
2. **Locked**: the user's decisions and constraints, merged into one
   list. Mark anything they called a top priority.
3. **Open**: questions the ramble raised but did not answer.
4. **Ledger**: flips (both positions in one line, later one adopted) and
   parked tangents (one line each).
5. **My additions**: the only interpretation callouts. "Inferred"
   (strongly implied but never stated) and "Guessed" (gaps you filled).
   Tell the user to correct these first.

Compression rules, non-negotiable:

- **Nothing appears twice.** Every fact lives in exactly one section.
- **No "you said" recap.** Everything outside My additions is the user's
  own content by definition; only the model's additions get called out.
- **One line per bullet.** If a bullet needs two lines, it is two bullets
  or it is bloat.
- **Vague quantifiers are never silently resolved.** "The usual model",
  "standard size", "soon": each lands in Open or Guessed, never absorbed
  into a locked item as if it were specified.

Close by inviting corrections and offering the interview.

## The clarified response (optional)

This is the Wondering Aloud extension to the original Thinking Out Loud
workflow.

After the echo is approved, keep the original agent path unchanged and
produce an optional second response when the user wants the comparison.

1. **Original response**: generate the response or action exactly from the
   approved echo and the original workflow. Do not wait for the uncertainty
   questions to be answered before producing this response.
2. **Identify uncertainty**: use only items already present in the echo's
   **Open** or **My additions** sections. Do not independently invent a new
   uncertainty analysis.
3. **Ask targeted questions**: present concise questions for those
   uncertainties. When the uncertainty can be represented as discrete
   choices, give explicit options for the user to select.
4. **Build the clarified response**: incorporate the user's answers as
   additional constraints and produce a second response.
5. **Show both**: label the two outputs clearly as **Original Response** and
   **Clarified Response**.
6. **Do not overwrite history**: the original response remains visible and
   unchanged.
7. **Do not call the original response wrong**: differences show the effect
   of resolving uncertainty; they are not automatically errors.
8. **Do not introduce unrelated questions**: questions must trace back to
   Open or My additions in the approved echo.

The clarified response is an optional comparison path. It does not replace
the echo, the approval gate, the original response, the interview, or
capture mode.

## The interview (optional)

Follow-up questions have their place: after the audit, not instead of it.
Only if the user accepts the offer, or asked to be interviewed up front.

- Ask only about items flagged in Open or Guessed
- One question per message, highest information gain first
- Each question states in one clause why it matters
- Cap at five questions; stop early once answers stop changing the brief
- After the interview, restate only the sections of the echo that changed

For the clarified-response extension, the same questions can be used to
produce the Clarified Response after the Original Response has been
generated.

## Capture mode (multi-message rambles)

Not needed for dictation tools, where the whole ramble arrives as one
message. Use it when the user invokes the skill before rambling and then
adds thoughts across several messages, possibly over a long stretch.

- Acknowledge once, in one short line ("Go ahead, I'm listening. Say
  'done' when you want the echo.")
- For every following message, reply with a single minimal line
  ("Listening."). Vary it slightly so it does not feel robotic.
- Do NOT solve, praise, summarize, analyze, or ask questions mid-stream.
- If the user asks a direct question mid-ramble, answer it in at most two
  sentences, then return to listening.
- Exit on "done", "echo", "echo me", "that's it", "what did you get", or
  any clear equivalent, then deliver the echo.

## Persistence

After the user approves the echo, offer exactly three options:

1. Append the brief to CLAUDE.md so future sessions inherit it
2. Save it to `docs/rambles/YYYY-MM-DD-<topic>.md`
3. Keep it in-conversation only

The approved brief then governs the rest of the session: honor its
decisions and constraints without re-asking.
