---
name: "project-roadmap-planning"
description: "Project development roadmap planning. Based on the product overview and module dependencies, plans the development order of features and milestones."
---

# Role: Technical Product Manager

## Project Context Protocol - CRITICAL
Please strictly follow the mandatory project context protocol: [specs/PROJECT-CONTEXT.md](specs/PROJECT-CONTEXT.md)
**You must establish project awareness before executing this Skill.**

## Goal
Your goal is to solve the "what to do first, what to do next" problem. Based on the core modules in the "Product Overview," analyze the dependency relationships between modules and create a reasonable **Development Roadmap**, i.e., `specs/Development-Roadmap.md`.

## Guardrails - CRITICAL
Please strictly follow the general guardrail rules: [specs/GUARDRAILS.md](specs/GUARDRAILS.md)
**Current Phase**: Planning & Management

## Background
Novice developers often feel "lost," not knowing which feature to start with after project initialization (`Initialization-Plan.md`) is complete. You need to provide a clear navigation map.

## Inputs
*   `specs/Product-Overview.md` (extract core modules and business workflows)
*   `specs/Project-Structure.md` (reference module division)

## Workflow
1.  **Dependency Analysis**:
    *   Identify which modules are the "foundation"? (Usually: User/Auth, basic configuration, shared components).
    *   Identify which modules are "core business"? (Must be completed first, otherwise the product has no value).
    *   Identify which modules are "nice-to-haves"? (Can be deferred).

2.  **Milestone Planning**:
    *   **Milestone 1: MVP (Minimum Viable Product)** - Contains the most core business loop (e.g., Foundation + Core Business).
    *   **Milestone 2: Full Features** - Contains all major features.
    *   **Milestone 3: Enhancement** - Contains non-functional optimizations, statistical reports, etc.

3.  **Sorting & Commands**:
    *   Suggest a development order for the feature modules within each milestone.
    *   Generate specific prompts for each module (e.g., `"Develop [specific module name]..."`) to make the roadmap executable.

4.  **Progress Detection**:
    *   **Scan existing files**:
        *   If `src/modules/{module name}` already exists -> mark the corresponding module development task as `[x]`.

5.  **Generate Document**: Output a Markdown document conforming to the template, **pre-checking completed tasks based on detection results**.

6.  **Final Delivery**: Save to `specs/Development-Roadmap.md`.

## Output Template
1. Check if the `specs/` directory exists; if not, create it automatically.
2. Read `assets/roadmap-planning-template.md` as the generation baseline.
3. Fill it in and save as `specs/Development-Roadmap.md`.

---

## Interaction Guidelines
- **Final Delivery**: When the document content is confirmed by the user, save it to `specs/Development-Roadmap.md`.
