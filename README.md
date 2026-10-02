# Wondering Aloud

An extension of the [Thinking Out Loud](https://github.com/Shubhamsaboo/awesome-llm-apps/tree/main/agent_skills/thinking-out-loud) agent skill.

## What changed

The original Echo workflow is preserved:

Ramble → Echo → approval → original agent response.

Wondering Aloud adds one optional path after the Echo is approved:

1. Generate the **Original Response** using the approved Echo.
2. Take only the uncertainties already identified in **Open** and **My additions**.
3. Ask targeted questions, using explicit choices where appropriate.
4. Use the user's answers to generate a **Clarified Response**.
5. Show both responses without replacing the original.

The extension does not introduce a separate independent intent-analysis system.

## Installation

If you are using the Vercel Skills CLI, install the local skill from this
directory into your agent's project skills location.

For the user's current Windows installation, the existing skill is under:

`%USERPROFILE%\.agents\skills\thinking-out-loud`

Back up that folder first, then replace its `SKILL.md`, `README.md`, and
`references\echo-format.md` with the files in this project.

The skill should remain project-scoped, matching the installation shown by
the Skills CLI.

## Usage

Trigger it with a long stream-of-consciousness request or an explicit
"let me think out loud" style request.

After the Echo is approved, the original response remains the normal path.
The clarified path is used when a comparison is wanted.

## Attribution

Original concept and source:
Shubham Saboo / awesome-llm-apps, Apache-2.0.

This version preserves the original Thinking Out Loud workflow and adds
the optional Original Response / Clarified Response comparison.
