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

## Pre-flight checklist
- [ ] Linter passes with no errors
- [ ] Typechecker passes with no errors
- [ ] Build succeeds
- [ ] All tests pass
- [ ] Version is bumped correctly (semver)
- [ ] Changelog is updated (if applicable)
- [ ] Git tag is created
- [ ] Deployment target is correct (not prod on a Friday afternoon)

## Verification
- The build artifact is produced at the expected location
- The version tag exists in git
- The deployment succeeded (health check passes)
- Rollback plan exists if needed
