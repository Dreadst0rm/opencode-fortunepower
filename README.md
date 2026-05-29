# OpenCode Agent Skills

Drop-in agent skills and rules for [OpenCode](https://opencode.ai).

## Quick Start: Fresh Install in 2 Steps

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

## What's Included

| Skill | Triggers |
|-------|---------|
| `architect` | architecture, design decision, tradeoffs, ADR |
| `build` | install deps, setup project, compile, build |
| `debug` | bug, crash, wrong output, regression |
| `document` | write docs, document this, README |
| `optimize` | slow, performance, bottleneck, profile |
| `reflect` | remember, reflect, learnings, corrections |
| `refactor` | refactor, clean up, technical debt, restructure |
| `review` | review this code, code review, quality check |
| `secure` | security, vulnerability, owasp, CVE |
| `ship` | deploy, release, publish, ship it |
| `test` | write tests, tdd, test-driven |
| `troubleshoot` | CI failing, dependency conflict, env, config |
| `karpathy-guidelines` | overcomplicated, simplify, surgical, assumptions, verify goals |

## What Each File Does

| File | Purpose |
|------|---------|
| `AGENTS.md` | Agent conversation rules, skill trigger mappings, reflect system config |
| `.opencode/skills/*/SKILL.md` | Per-skill workflows, guardrails, and verification steps (13 skills) |
| `opencode.json` | Opencode config with permission grants |
| `EXAMPLES.md` | Concrete coding-pitfall examples from karpathy-guidelines for reference |

## Customization

- **Add a skill**: `.opencode/skills/<name>/SKILL.md` — opencode discovers it automatically
- **Edit skills**: modify the SKILL.md files to fit your project's conventions
- **Edit agent rules**: modify AGENTS.md to add trigger phrases, project-specific rules, or memory targets

## License

MIT
