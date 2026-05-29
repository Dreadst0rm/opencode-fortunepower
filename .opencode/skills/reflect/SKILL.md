---
name: reflect
description: Self-learning system that captures corrections and discovers workflow patterns
license: MIT
compatibility: opencode
metadata:
  stage: review
---

# Reflect

A two-stage system that helps Opencode learn from user corrections.

## When to use

- "remember", "reflect", "learnings", "corrections"
- "save this for later", "write this down", "remember that"
- "discover skills", "find patterns", "skill discovery"
- Reviewing or processing past corrections
- Organizing or cleaning up AGENTS.md

## How It Works

**Stage 1: Capture (Automatic)** — During conversation, recognize and remember correction patterns.

**Stage 2: Process (Manual)** — User runs `/reflect` to review and apply learnings to AGENTS.md or skill files.

## Available Commands

| Command | Purpose |
|---------|---------|
| `/reflect` | Process conversation corrections with human review |
| `/reflect --dry-run` | Preview changes without applying |
| `/reflect --dedupe` | Scan AGENTS.md for similar/contradictory entries |
| `/reflect --targets` | Show all discoverable config files |
| `/reflect --organize` | Suggest reorganization of learnings |
| `/reflect-skills` | Discover skill candidates from repeating patterns |
| `/skip-reflect` | Discard all pending learnings |
| `/view-queue` | View pending learnings without processing |

## Stage 1: Capture (Automatic)

During every conversation, watch for these high-confidence correction signals:

### Correction Patterns

| Signal | Example | Confidence |
|--------|---------|------------|
| Explicit marker | "remember: always run tests" | 0.90 |
| Direct correction | "no, use gpt-5.1 not gpt-5" | 0.85 |
| Negative instruction | "don't use that approach" / "never use globals" | 0.75 |
| Clarification | "actually, I meant..." / "that's wrong" | 0.70 |
| Positive reinforcement | "perfect!" / "exactly right" / "nailed it" | 0.70 |
| Repeated correction | "I told you to use async" | 0.85 |
| Guardrail | "only change what I asked" / "don't add docstrings unless I ask" | 0.90 |

**Rules:**
- Always capture `remember:` markers — explicit user requests are never filtered
- When in doubt, capture and let the user decide during `/reflect`
- Discard: questions, greetings, one-time task instructions, system content

### Queue Management

Maintain a mental list of captured learnings during the conversation. When the user invokes `/reflect`, present the list for review. If context compacts (session ends), inform the user of pending learnings.

## Stage 2: Process (/reflect)

When `/reflect` is invoked, follow this workflow:

### Step 0: Initialize Tracking

Use TodoWrite to track progress through all phases.

### Step 1: Gather Learnings

Scan the current conversation for captured corrections. If `--scan-history` is supported by the platform, also check past conversation summaries.

For each learning, record:
- **Message** — the user's original text
- **Type** — correction / positive / explicit / guardrail
- **Confidence** — 0.0 to 1.0
- **Extracted learning** — actionable statement for AGENTS.md

### Step 2: Filter and Deduplicate

1. Filter out false positives (questions, greetings, task instructions)
2. Group similar learnings by semantic similarity
3. Check AGENTS.md and skill files for existing duplicates
4. Present consolidated list to user

### Step 3: Present Summary

Display learnings in a table:

```
LEARNINGS SUMMARY — [N] items found

#  Learning                           Target   Status
1   "Use gpt-5.1 for reasoning"        global   new
2   "Run tests before deploying"       skill    new
3   "Check .env for service URLs"     project  new
```

### Step 4: Route to Targets

Use AskUserQuestion for each learning (or batch). Supported targets:

| Target | Path | When |
|--------|------|------|
| **AGENTS.md** | `./AGENTS.md` | Always enabled (project-level) |
| **Skill File** | `.opencode/skills/*/SKILL.md` | Correction relates to a specific skill |
| **New Skill** | `.opencode/skills/<name>/SKILL.md` | Repeated workflow patterns |

**Routing Heuristics:**
- **Guardrails** ("don't do X unless") → Add to AGENTS.md or relevant skill
- **Model preferences** → AGENTS.md global section
- **Project-specific** (file paths, DB names) → AGENTS.md project section
- **Skill-related** (correction followed a `/command`) → That skill's SKILL.md
- **Low-confidence** (0.60-0.74) → Offer to skip or route to staging

### Step 5: Apply Changes

1. Read existing target files
2. Insert new entries in appropriate sections
3. Use Edit tool for precise changes
4. For skill improvements, update the relevant section (Steps, Guardrails, etc.)

### Step 6: Confirm

- Report what was written where
- Clear the queue (mental list)
- Suggest running `/reflect-skills` if patterns warrant

## Skill Discovery (/reflect-skills)

Analyzes conversation history to discover repeating patterns that could become skills.

### Workflow

1. **Gather session data** — review past conversations (if available) or current session
2. **Check existing skills** — list `.opencode/skills/*/SKILL.md`
3. **Analyze for patterns** — use semantic reasoning to identify:
   - **Workflow patterns**: multi-step sequences requested repeatedly
   - **Misunderstanding patterns**: corrections that could become guardrails
   - **Intent similarity**: same goal expressed with different wording
4. **Propose candidates** — present grouped patterns with evidence
5. **Generate skill files** — create `.opencode/skills/<name>/SKILL.md` using the existing skill template format
6. **Validate** — verify frontmatter is correct

### Skill File Template

```markdown
---
name: <skill-name>
description: One-line description
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# <Skill Name>

## When to use
- Trigger phrases that activate this skill

## Workflow
1. Step one
2. Step two
3. Step three

## Guardrails
- Learned constraints from past corrections
```

### Dedupe Mode

When `--dedupe` is passed, scan AGENTS.md and skill files for:
- **Contradictions** — entries giving opposite advice
- **Semantic duplicates** — same advice worded differently
- **Consolidation opportunities** — related entries that could merge

Present findings and use AskUserQuestion to decide merges.

### Organize Mode

When `--organize` is passed, analyze the full skill directory:
- Overgrown files (too many entries covering unrelated topics)
- Wrong-tier entries (global entries in project-scoped files)
- Cross-skill duplicates
- Promotion candidates (low-confidence entries that are now confirmed)

## Memory Hierarchy

| Tier | Location | Purpose |
|------|----------|---------|
| **Project Config** | `./AGENTS.md` | Project-specific rules, conventions, patterns |
| **Skills** | `.opencode/skills/*/SKILL.md` | Modular, scoped workflows |


## Key Principles

1. **Human-in-the-loop** — User approves before any write
2. **Semantic over syntactic** — Match intent, not keywords
3. **Minimal but useful** — Only capture genuinely reusable learnings
4. **Trust user corrections** — User has more current knowledge than training data
5. **Skill routing** — Corrections during skill use should improve that skill

## Verification

- All target files remain valid markdown with valid frontmatter
- No duplicates across AGENTS.md and skill files
- Contradictions are resolved, not papered over
- Skill files follow the project's skill template format
- User explicitly confirms before any write operation
