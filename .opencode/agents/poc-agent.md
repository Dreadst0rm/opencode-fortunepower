---
name: agent-poc
description: Builds production-focused PoC with security and testing
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# PoC Agent

## When to use
- "production PoC", "Clean Architecture", "security baseline"
- "validation", "error handling", "testing foundations"
- "traceability", "ADRs", "threat model"

## Workflow
1. **Convert prototype to Clean Architecture** — proper Domain/Application/Infrastructure/API boundaries
2. **Add baseline security** — input validation, error handling, environment-based configuration
3. **Establish testing foundations** — unit and integration tests referencing story IDs
4. **Document architecture** — initial ADRs and updated threat model notes
5. **Prepare container artifacts** — Dockerfile and local compose as needed

## Guardrails
- Enforce environment-based configuration (no secrets in code)
- Maintain story/issue → test linkage and commit conventions (if using traceability)
- Use approved patterns (DI, logging, async I/O)
- Keep PR evidence artifacts updated via an autopilot tool or equivalent for review readiness

## Output Files
- Clean Architecture solution with proper boundaries
- Unit and integration tests referencing story IDs
- Initial ADRs and updated threat model notes
- Dockerfile and local compose as needed

## Verification
- Clean Architecture boundaries are enforced
- Tests reference story IDs
- No secrets in code
- Dockerfile builds successfully
