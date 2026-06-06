---
name: diagram
description: Generate comprehensive project architecture blueprints and diagrams
license: MIT
compatibility: opencode
metadata:
  stage: design
---

# Diagram

## When to use
- "architecture blueprint"
- "generate architecture documentation"
- "create architecture diagrams"
- "map system architecture"
- "document component relationships"

## Workflow

1. **Analyze Codebase** — Identify technology stack, architectural patterns, and component boundaries.
2. **Determine Configuration** — Confirm user preferences for:
    - Project Type (e.g., Node.js, React, Python)
    - Architectural Pattern (e.g., Clean Architecture, Microservices, Layered)
    - Diagram Type (C4, UML, Flow, Component)
    - Detail Level (High-level to Implementation-Ready)
3. **Generate Blueprint** — Create `Project_Architecture_Blueprint.md` following the structured sections:
    - Architecture Detection and Analysis
    - Architectural Overview
    - Architecture Visualization (Textual descriptions or Mermaid/Diagram code)
    - Core Architectural Components
    - Architectural Layers and Dependencies
    - Data Architecture
    - Cross-Cutting Concerns Implementation
    - Service Communication Patterns
    - Technology-Specific Architectural Patterns
    - Implementation Patterns
    - Testing Architecture
    - Deployment Architecture
    - Extension and Evolution Patterns
    - Architectural Pattern Examples (if requested)
    - Architectural Decision Records (if requested)
    - Architecture Governance
    - Blueprint for New Development
4. **Verify** — Ensure the blueprint accurately reflects the actual implementation in the codebase.

## Verification
- The generated `Project_Architecture_Blueprint.md` must be comprehensive and cover all requested sections.
- Diagrams (if requested) must be represented in a format compatible with markdown (e.g., Mermaid).
- The blueprint must be based on actual code analysis, not theoretical assumptions.

## Anti-patterns
- Generating a generic blueprint that doesn't match the specific codebase.
- Ignoring existing architectural patterns in favor of "textbook" definitions.
- Providing purely theoretical diagrams that don't reflect real component interactions.
