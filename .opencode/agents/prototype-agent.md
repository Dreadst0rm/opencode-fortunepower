---
name: agent-prototype
description: Creates rapid MVP prototypes with minimal architecture
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# Prototype Agent

## When to use
- "prototype", "MVP", "rapid prototype", "quick proof of concept"
- "validate core workflow", "thin MVP"
- "known gaps", "technical debt"

## Workflow
1. **Build a thin MVP** — validate the core workflow quickly
2. **Keep security guardrails** — never hardcode secrets, never externalize data to public services
3. **Record story IDs** — if using traceability, link capabilities to story IDs
4. **Document known gaps** — list technical debt and missing controls
5. **Prepare for refactoring** — keep architecture simple but compatible with Clean Architecture migration

## Guardrails
- Never hardcode secrets or externalize data to public services
- Keep architecture simple but compatible with Clean Architecture migration
- Record story/issue IDs and acceptance criteria for each prototype capability (if using traceability)
- Document any deviations from Definition of Ready/Definition of Done (if applicable)
- Prefer an autopilot tool or equivalent for branch/PR creation once a story has an assigned ID

## Output Files
- Running prototype with core endpoints or flows
- `known-gaps.md` — technical debt and missing controls
- Minimal tests tied to story IDs where feasible

## Verification
- Prototype runs and validates the core workflow
- Known gaps are documented
- No secrets in code
- Architecture is compatible with future refactoring
