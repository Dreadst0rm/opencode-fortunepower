---
name: build
description: Detect project language, install dependencies, and compile/build the project
license: MIT
compatibility: opencode
metadata:
  stage: build
---

# Build

## When to use
- "install deps", "setup project", "compile", "build"
- "npm install", "pip install", "go build", "cargo build"
- First-time project setup or rebuilding

## Workflow
1. **Detect project type** by examining `package.json`, `Cargo.toml`, `go.mod`, `pyproject.toml`, `requirements.txt`, `Makefile`, etc.
2. **Resolve package manager** (npm, bun, uv, pip, cargo, go, mvn, gradle)
3. **Install dependencies** using the correct package manager
4. **Build/compile** the project
5. **Fix build errors** if any, in order of dependency chain

## Language-specific notes
- **Node.js**: prefer `package-lock.json` or `bun.lock`; use `npm ci` for deterministic installs
- **Python**: prefer `uv` over `pip`; use `uv sync` for `pyproject.toml` projects
- **Rust**: `cargo build`; check `rust-toolchain.toml` for version
- **Go**: `go mod tidy` then `go build ./...`
- **Multi-language**: install layer by layer (system → language runtime → project deps)

## Verification
- Build completes with exit code 0
- No unresolved dependency errors
- Artifacts exist at expected paths
