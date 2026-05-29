---
name: review
description: Review code for correctness, style, edge cases, and maintainability
license: MIT
compatibility: opencode
metadata:
  stage: review
---

# Review

## When to use
- "review this code", "code review", "quality check"
- "audit", "is this correct?"
- Before merging any changes

## Workflow
1. **Read the full diff** — understand what changed and why
2. **Check correctness**:
   - Does the logic handle the intended case?
   - Are there off-by-one, null/undefined, or type errors?
3. **Check edge cases**:
   - Empty inputs, zero values, boundary conditions
   - Concurrency/race conditions if applicable
4. **Check error handling**:
   - Are errors properly caught/propagated?
   - Are error messages actionable?
5. **Check maintainability**:
   - Is the code readable? Would another dev understand it in 6 months?
   - Are there magic numbers/strings that should be constants?
6. **Check consistency**:
   - Does it match the surrounding code style?
   - Does it follow the project's established patterns?

## What to flag
- Logic bugs or incorrect assumptions
- Missing error handling
- Hardcoded values that should be configurable
- Dead code or commented-out code
- Security concerns (defer to `secure` skill)
- Missing tests or incomplete coverage

## What NOT to flag
- Style preferences not enforced by the project's formatter
- Trivial naming differences that are still clear

## Verification
- All issues are documented with file:line references
- Each issue has a severity: error / warning / suggestion
- The author should address all errors and warnings before merge
