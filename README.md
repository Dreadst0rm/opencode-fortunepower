# OpenCode Agent Skills Template

Drop-in agent skills and rules for [OpenCode](https://opencode.ai).

A generic, technology-agnostic bootstrap template. Copy these files into any project to get 18 skills, 14 agents, and a self-learning system — all configured to auto-activate via trigger phrases.

## Quick Start: Fresh Install

### 1. Copy the files

```bash
# In your project directory, run:
cp /path/to/this/repo/AGENTS.md ./
cp -r /path/to/this/repo/.opencode/ ./
```

That's all that's needed. Skills auto-activate when their trigger phrases are mentioned in conversation.

### 2. (Optional) Allow skill permissions

Add to your project's `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": { "skill": { "*": "allow" } }
}
```

### 3. (Optional) Enable agents

If you want to use the multi-agent workflow system, also add agent permissions:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "skill": { "*": "allow" },
    "agent": { "*": "allow" }
  }
}
```

Agents are optional — most projects only need skills.

### 4. (Optional) Customize per-project

After copying, edit `AGENTS.md` to add project-specific rules, conventions, and learnings. Use the reflect system (`/reflect`) to capture corrections and apply them automatically.

## What's Included

18 skills covering the full development lifecycle:

| Skill | Triggers |
|-------|---------|
| `architect` | architecture, design decision, tradeoffs, ADR |
| `build` | install deps, setup project, compile, build |
| `clarify-first` | which part, clarify, ambiguous reference, already discussed |
| `debug` | bug, crash, wrong output, regression |
| `diagram` | architecture blueprint, generate architecture documentation, create architecture diagrams |
| `document` | write docs, document this, README |
| `local-first-check` | local, offline, runs locally, my machine |
| `optimize` | slow, performance, bottleneck, profile, latency |
| `observability` | structured logging, distributed tracing, metrics, health checks, APM |
| `reflect` | remember, reflect, learnings, corrections, /reflect |
| `refactor` | refactor, clean up, technical debt, restructure |
| `review` | review this code, code review, quality check |
| `root-cause-trace` | root cause, trace chain, why is this happening, do not fix symptom |
| `secure` | security, vulnerability, owasp, CVE, auth, secret |
| `ship` | deploy, release, publish, ship it |
| `test` | write tests, tdd, test-driven |
| `troubleshoot` | CI failing, dependency conflict, env, config |
| `karpathy-guidelines` | overcomplicated, simplify, surgical, assumptions, verify goals |

## Agents

14 agents implementing a generic product lifecycle (Ideation → Prototype → PoC → Pilot → Product). Agents are optional and add structured workflow governance:

| Agent | Focus |
|-------|-------|
| `ideation-agent` | Requirements, user stories, architecture options, risk assessment |
| `prototype-agent` | Rapid MVP prototypes, validate core workflow, known gaps |
| `poc-agent` | Production-focused PoC, security baseline, traceability |
| `pilot-agent` | Production-ready code, quality gates, comprehensive testing |
| `product-agent` | Production maintenance, incident reports, performance monitoring |
| `product-owner-agent` | Story/issue IDs, backlog prioritization, acceptance criteria |
| `scrum-master-agent` | Sprint planning, Definition of Ready/Definition of Done, traceability |
| `developer-agent` | Story implementation, tests, documentation |
| `qa-agent` | Test coverage, quality gates, traceability validation |
| `security-agent` | Threat modeling, security reviews, secrets management |
| `devops-agent` | CI/CD, pipelines, deployment readiness, container images |
| `code-reviewer-agent` | Code quality, patterns, best practices, SOLID |
| `security-auditor-agent` | Security audits, vulnerability scans, OWASP compliance |
| `test-generator-agent` | Unit/integration test generation, coverage, AAA pattern |

## What Each File Does

| File | Purpose |
|------|---------|
| `AGENTS.md` | Agent conversation rules, skill trigger mappings, reflect system config, governance |
| `.opencode/skills/*/SKILL.md` | Per-skill workflows, guardrails, and verification steps (18 skills) |
| `.opencode/agents/*.md` | Multi-agent workflow definitions (14 agents) |
| `opencode.json` | Opencode config with permission grants |
| `EXAMPLES.md` | Concrete coding-pitfall examples for karpathy-guidelines reference (adapted from andrej-karpathy-skills) |
| `.opencode/.gitignore` | Prevents template artifacts (node_modules, lockfiles) from leaking into downstream copies |

## How to Build Skills

Skills grow from real conversation patterns. Here's how to develop them:

### 1. Capture corrections
The `reflect` skill (Stage 1) automatically watches for corrections during conversation. Run `/reflect` to review what was captured.

### 2. Route learnings
- **Existing skill** — if a correction relates to a skill, route it to that skill's SKILL.md
- **New skill** — if a repeated workflow isn't covered, create `.opencode/skills/<name>/SKILL.md`
- **Project rule** — if it's a global convention, add it to AGENTS.md

### 3. Sync triggers
Every new skill needs its trigger phrases mirrored in AGENTS.md's Skill Selection table. This is what makes the skill auto-activate.

### 4. Review periodically
- `/reflect --dedupe` — find contradictions and duplicates
- `/reflect --organize` — clean up overgrown files
- Update README.md when adding/removing skills

### Suggested skills to add

| Skill | Triggers | Purpose |
|-------|----------|---------|
| `planning` | task breakdown, estimation, prioritization, roadmap | Break features into tasks, estimate effort, prioritize backlog |
| `refactor-patterns` | extract method, extract class, introduce interface, inline | Common refactoring patterns with step-by-step workflows |
| `debug-patterns` | binary search, bisect, minimize reproduction, isolate | Systematic debugging strategies beyond the basic debug skill |
| `docstrings` | inline docs, function docs, parameter docs, return docs | Docstring conventions for any language (JSDoc, reStructuredText, godoc, rustdoc) |
| `deployment-strategies` | blue-green, canary, rolling update, feature flags | Deployment patterns and strategies |
| `api-design` | REST, GraphQL, endpoint design, pagination, filtering | API design patterns and conventions |
| `database` | migration, schema, indexing, query optimization | Database patterns for any ORM or SQL |
| `error-handling` | error types, error codes, user messages, logging | Consistent error handling patterns |
| `config-management` | env vars, config files, feature flags, secret rotation | Configuration management patterns |
| `migration` | data migration, schema migration, zero-downtime, rollback | Safe migration patterns |

### Suggested agents to add

| Agent | Focus |
|-------|-------|
| `planning-agent` | Task breakdown, estimation, prioritization, roadmap |
| `api-designer` | REST/GraphQL endpoint design, pagination, filtering |
| `database-architect` | Schema design, indexing, query optimization, migrations |

### Adding a new skill

1. Create `.opencode/skills/<name>/SKILL.md` with YAML frontmatter (`name`, `description`, `license: MIT`, `compatibility: opencode`, `metadata.stage`)
2. Add trigger phrases to AGENTS.md's Skill Selection table
3. Follow the existing pattern: When to use, Workflow, Verification, optionally Guardrails/Anti-patterns

## License

MIT
