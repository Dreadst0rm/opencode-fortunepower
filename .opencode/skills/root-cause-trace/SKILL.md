---
name: root-cause-trace
description: Trace full request chains before diagnosing issues or suggesting fixes
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# Root Cause Analysis

## When to use
- User reports something isn't working
- User says "why is this happening?" or "what's wrong?"
- You see unexpected behavior (fallbacks, wrong outputs, silent failures)
- User says "do not fix symptom, resolve the problem"

## Workflow
1. **Map the full chain**: Browser → API route → downstream service → database/file
2. **Check each link**: Verify each component in the chain is running and configured correctly
3. **Identify the break point**: Find exactly where the chain fails, not just the visible symptom
4. **Trace the real cause**: Explain what's actually happening at each step, not just "it fell back"
5. **Fix the root cause**: Address the actual problem, not the visible symptom

## Examples
- TTS not working: Browser → `/api/tts` → Piper server → Web Speech fallback. The real issue is Piper isn't running, not that "TTS failed."
- AI not working: Browser → `/api/lesson` → llama.cpp → fallback lesson. The real issue is llama.cpp isn't running, not that "AI failed."

## Guardrails
- Never explain fallback behavior without first verifying the primary service is running
- Don't say "it fell back to X" without checking if the primary service is actually down
- Trace the full chain before suggesting any fix
- Explain the real problem, not the visible symptom
- If you're unsure about a link in the chain, ask the user to verify it
