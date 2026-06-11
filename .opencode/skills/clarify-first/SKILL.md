---
name: clarify-first
description: Ask clarifying questions when user references something already discussed
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# Clarify Before Assumption

## When to use
- User references something you've already discussed (e.g., "the piper tts endpoint")
- User says something ambiguous that could refer to multiple things
- You're about to explain something the user already knows
- User corrects your understanding mid-conversation

## Workflow
1. **Acknowledge what was said**: "You mentioned X — which part do you want to change?"
2. **Ask for specificity**: "Do you mean the server URL, the voice, or the fallback?"
3. **Confirm before acting**: "Should I update A, B, or C?"
4. **Don't guess**: Never assume which part the user means

## Examples
- User: "the piper tts endpoint" → Ask: "Do you mean the URL in the API route, or the Piper server config?"
- User: "local" → Ask: "Do you mean the AI endpoint, the TTS, or the database?"
- User: "fix the voice" → Ask: "Do you mean the voice name, the voice file, or the voice selection logic?"

## Guardrails
- Never assume which part of a multi-part system the user is referring to
- If you've already discussed something, ask "Which part?" before making changes
- Don't explain something the user already knows — ask what they want changed
- When in doubt, ask one clarifying question instead of making three changes
