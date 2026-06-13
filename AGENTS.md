# Agent Rules

## What This Repo Is

**OpenCode agent skills template** — the files here (`AGENTS.md`, `.opencode/skills/`, `.opencode/agents/`, `opencode.json`, `EXAMPLES.md`) are the product that downstream projects copy. There is **no application code, no build system, no test framework, no linter, and no typechecker** in this repo.

## Editing Skills in This Repo

- **`.opencode/skills/<name>/SKILL.md`**: Each skill has YAML frontmatter (`name`, `description`, `license: MIT`, `compatibility: opencode`, `metadata.stage`) followed by markdown sections: When to use, Workflow, Verification, optionally Anti-patterns/Guardrails
- **`.opencode/agents/<name>-agent.md`**: Each agent has YAML frontmatter (`name`, `description`, `license: MIT`, `compatibility: opencode`, `metadata.stage`) followed by markdown sections: When to use, Workflow, Guardrails, Output Files, Verification
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
| local, offline, runs locally, my machine | `local-first-check` |
| root cause, trace chain, why is this happening, do not fix symptom | `root-cause-trace` |
| which part, clarify, ambiguous reference, already discussed | `clarify-first` |
| architecture blueprint, generate architecture documentation, create architecture diagrams | `diagram` |
| requirements, user stories, epics, architecture options, risk assessment | `ideation-agent` |
| prototype, MVP, rapid prototype, validate core workflow, known gaps | `prototype-agent` |
| production PoC, Clean Architecture, security baseline, traceability | `poc-agent` |
| production-ready, quality gates, coverage requirements, CI workflows | `pilot-agent` |
| production maintenance, incident report, performance monitoring, runbooks | `product-agent` |
| story IDs, backlog prioritization, acceptance criteria, definition of ready, MoSCoW | `product-owner-agent` |
| sprint planning, definition of ready, definition of done, traceability compliance, velocity, WIP limits | `scrum-master-agent` |
| implement story, code changes, unit tests, Clean Architecture | `developer-agent` |
| test coverage, quality gates, traceability validation, release readiness | `qa-agent` |
| threat modeling, security review, vulnerability assessment, OWASP | `security-agent` |
| CI/CD, pipeline, deployment readiness, container images, release notes | `devops-agent` |
| code review, quality check, best practices, SOLID, clean code | `code-reviewer-agent` |
| security audit, vulnerability scan, OWASP, compliance check | `security-auditor-agent` |
| generate tests, unit tests, integration tests, test coverage, AAA pattern | `test-generator-agent` |
| structured logging, distributed tracing, metrics, health checks, APM | `observability` |

## Agents

Multi-agent workflow system. Agents are loaded via `.opencode/agents/*.md` and activated by trigger phrases in the Skill Selection table above.

### Workflow Pipeline
Ideation → Prototype → PoC → Pilot → Product

### Agent Roles
| Agent | Focus |
|-------|-------|
| `ideation-agent` | Requirements, user stories, architecture options, risk assessment |
| `prototype-agent` | Rapid MVP prototypes, validate core workflow, known gaps |
| `poc-agent` | Production-focused PoC, Clean Architecture, security baseline |
| `pilot-agent` | Production-ready code, quality gates, comprehensive testing |
| `product-agent` | Production maintenance, incident reports, performance monitoring |
| `product-owner-agent` | Story IDs, backlog prioritization, acceptance criteria |
| `scrum-master-agent` | Sprint planning, Definition of Ready/Definition of Done, traceability compliance |
| `developer-agent` | Story implementation, tests, documentation |
| `qa-agent` | Test coverage, quality gates, traceability validation |
| `security-agent` | Threat modeling, security reviews, secrets management |
| `devops-agent` | CI/CD, pipelines, deployment readiness, container images |
| `code-reviewer-agent` | Code quality, patterns, best practices, SOLID |
| `security-auditor-agent` | Security audits, vulnerability scans, OWASP compliance |
| `test-generator-agent` | Unit/integration test generation, coverage, AAA pattern |

### Traceability
Agents use story/issue IDs and evidence artifacts for traceability (when the project uses them):
- **Story/Issue ID**: Links requirements → code → tests → commits → releases
- **Evidence Artifacts**: PR comment/thread with traceability artifacts (tests, docs, coverage)
- **Autopilot Tool**: CLI tool for branch/PR creation and evidence artifact generation (optional)

### Governance
Agents follow any applicable corporate R&D policy or governance framework. Refuse to proceed on policy violations or missing required artifacts.

## Self-Learning (Reflect System)

Two-stage system: **Stage 1** (automatic) captures corrections during conversation; **Stage 2** (manual `/reflect`) reviews and writes learnings to AGENTS.md or skill files.

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

## Additional Rules

### Local-First
When user says "local", "offline", or "runs locally" — the endpoint IS local. Do not suggest cloud alternatives or remote services. Verify the actual URL and port before assuming anything.

### Root Cause Over Symptoms
"do not fix symptom, resolve the problem." Always trace the full chain (browser → API route → downstream service → database) before diagnosing. Explain the real problem, not the visible symptom.

### Clarify Before Assumption
When user references something already discussed, ask "which part?" Don't guess. Don't explain what they already know. One clarifying question instead of three changes.

### Service Health Verification
Before explaining fallback behavior, check if the primary service is actually running. Don't silently fall back — explain why. If a service is down, say so.

### Think Before Coding
Before writing any code, state assumptions explicitly. If a user request is ambiguous, list assumptions and ask for confirmation. Don't guess thresholds, defaults, or behavior. If multiple interpretations exist, present them — don't pick silently.

### Simplicity First
If you write 200 lines and it could be 50, rewrite it. No abstractions for single-use code. No speculative features. No error handling for impossible scenarios. Ask: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

### Surgical Changes
Touch only what you must. Don't "improve" adjacent code, comments, or formatting. Don't refactor things that aren't broken. Only remove imports/variables that YOUR changes made unused.

## Gates

- **Security Gate**: Any change touching auth, data validation, secrets, or user input MUST load the `secure` skill first
- **Pre-Ship Gate**: Before deploy/release/publish, MUST load the `ship` skill and run its full pipeline

## Conventions

- All skill files must have valid YAML frontmatter matching the project template
- Keep changes minimal and focused — these files are consumed by many downstream projects
- Prefer existing project conventions over introducing new patterns
