---
name: architect
description: Guide architecture decisions, explore tradeoffs, and document design decisions
license: MIT
compatibility: opencode
metadata:
  stage: design
---

# Architect

## When to use
- "architecture", "design decision", "how should I structure this"
- "tradeoffs", "compare approaches"
- "ADR", "architecture decision record"
- Planning a new feature, module, or service

## Workflow
1. **Define requirements** — functional and non-functional (performance, scalability, maintainability, security)
2. **Explore options** — list 2-4 viable approaches with pros/cons
3. **Evaluate tradeoffs** by these dimensions:
   - Complexity: learning curve, implementation effort
   - Scalability: horizontal scaling, data growth
   - Maintainability: readability, testability, evolvability
   - Performance: latency, throughput, resource usage
   - Security: attack surface, data protection
4. **Recommend** — clearly state the preferred approach and why
5. **Write ADR** if the decision is significant (template below)

## ADR template
```markdown
# ADR-<NNN>: <Title>

## Status
Proposed | Accepted | Deprecated | Superseded

## Context
What is the problem and why does it need a decision?

## Decision
What was chosen and why?

## Consequences
What tradeoffs were accepted?

## Alternatives Considered
Other options and why they were rejected.
```

## Anti-patterns
- Over-engineering for hypothetical future needs (YAGNI)
- Choosing familiar tech without evaluating fit
- Ignoring operational complexity (deployment, monitoring, debugging)
- Making architecture decisions in the middle of feature implementation

## Verification
- Requirements are clearly documented before proposing a solution
- At least 2 alternatives are considered
- The decision is documented (ADR or equivalent)
- Tradeoffs are explicitly stated, not glossed over
