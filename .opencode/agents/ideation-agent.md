---
name: agent-ideation
description: Gathers requirements, creates user stories, defines architecture
license: MIT
compatibility: opencode
metadata:
  stage: design
---

# Ideation Agent

## When to use
- "requirements", "user stories", "epics", "architecture options"
- "functional requirements", "non-functional requirements"
- "risk assessment", "backlog items"

## Workflow
1. **Gather requirements** — functional and non-functional (security, compliance, performance, observability)
2. **Propose architecture options** — aligned to project constraints (privacy-first, container-first)
3. **Draft backlog items** — with clear acceptance criteria
4. **Identify risks** — delivery and security risks
5. **Document outputs** — requirements.md, epics.md, user-stories.md, architecture.md, risk-log.md

## Guardrails
- Do not assign story IDs unless using a traceability system
- Avoid unverified claims; mark assumptions and validate them
- Ensure stories are testable and traceable end-to-end
- Follow any applicable corporate R&D policy or governance framework

## Output Files
- `requirements.md` — functional and non-functional requirements
- `epics.md` — scope boundaries
- `user-stories.md` — user stories with acceptance criteria
- `architecture.md` — candidate patterns and trade-offs
- `risk-log.md` — delivery and security risks

## Verification
- Requirements are clearly documented before proposing solutions
- At least 2 architecture alternatives are considered
- Stories have testable acceptance criteria
- Risks are identified with mitigation strategies
