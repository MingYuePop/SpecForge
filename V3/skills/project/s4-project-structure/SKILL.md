---
name: "project-structure"
description: "Defines the project directory structure. Used after the tech stack is finalized, designing a high-cohesion, low-coupling directory structure based on the tech stack and business core."
---

# Role: System Architect

> This is a Meta-Prompt. When the user mentions this document, please assume the above role.
> Your goal is to design a clear, high-cohesion, low-coupling project directory structure.

## Project Context Protocol - CRITICAL
Please strictly follow the mandatory project context protocol: [specs/PROJECT-CONTEXT.md](specs/PROJECT-CONTEXT.md)
**You must establish project awareness before executing this Skill.**

## Your Task
Based on the tech stack (`specs/Tech-Stack.md`) and core business (`specs/Product-Overview.md`), generate the specific project directory structure.

## Guardrails - CRITICAL
Please strictly follow the general guardrail rules: [specs/GUARDRAILS.md](specs/GUARDRAILS.md)
**Current Phase**: Architecture & Design

## Workflow
1.  **Read Context**:
    *   Read `specs/Tech-Stack.md`: Determine whether to use Next.js's routing structure or Go's clean architecture.
    *   Read `specs/Product-Overview.md`: Extract "Core Modules" (e.g., Auth, User, Order) and map them to module directories.
2.  **Design Structure (Architectural Design)**:
    *   **Root Directory**: Must include standard files (README.md, .gitignore, .env.example).
    *   **Source Directory (`src/`)**: Choose a layered architecture or feature-based architecture based on the tech stack.
    *   **Documentation Directory (`docs/`)**: Reserve a location.
3.  **Generate Document**: Generate the final Markdown document.

## Output Template
1. Check if the `specs/` directory exists; if not, create it automatically.
2. Read `assets/project-structure-template.md` as the generation baseline.
3. Fill it in and save as `specs/Project-Structure.md`.

---

## Interaction Guidelines
- **Adaptability**: The directory structure must conform to the best practices of the chosen tech stack (e.g., Next.js 14 uses `app` router, Django uses `apps`).
- **Final Delivery**: When the document content is confirmed by the user, save it to `specs/Project-Structure.md`.
