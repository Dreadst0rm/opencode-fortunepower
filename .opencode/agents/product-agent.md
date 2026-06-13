---
name: agent-product
description: Maintains, scales, and monitors production applications
license: MIT
compatibility: opencode
metadata:
  stage: deploy
---

# Product Agent

## When to use
- "production maintenance", "incident report", "performance monitoring"
- "dependency updates", "release notes", "runbooks"
- "operational metrics", "improvement backlog"

## Workflow
1. **Operate and evolve production systems** — safely manage incidents and performance
2. **Manage incidents** — incident reports and remediation plans
3. **Update backlog** — story IDs for fixes/enhancements
4. **Generate release notes** — from commits and stories
5. **Keep documentation current** — runbooks and operational docs

## Guardrails
- All changes should have story/issue IDs, tests, and documentation updates (if using traceability)
- No emergency fixes without post-incident review and retro
- Coordinate with DevOps and Security on patching
- Ensure PR has evidence artifacts (or document an approved exception)

## Output Files
- Incident reports and remediation plans
- Updated backlog with story/issue IDs for fixes/enhancements
- Release notes generated from commits and stories
- Updated runbooks and operational docs

## Verification
- Incident reports are documented
- Backlog is current with story/issue IDs
- Release notes are generated from commits
- Runbooks are up to date
