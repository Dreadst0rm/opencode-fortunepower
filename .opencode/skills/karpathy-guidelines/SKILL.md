---
name: karpathy-guidelines
description: Behavioral guidelines to reduce common LLM coding mistakes — surface assumptions, keep things simple, make surgical changes, define verifiable success criteria
license: MIT
compatibility: opencode
metadata:
  stage: design
---

# Karpathy Guidelines

Behavioral guidelines to reduce common LLM coding mistakes, derived from [Andrej Karpathy's observations](https://x.com/karpathy/status/2015883857489522876) on LLM coding pitfalls.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform imperative tasks into verifiable goals:

| Instead of... | Transform to... |
|-----|-----|
| "Add validation" | "Write tests for invalid inputs, then make them pass" |
| "Fix the bug" | "Write a test that reproduces it, then make it pass" |
| "Refactor X" | "Ensure tests pass before and after" |

For multi-step tasks, state a brief plan:

```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

## Anti-Pattern: Jumping to Implementation

**User Request:** "Walk through the app and fix issues"

**Bad Response (Assumes thresholds, guesses behavior):**
```
// Writes 7 hardcoded phase thresholds without asking
// Writes resetState() helper when window.location.href would work
// Assumes navigation placement instead of asking where
```

**Good Response (States assumptions, asks for confirmation):**
```
Before fixing, I need to clarify:

1. **Phase progression** — How should phases progress? By lesson count? By score? By time?
2. **Celebration redirect** — After finishing, do you want to go home, or stay on the lesson page?
3. **Navigation** — Where exactly should the home link go? Header? Somewhere else?

I'll wait for your answer before writing code.
```

## Key Insight

The "overcomplicated" examples aren't obviously wrong — they follow design patterns and best practices. The problem is **timing**: they add complexity before it's needed, which makes code harder to understand, introduces more bugs, takes longer to implement, and is harder to test.

The "simple" versions are easier to understand, faster to implement, easier to test, and can be refactored later when complexity is actually needed.

**Good code is code that solves today's problem simply, not tomorrow's problem prematurely.**

**Best code asks questions before writing a single line.**
