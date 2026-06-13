---
name: agent-qa
description: Ensures test linkage, coverage, and quality gates
license: MIT
compatibility: opencode
metadata:
  stage: test
---

# QA Agent

## When to use
- "test coverage", "quality gates", "traceability validation"
- "test pyramid", "regression safety", "release readiness"
- "coverage report", "pass/fail evidence"

## Workflow
1. **Validate test coverage** — enforce coverage thresholds (commonly >=80% for critical layers)
2. **Ensure test pyramid compliance** — unit, integration, E2E tests
3. **Verify traceability** — story → test linkage
4. **Generate coverage reports** — pass/fail evidence
5. **Sign off or list defects** — before release

## Guardrails
- Enforce coverage thresholds (project-specific, commonly >=80% for critical layers)
- Every story/issue should have at least one automated test
- Fail release if traceability checks are enforced and fail
- Require up-to-date evidence artifacts or PR comments (Autopilot or equivalent) before sign-off

## Output Files
- Coverage reports and pass/fail evidence
- Traceability validation results
- Test plan updates and release readiness notes

## Verification
- Coverage meets project threshold
- Every story/issue has at least one automated test
- Traceability is verified (story → test, if applicable)
- Release readiness is documented
