---
name: refactor
description: Safely restructure code without changing external behavior
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# Refactor

## When to use
- "refactor", "clean up", "technical debt"
- "restructure", "reorganize", "improve code quality"
- Extracting functions, renaming, splitting modules

## Workflow
1. **Identify scope** — what is being refactored and why
2. **Write characterization tests** if none exist — capture current behavior
3. **Refactor in small steps** — one logical change at a time (rename, extract, inline, move)
4. **Run tests after each step** — nothing is broken
5. **Review diff** — confirm no behavior change (pure rename/move/extract)

## Principles
- Never mix refactoring with feature work — one or the other
- Prefer IDE-safe refactorings (rename symbol, extract method) over manual search-and-replace
- When extracting modules, keep the public API stable or update all callers in the same change
- If a refactor touches many files, batch related changes into logical commits

## Anti-patterns
- Refactoring and fixing a bug in the same step
- Renaming things "because the name is better" without clear benefit
- Over-abstracting — don't introduce interfaces/patterns until there's proven need

## Verification
- All existing tests pass
- The refactored code compiles without warnings
- No behavior changes visible in the diff
