---
name: document
description: Generate and maintain README, API docs, docstrings, and project documentation
license: MIT
compatibility: opencode
metadata:
  stage: review
---

# Document

## When to use
- "write docs", "document this", "README"
- "api docs", "docstring", "update documentation"
- "how do I use this?", "missing docs"

## Workflow
1. **Identify what to document**:
   - Public API: exported functions, classes, types, endpoints
   - Project: README, contribution guide, setup instructions
   - Internal: complex logic, non-obvious decisions
2. **Write/fix docstrings** — include: purpose, params, return, raises/exceptions, example if non-trivial
3. **Update README**:
   - What the project does
   - Quick start / setup
   - Usage examples
   - API reference (or link to it)
   - Configuration reference
4. **Generate API docs** if applicable (JSDoc, Sphinx, godoc, rustdoc)

## Style guidelines
- Docstrings: follow the language standard (JSDoc, reStructuredText, godoc, rustdoc)
- README: clear, concise, start with what and why, then how
- Examples: always include runnable examples for the primary use case
- Keep docs close to code (inline docstrings > separate docs)

## Verification
- Every public API has a docstring
- README is up to date with the current state
- Examples in docs actually work
- No outdated/contradictory documentation
