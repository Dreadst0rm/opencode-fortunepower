# Agent Rules

## What This Repo Is

**OpenCode agent skills template** — the files here (`AGENTS.md`, `.opencode/skills/`, `opencode.json`, `EXAMPLES.md`) are the product that downstream projects copy. There is **no application code, no build system, no test framework, no linter, and no typechecker** in this repo.

## Editing Skills in This Repo

- **`.opencode/skills/<name>/SKILL.md`**: Each skill has YAML frontmatter (`name`, `description`, `license: MIT`, `compatibility: opencode`, `metadata.stage`) followed by markdown sections: When to use, Workflow, Verification, optionally Anti-patterns/Guardrails
- **Mirror triggers**: Trigger phrases in the Skill Selection table below must stay in sync with each skill's "When to use" section
- **New skill**: Create `.opencode/skills/<name>/SKILL.md` — opencode auto-discovers it
- **Changes to AGENTS.md, skill files, or EXAMPLES.md** affect all downstream projects; be surgical
- **`.opencode/.gitignore`** prevents template files (node_modules, package.json, lockfiles) from leaking into downstream copies

## Lifecycle Enforcement

Every task follows this pipeline:
1. **Build** — compile, install deps, resolve setup
2. **Test** — write and run tests
3. **Review** — review code quality before completing

## Skill Selection

When a task matches a skill's trigger phrases, you MUST load and follow that skill before acting.

| Trigger | Skill |
|---------|-------|
| compile, build, install, setup deps | `build` |
| test, spec, coverage, tdd | `test` |
| review, audit, quality, check | `review` |
| security, vulnerability, owasp, CVE, auth, secret | `secure` |
| refactor, clean, technical debt, restructure | `refactor` |
| bug, null, crash, wrong output, regression | `debug` |
| CI failing, deploy error, dependency conflict, env, port, config | `troubleshoot` |
| architecture, design, decision, ADR, tradeoff | `architect` |
| document, readme, api docs, docstring | `document` |
| slow, performance, bottleneck, profile, latency | `optimize` |
| deploy, release, tag, publish, CI | `ship` |
| remember, reflect, learning, correction, save this, /reflect, /reflect-skills, /skip-reflect, /view-queue, discover skill, find pattern, skill candidate | `reflect` |
| overcomplicated, simplify, surgical, assumptions, verify goals | `karpathy-guidelines` |

## Self-Learning (Reflect System)

Two-stage system from claude-reflect: **Stage 1** (automatic) captures corrections during conversation; **Stage 2** (manual `/reflect`) reviews and writes learnings to AGENTS.md or skill files.

**Capture Rules:**
- `remember:` markers are always captured
- Direct corrections, negative instructions, clarifications, guardrails → capture
- Questions, greetings, one-time task instructions → discard

**Memory Targets:**
- AGENTS.md — project-level rules
- `.opencode/skills/*/SKILL.md` — per-skill improvements
- `.opencode/skills/<name>/SKILL.md` — new skill from discovered patterns

**Commands:**
- `/reflect` — review & apply / `/reflect --dry-run` — preview / `/reflect --dedupe` — find contradictions
- `/reflect-skills` — discover skill candidates / `/skip-reflect` — discard / `/view-queue` — view pending

## Gates

- **Security Gate**: Any change touching auth, data validation, secrets, or user input MUST load the `secure` skill first
- **Pre-Ship Gate**: Before deploy/release/publish, MUST load the `ship` skill and run its full pipeline

## Conventions

- All skill files must have valid YAML frontmatter matching the project template
- Keep changes minimal and focused — these files are consumed by many downstream projects
- Prefer existing project conventions over introducing new patterns
