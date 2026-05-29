---
name: test
description: Write, update, and run tests; enforce coverage and quality thresholds
license: MIT
compatibility: opencode
metadata:
  stage: test
---

# Test

## When to use
- "write tests", "add test coverage", "run tests"
- "tdd", "test-driven", "spec"
- "test is failing", "fix test"
- Before committing any new or modified code

## Workflow
1. **Identify test framework** from config files (`jest.config.*`, `pytest.ini`, `Cargo.toml` dev-dependencies, `go.mod` test patterns)
2. **Understand existing patterns** — read a neighboring test file to match style
3. **Write/update tests**:
   - Cover the happy path first, then edge cases, then error paths
   - Match existing project conventions (describe/it, test/assert, etc.)
4. **Run the test suite** — full suite, not just the new test
5. **Report failures** — if any test fails, load the `debug` skill

## Language-specific notes
- **JavaScript/TypeScript**: Jest, Vitest, Mocha; use `--coverage`
- **Python**: pytest; use `pytest -v --tb=short`
- **Rust**: `cargo test`; use `#[cfg(test)]` modules
- **Go**: `go test ./... -v -race`

## Verification
- All tests pass
- New code has test coverage
- Existing tests are not broken
- No flaky tests introduced (deterministic, no sleeps/timers)
