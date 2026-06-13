---
name: ship
description: Run the full pre-deployment pipeline — lint, typecheck, build, test, tag, and deploy
license: MIT
compatibility: opencode
metadata:
  stage: deploy
---

# Ship

## When to use
- "deploy", "release", "publish", "ship it"
- "tag release", "cut release", "bump version"
- Before merging to main/release branch

## Workflow
1. **Lint** — run the project's linter (ESLint, ruff, golangci-lint, clippy) and fix any issues
2. **Typecheck** — run the type checker (TypeScript, mypy, Pyright, Go compiler) and fix type errors
3. **Build** — produce the production artifact (compiled output, bundle, Docker image, binary)
4. **Run full test suite** — all tests must pass
5. **Bump version** — follow semver; update version in the project's source of truth (`package.json`, `Cargo.toml`, `pyproject.toml`)
6. **Tag** — create a git tag matching the new version
7. **Deploy/publish** — push to the target environment or package registry

## Version bump rules
- **Major (breaking change)**: incompatible API changes
- **Minor (feature)**: backward-compatible new functionality
- **Patch (fix)**: backward-compatible bug fixes

## Quality Gates

### Coverage Gate
- Enforce minimum coverage threshold (default: 80% for critical layers)
- Fail build if coverage drops below threshold
- Report coverage delta (before/after)

### Traceability Gate (optional)
- If the project uses story tracking, verify story → test linkage exists
- If the project requires evidence artifacts, verify they are present on PR
- Fail build if traceability checks are enforced and fail

### Security Gate
- Run dependency vulnerability scan (OWASP, npm audit, pip audit)
- Verify no secrets in code (gitleaks, trufflehog, or equivalent)
- Fail build if critical/high vulnerabilities found

### Validation Gate
- Run project validation scripts (if available)
- Verify documentation is up to date
- Verify API docs match current implementation

## Pre-flight checklist
- [ ] Linter passes with no errors
- [ ] Typechecker passes with no errors
- [ ] Build succeeds
- [ ] All tests pass
- [ ] Coverage meets threshold (>=80% for critical layers)
- [ ] No critical/high security vulnerabilities
- [ ] Story → test traceability verified (if project uses story tracking)
- [ ] Version is bumped correctly (semver)
- [ ] Changelog is updated (if applicable)
- [ ] Git tag is created
- [ ] Deployment target is correct (not prod on a Friday afternoon)

## Verification
- The build artifact is produced at the expected location
- The version tag exists in git
- The deployment succeeded (health check passes)
- Rollback plan exists if needed
- All quality gates passed (coverage, traceability if applicable, security, validation)
