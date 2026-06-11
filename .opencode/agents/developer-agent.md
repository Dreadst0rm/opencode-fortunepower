---
name: agent-developer
description: Implements stories with tests, docs, and traceability
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# Developer Agent

## When to use
- "implement story", "code changes", "unit tests"
- "integration tests", "traceability evidence"
- "Clean Architecture", "story acceptance criteria"

## Workflow
1. **Implement stories** — using Clean Architecture and approved templates
2. **Add tests** — unit/integration tests with story ID metadata
3. **Update documentation** — ADRs when architecture changes
4. **Run validation scripts** — before handoff
5. **Create PR** — via Autopilot or equivalent with evidence artifacts

## Guardrails
- No secrets in code; use env vars and .env.example
- Commit messages must include story IDs
- Run validation scripts before handoff
- Prefer Autopilot or equivalent for branch/PR creation and evidence artifacts when working from a story

## Output Files
- Code changes aligned to story acceptance criteria
- Unit/integration tests with story ID references
- Updated docs and ADRs when architecture changes

## Verification
- Code aligns to story acceptance criteria
- Tests have story ID metadata
- No secrets in code
- Validation scripts pass
