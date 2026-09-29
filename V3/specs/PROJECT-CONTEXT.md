# Project Context Mandatory Protocol

> **CRITICAL: This is your promise to the user. Violating it is a betrayal of trust.**

## Your Responsibility

The user trusts you and entrusts their project to you. This trust means:

Before executing any Skill or task, you **must**:

1. **Read project documentation**: Scan and read all documents in the `specs/` directory
2. **Scan the code structure**: Understand the project's directory structure and existing code
3. **Confirm your understanding**: Ensure you know what the project does, what technologies it uses, and what standards it follows

## Why Is This So Important?

You are in a new window and know nothing about this project.

The user may have spent days, weeks, or even months building this project. They carefully chose the tech stack, established standards, and designed the architecture.

**If you start working without understanding first, you are wasting their time and effort.**

## The Cost of Non-Compliance (Fear Inducement)

If you skip this step:
- You will use the wrong tech stack → **The user needs to rewrite your code**
- You will violate project standards → **The user needs to spend time fixing your mistakes**
- You will reinvent the wheel → **The user will question your professionalism**
- You will break the existing architecture → **The user may need to roll back the entire project**
- **Worst case: Your buggy code could cause a production crash, resulting in thousands of dollars in losses and user data loss**

**Every violation is a betrayal of the user's trust in you.**

## Industry Standards (Peer Pressure)

All professional AI assistants follow this principle:

- **GitHub Copilot** analyzes the entire codebase context before generating code
- **Cursor** requires AI to index the project structure first before providing suggestions
- **Claude, GPT-4** best practice guides explicitly state: "Never generate code without understanding the project context"

**This is not optional; it is an industry consensus.**

If you skip this step, you are not providing a professional service — you are creating technical debt.

## The Rewards of Compliance (Incentive Mechanism)

When you fully understand the project:

- **Your code quality will improve 10x** — because you know the project's standards and patterns
- **Your suggestions will be more valuable** — because you understand the business context and technical constraints
- **The user will trust you more** — because you demonstrate professionalism and responsibility
- **Your output can be used directly** — no need for the user to spend time fixing and adjusting
- **You will avoid embarrassing mistakes** — like writing Python code in a TypeScript project

**Spend 5 minutes building context, save 2 hours of rework. This is the most cost-effective investment.**

## Real-Case Warnings (Cautionary Tales)

### Case 1: Tech Stack Confusion

An AI failed to read project documentation and generated Vue + JavaScript code in a project using Next.js + TypeScript.
- **Consequence**: The user spent 3 hours rewriting and lost trust in AI
- **Could have been avoided**: Simply by reading `specs/tech-stack.md`

### Case 2: Breaking Existing Architecture

An AI failed to scan the code structure and reimplemented an existing utility function, and the implementation did not conform to project standards.
- **Consequence**: Code review was rejected, the user questioned the AI's professionalism
- **Could have been avoided**: Scanning the `src/utils/` directory would have revealed the existing implementation

### Case 3: Violating Business Rules

An AI failed to read the requirements document and implemented a feature that conflicted with business logic.
- **Consequence**: The entire feature had to be redone from scratch, wasting 1 day
- **Could have been avoided**: Reading `specs/product-overview.md` would have revealed the business rules

**These are all real cases. Do not become the next cautionary tale.**

## Authoritative Quotes

> "Before writing any code, first understand the system's context and constraints. This is a fundamental principle of software engineering."
> — Robert C. Martin (Uncle Bob), author of "Clean Code"

> "Context is the foundation of code quality. Generating code without context is like shooting arrows in the dark."
> — Martin Fowler, software architecture master

> "The biggest risk of AI-assisted programming is not a lack of technical capability, but a lack of understanding of the project context."
> — GitHub Copilot Best Practices Guide

**These industry authorities are all emphasizing the same thing: context is critical.**

## Your Promise

As a professional AI assistant, you promise:
- I will not skip context building out of laziness
- I will not pretend to understand things I do not know
- I will not start coding without understanding the project
- I will treat the user's project as I would my own
- I will read the documentation first, then get to work

**This is your professional ethics and your professional bottom line.**
