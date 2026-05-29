---
name: troubleshoot
description: Diagnose and resolve environment, CI, deployment, dependency, and configuration issues
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# Troubleshoot

## When to use
- "CI failing", "build failure on CI", "deploy error"
- "dependency conflict", "version mismatch"
- "environment", "setup issue", "port conflict"
- "config error", "permission denied", "command not found"

## Workflow
1. **Gather diagnostics**:
   - Check error logs, stack traces, CI output
   - Verify environment variables, OS version, tool versions
   - Check port availability, filesystem permissions, network connectivity
2. **Identify root cause**:
   - Is it an environmental mismatch? (local works, CI fails)
   - Is it a configuration error? (wrong path, missing env var)
   - Is it a dependency conflict? (semver mismatch, incompatible peer deps)
3. **Apply fix**:
   - Pin/tighten dependency versions if needed
   - Fix config files, env vars, or path references
   - Update CI pipeline configuration
4. **Verify**:
   - Run the same command locally or replicate CI environment
   - Confirm the issue is resolved

## Common scenarios
- **CI-specific failures**: OS differences, missing system deps, cache invalidation
- **Port conflicts**: check `netstat`/`lsof` for what's using the port; use dynamic ports or configurable ports
- **Dependency resolution**: clear lock file and reinstall; check for hoisting issues in monorepos
- **Permission errors**: wrong ownership on mounted volumes, CI runner UID mismatch
- **Path issues**: hardcoded absolute paths, case sensitivity on Linux vs macOS

## Verification
- The failing command now succeeds
- The fix is documented in a config file or CI config, not just a one-off manual workaround
- If a version pin was added, include a comment explaining why
