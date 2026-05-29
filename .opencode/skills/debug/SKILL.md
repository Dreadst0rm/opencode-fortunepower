---
name: debug
description: Reproduce, isolate, and fix code logic bugs systematically
license: MIT
compatibility: opencode
metadata:
  stage: test
---

# Debug

## When to use
- "bug", "crash", "null pointer", "wrong output"
- "regression", "unexpected behavior"
- Test failures that aren't obviously related to new code

## Workflow
1. **Reproduce** — get a reliable reproduction case (test, script, or steps)
2. **Isolate root cause**:
   - Narrow down by binary search (comment out half the code, check)
   - Check inputs, state, and order of operations
   - Add logging/print statements or use a debugger
3. **Write a failing test** that captures the bug
4. **Fix** — apply the minimal change that resolves the bug
5. **Verify** — the failing test passes, all other tests still pass

## Common root causes
- Null/undefined dereference
- Off-by-one errors in loops
- Race conditions or incorrect async ordering
- Mutable state modified unexpectedly
- Incorrect type coercion
- Floating point precision
- Environment differences (OS, locale, timezone)

## Language-specific notes
- **JavaScript/TypeScript**: use `node --inspect-brk`, `console.log` with JSON.stringify, debugger statements
- **Python**: `pdb`, `ipdb`, `breakpoint()`
- **Rust**: `RUST_BACKTRACE=1`, `println!`, `dbg!`
- **Go**: `delve` debugger, `fmt.Printf`

## Verification
- The bug is fixed with no side effects
- A regression test is added (the failing test from step 3)
- No new warnings or lint errors introduced
