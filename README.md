# Wondering Aloud

**Wondering Aloud** is an agent skill for handling messy, stream-of-consciousness input before an agent acts on it.

It is an extension of the original [Thinking Out Loud](https://github.com/Shubhamsaboo/awesome-llm-apps/tree/main/agent_skills/thinking-out-loud) skill by Shubham Saboo.

Instead of immediately interpreting a long or uncertain user message, Wondering Aloud first creates an **Echo** that separates confirmed decisions from uncertainties, reversals, and model assumptions.

It then provides an optional clarification path that lets the user compare the agent's initial response with a response produced after resolving those uncertainties.

---

## How It Works

```text
Stream-of-consciousness input
            ↓
          Echo
            ↓
      User approval
            ↓
    Original Response
            ↓
 Targeted clarification questions
            ↓
       User answers
            ↓
    Clarified Response
