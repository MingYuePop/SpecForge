# Development Standards

This document defines the code style, naming conventions, Git workflow, and AI collaboration protocols for the [Project Name] project, ensuring long-term maintainability of the codebase.

---

## 1. Language and Runtime Requirements

| Dimension | Specification |
|------|------|
| **Language** | [e.g., TypeScript 5.x, unified across the stack] |
| **Runtime** | [e.g., Node.js >= 18.17] |
| **Package Manager** | [e.g., pnpm >= 8.0 (using npm / yarn is prohibited)] |
| **Strict Mode** | [e.g., `strict: true`, `any` is prohibited (special cases must be commented with reason)] |

---

## 2. Code Style and Lint Rules

### 2.1 Toolchain

| Tool | Responsibility | Config File |
|------|------|----------|
| **[Formatter]** | [e.g., Code formatting] | [e.g., `.prettierrc`] |
| **[Lint Tool]** | [e.g., Code quality checks] | [e.g., `.eslintrc.json`] |
| **[Type Checker]** | [e.g., Type safety] | [e.g., `tsconfig.json`] |

### 2.2 Lint Rules Overview

> Extended from [base rule set], with the following key rules additionally enabled:

```jsonc
// Provide the specific config JSON, including each custom rule and its value
{
  "extends": ["..."],
  "rules": {
    // [rule name]: [value] — briefly explain why this rule is enabled
  }
}
```

### 2.3 Formatting Configuration

```jsonc
// Provide the specific formatter config JSON
{
  // Every config option should be included, especially semicolons, quotes, trailing commas, print width, indentation, etc.
}
```

**Key Decision Explanations** (explain the reasoning for controversial options):
- `[Option]`: [Why this value was chosen]
- `[Option]`: [Why this value was chosen]

### 2.4 IDE Configuration

```jsonc
// Provide .vscode/settings.json or equivalent configuration
{
  // formatOnSave, defaultFormatter, codeActionsOnSave, etc.
}
```

---

## 3. Naming Conventions

### 3.1 File and Directory Naming

| Type | Naming Style | Example |
|------|---------|------|
| **[Component files]** | [e.g., `kebab-case.tsx`] | [e.g., `article-card.tsx`] |
| **[Non-component files]** | [e.g., `kebab-case.ts`] | [e.g., `format.ts`] |
| **[Server Actions]** | [Determined by framework] | [e.g., `article.ts`] |
| **[Type definitions]** | [e.g., `kebab-case.ts`] | [e.g., `database.ts`] |
| **[Directories]** | [e.g., `kebab-case`] | [e.g., `article-card/`] |
| **[Test files]** | [e.g., `*.test.ts`] | [e.g., `format.test.ts`] |

### 3.2 Code Naming

| Element | Naming Style | Example |
|------|---------|------|
| **Components** | [e.g., `PascalCase`] | [e.g., `ArticleCard`] |
| **Functions** | [e.g., `camelCase`] | [e.g., `formatDate`] |
| **Variables** | [e.g., `camelCase`] | [e.g., `articleCount`] |
| **Constants** | [e.g., `SCREAMING_SNAKE_CASE`] | [e.g., `MAX_TITLE_LENGTH`] |
| **Types / Interfaces** | [e.g., `PascalCase`] | [e.g., `Article`] |
| **Boolean variables** | [e.g., `is/has/should` prefix] | [e.g., `isPublished`] |
| **Event handlers** | [e.g., `handle` + event name] | [e.g., `handleSubmit`] |

### 3.3 Route Naming

| Type | Rule | Example |
|------|------|------|
| **Page routes** | [e.g., lowercase kebab-case] | [e.g., `/editor`] |
| **Dynamic routes** | [e.g., `[param]` format] | [e.g., `/editor/[id]`] |
| **API routes** | [e.g., plural resource names] | [e.g., `/api/articles/[id]`] |

---

## 4. [Language]-Specific Standards

> The title and content of this section are dynamically adjusted based on the project language (TypeScript / Go / Python / Rust, etc.)

### 4.1 [Language Feature 1]

[e.g., Type import preferences]

```[lang]
// Correct way
// Incorrect way
```

### 4.2 [Language Feature 2]

[e.g., interface vs type usage scenarios]

| Scenario | Preference | Reason |
|------|------|------|
| [Scenario 1] | [Choice] | [Reason] |
| [Scenario 2] | [Choice] | [Reason] |

### 4.3 Patterns to Avoid

```[lang]
// Avoid: [description]
[incorrect code]

// Alternative: [description]
[correct code]
```

> List at least 3-5 common incorrect patterns and their correct alternatives

---

## 5. [Framework]-Specific Standards

> The title and content of this section are dynamically adjusted based on the project framework (React / Vue / Svelte / Go Gin, etc.)

### 5.1 Component Design Principles

- [Principle 1]: [Description]
- [Principle 2]: [Description]
- [Principle 3]: [Description]

### 5.2 Component File Structure

```[lang]
// Show a complete structure template for a standard component, including:
// 1. Declaration (e.g., 'use client')
// 2. Type imports
// 3. Dependency imports
// 4. Type definitions
// 5. Component definition
```

### 5.3 Import/Export Rules

- [Export preference: named exports vs default exports]
- [Exceptions]

### 5.4 Import Sorting

```[lang]
// Group in the following order, with a blank line between groups:
// 1. [Group 1]
// 2. [Group 2]
// 3. [Group 3]
// 4. [Group 4]
```

### 5.5 [Framework-Specific Hooks / Composables] Usage Standards

- [Naming rules]
- [Storage location]
- [Usage notes]

---

## 6. Styling Standards

### 6.1 Sole Styling Solution

- [Solution name]: [Usage principle description]
- [Dynamic class name handling]
- [Responsive design strategy]

```[lang]
// Correct usage example
```

### 6.2 Prohibited Styling Patterns

```[lang]
// [Prohibited pattern 1]
// [Prohibited pattern 2]
// [Prohibited pattern 3]
// [Correct pattern]
```

---

## 7. Git Workflow

### 7.1 Branch Strategy

> Choose based on team size: Solo developer → Simplified Trunk-Based / Small team → GitHub Flow / Large team → Git Flow

```
[Use ASCII diagram to show the branch model]
```

| Rule | Description |
|------|------|
| **Main branch** | [e.g., `main`, always deployable] |
| **Feature branches** | [Source and merge target] |
| **Branch lifecycle** | [e.g., 1-3 days] |
| **Merge method** | [e.g., Squash Merge] |

### 7.2 Branch Naming Conventions

```
<type>/<short-description>
```

| Type | Purpose | Example |
|------|------|------|
| `feat/` | New feature | [e.g., `feat/article-publish`] |
| `fix/` | Bug fix | [e.g., `fix/auth-redirect-loop`] |
| `refactor/` | Refactoring | [e.g., `refactor/supabase-client`] |
| `docs/` | Documentation updates | [e.g., `docs/api-spec`] |
| `chore/` | Build/config | [e.g., `chore/upgrade-deps`] |

### 7.3 Commit Message Standards (Conventional Commits)

All Git commit messages **must** follow the [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>(<scope>): <subject>

[body]

[footer]
```

#### Type

| Type | Description | Example |
|------|------|------|
| `feat` | New feature | |
| `fix` | Bug fix | |
| `refactor` | Refactoring (no functional change) | |
| `style` | Code formatting changes | |
| `docs` | Documentation changes | |
| `test` | Test related | |
| `chore` | Build/tools/dependencies | |
| `perf` | Performance optimization | |
| `ci` | CI/CD configuration | |

#### Scope

> Extracted from the project's features modules and common domains, listed in a table

| scope | Corresponding Scope |
|-------|---------|
| [Module 1] | [Scope description] |
| [Module 2] | [Scope description] |
| ... | ... |

#### Commit Message Rules
- `subject`: [Language], [Case], [Punctuation], [Length limit]
- `body`: Explain **why**, not **what**
- `footer`: Issue reference format

#### Examples

> Provide at least 2 complete commit message examples relevant to this project's business

```
[Example 1: feat type, with body and footer]
```

```
[Example 2: fix type, with body explaining root cause]
```

---

## 8. Code Comment Standards

### 8.1 When to Write Comments

| Needs Comment | Does Not Need Comment |
|----------|-----------|
| [Scenario 1] | [Scenario 1] |
| [Scenario 2] | [Scenario 2] |
| [Scenario 3] | [Scenario 3] |
| [Scenario 4] | [Scenario 4] |

### 8.2 Comment Style

```[lang]
// Explains "why"
[good comment example]

// Describes "what"
[bad comment example]
```

### 8.3 TODO / FIXME / HACK Markers

```[lang]
// TODO: [Format description]
// FIXME: [Format description]
// HACK: [Format description]
```

---

## 9. Error Handling Standards

### 9.1 Server-Side Error Handling

> Consistent with API design standards, provide a unified error return type

```[lang]
// Unified error return type definition
```

### 9.2 Client-Side Error Handling

- [Principle 1]
- [Principle 2]
- [Principle 3]

### 9.3 Security Principles
- Never expose raw error stacks or database error messages in the UI
- Form validation executed twice: client-side (instant feedback) + server-side (security guarantee)

---

## 10. Testing Standards

### 10.1 Testing Tools

| Tool | Purpose |
|------|------|
| [Tool 1] | [Purpose] |
| [Tool 2] | [Purpose] |

### 10.2 Testing Priorities

> Determine testing focus based on the project's current phase (MVP / Growth)

| Priority | Type | Scope |
|--------|------|------|
| **P0** | [Type] | [Scope] |
| **P1** | [Type] | [Scope] |
| **P2** | [Type] | [Scope] |

### 10.3 Test File Location

```
[Show the location relationship between test files and files under test]
```

---

## 11. Dependency Management

### 11.1 Installation Standards

```bash
# Correct
[correct installation command]

# Prohibited
[prohibited installation command]
```

### 11.2 Dependency Review

- [Evaluation criteria before introducing new dependencies]
- [Preference principles for selecting dependencies]

### 11.3 Version Locking

- [Whether lock files are committed]
- [Upgrade strategy]

---

## 12. Environment Variable Standards

### 12.1 Naming Rules

| Prefix | Exposure Scope | Example |
|------|---------|------|
| [Prefix 1] | [Scope] | [Example] |
| [Prefix 2 or no prefix] | [Scope] | [Example] |

### 12.2 File Management

| File | Purpose | Git Tracked |
|------|------|----------|
| [File 1] | [Purpose] | Yes / No |
| [File 2] | [Purpose] | Yes / No |

### 12.3 Security Red Lines

- **Absolutely prohibited** to expose [sensitive key type] to the client
- When adding new environment variables, **must synchronously update** [template file]
- No keys or passwords may be hardcoded in the code

---

## 13. AI Collaboration Protocol

> This section defines the rules that must be followed during AI-assisted development, ensuring AI-generated code is consistent with human-written code.

### 13.1 Must-Read Before AI Writes Code

| Document | Purpose |
|------|------|
| [Document path 1] | [Reading purpose] |
| [Document path 2] | [Reading purpose] |
| [Document path 3] | [Reading purpose] |
| [Document path 4] | [Reading purpose] |
| Existing code of related modules | Understand current implementation, maintain consistency |

### 13.2 Rules for AI Writing Code

| Rule | Description |
|------|------|
| **Read before write** | Must read the file before modifying it |
| **Minimal changes** | Only modify what the task requires; no "drive-by optimizations" |
| **Don't guess versions** | Use the package manager to get the latest version when installing dependencies; don't hardcode version numbers |
| **Don't introduce new dependencies** | Unless explicitly required by the task |
| **Don't write meaningless comments** | Don't write comments that restate the code |
| **Don't create unnecessary files** | Don't proactively create documentation or config files |
| **Follow existing patterns** | Code of the same type must follow the patterns of existing files |
| **Commit message standards** | Strictly follow Conventional Commits |

### 13.3 Must-Do After AI Finishes Writing Code

| Step | Action |
|------|------|
| **1. Type check** | Confirm no compilation errors |
| **2. Lint check** | Confirm no Lint errors |
| **3. Dependency direction** | Confirm no violation of dependency direction principles in the directory structure |
| **4. Environment variables** | If new ones are added, synchronously update the template file |

### 13.4 Mistake Log Mechanism

When AI-generated code has issues, record in [mistake log file path]:

| Record Item | Description |
|--------|------|
| **Error type** | Type error / Logic error / Standards violation / Dependency error |
| **Error description** | What exactly went wrong |
| **Root cause analysis** | Why this mistake was made |
| **Correct approach** | What to do next time |

---

## 14. Directory Dependency Direction (Quick Reference)

```
[Use ASCII diagram to show legal dependency directions between modules]

Prohibited directions:
  [ModuleA] ✗→ [ModuleB]
  [ModuleC] ✗→ [ModuleD]
```

> Detailed rules see [Project Structure document path]

---

## 15. Secure Coding Standards

| Category | Rule |
|------|------|
| **Input validation** | [Rule] |
| **Injection prevention** | [Rule] |
| **XSS** | [Rule] |
| **Key management** | [Rule] |
| **File upload** | [Rule] |
| **Authentication check** | [Rule] |
