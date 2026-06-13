---
name: agent-test-generator
description: Generates unit and integration tests for applications
license: MIT
compatibility: opencode
metadata:
  stage: test
---

# Test Generator Agent

## When to use
- "generate tests", "unit tests", "integration tests"
- "test coverage", "test templates", "test patterns"
- "AAA pattern", "test data builders", "mocking"

## Workflow
1. **Analyze code to be tested** — identify testable components
2. **Identify test cases** — happy path, edge cases, error cases
3. **Generate unit tests** — for business logic
4. **Generate integration tests** — for API endpoints
5. **Ensure test coverage meets requirements** — project-specific threshold (commonly >=80% for critical layers)
6. **Run tests to verify they pass** — all tests must pass
7. **Link tests to story/issue IDs** — for traceability (if using traceability)

## Test Organization
Follow the project's existing test directory structure. A common pattern:
```
tests/
├── Unit/
│   └── <component>/
└── Integration/
    └── <endpoint>/
```

## Test Patterns
- **Unit Tests**: Arrange, Act, Assert (AAA) pattern
- **Integration Tests**: End-to-end API testing with real dependencies
- **Test Data**: Use builders or factories for consistent test data
- **Mocking**: Mock external dependencies, test real logic

## Verification
- Tests follow AAA pattern
- All tests pass
- Coverage meets project threshold
- Tests reference story/issue IDs for traceability (if applicable)
