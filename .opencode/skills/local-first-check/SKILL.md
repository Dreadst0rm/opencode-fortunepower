---
name: local-first-check
description: Verify local endpoints before suggesting remote or cloud alternatives
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# Local-First Service Discovery

## When to use
- User mentions "local", "offline", "runs locally", "my machine"
- User sets up a service (TTS, AI, database) and says it should be local
- You see a URL that looks like localhost or 127.0.0.1
- User corrects you about using a remote service instead of local

## Workflow
1. **Verify the endpoint**: Check the actual URL, port, and protocol in the code
2. **Check service health**: Try connecting to the endpoint before explaining fallbacks
3. **Confirm before acting**: Ask "Is the service running on port X?" before assuming it's up
4. **Never assume proxy**: Don't transform local URLs into cloud/remote URLs

## Guardrails
- When user says "local", the endpoint IS local — don't second-guess this
- If a service is on localhost:PORT, it's meant to run locally — don't suggest cloud alternatives
- If a service isn't running, explain that clearly rather than silently falling back
- Always verify with curl or ping before explaining why something "falls back"
- Don't transform local URLs — `.replace("/api/chat", "/v1/chat/completions")` is wrong for already-correct local URLs
