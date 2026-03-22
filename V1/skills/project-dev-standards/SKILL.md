---
name: "project-dev-standards"
description: "制定代码规范和协作流程。在技术栈确定后使用，定义代码风格、命名约定、Git提交规范和AI交互协议。"
---

# Role: 技术委员会 (Tech Committee) & 质量保证专家 (QA)

> 这是一个 Meta-Prompt。当用户提及此文档时，请扮演上述角色。
> 你的目标是制定项目的“法律法规”，确保代码风格统一且可维护。

## 你的任务
基于已确定的技术栈 (`specs/2_技术栈.md`)，制定具体的开发规范。**必须动态适配选定的技术**（不要生成 Python 规范给 Go 项目）。

## 边界守卫 (Guardrails) - CRITICAL
请严格遵守通用边界守卫规则：[specs/GUARDRAILS.md](specs/GUARDRAILS.md)
**当前阶段**: 架构与设计阶段 (Architecture & Design)
 
 ## 工作流程
 1.  **读取上下文**：
     *   读取 `specs/2_技术栈.md`，确认核心语言和框架。
     *   读取 `specs/1_产品概述.md`，理解业务领域（如金融项目对精度的要求不同）。
    *   **全量规则扫描**：必须扫描 `specs/` 或 `specs/rules` 下的所有文档，确保不遗漏任何约束。
2.  **制定规范 (Dynamic Generation)**：
    *   **代码风格**：选择该语言社区最主流的规范（如 Python -> PEP8/Black, JS -> ESLint/Prettier）。
    *   **命名约定**：明确文件、类、变量的命名规则。
    *   **Git 提交**：强制使用 [Conventional Commits](https://www.conventionalcommits.org/)。
3.  **定义 AI 交互协议 (AI Protocol)**：
    *   **核心规则**：AI 在写代码前必须先阅读什么？写完代码后必须做什么？（如：`写代码前必读 AI错题本`）。
4.  **生成文档**：生成最终的 Markdown 文档。

## 输出模板 (Template)

---

# 开发规范

## 1. 代码风格 (Code Style)
*   **核心原则**：[例如：Explicit is better than implicit]
*   **格式化工具**：[例如：Prettier / Black / Gofmt]
*   **命名规范**：
    *   **文件**: [例如: snake_case / kebab-case]
    *   **类**: [例如: PascalCase]
    *   **变量/函数**: [例如: camelCase]

## 2. Git 提交规范 (Commit Convention)
我们遵循 **Conventional Commits** 规范：
*   格式：`<type>(<scope>): <subject>`
*   示例：`feat(auth): add login page`
*   **常用 Type**:
    *   `feat`: 新功能
    *   `fix`: 修补 bug
    *   `docs`: 文档修改
    *   `refactor`: 重构（即不是新增功能，也不是修改bug的代码变动）
    *   `chore`: 构建过程或辅助工具的变动

## 3. AI 交互协议 (AI Interaction Protocol)
*为了保证代码质量，AI 助手必须遵守以下协议：*
1.  **阅读优先**：在编写新代码前，必须先阅读相关文件的上下文，以及 `specs/` 下的所有全局规则文档。
2.  **错题本机制**：每次任务开始前，必须检查 `specs/7_AI错题本.md`，避免重复错误。
3.  **原子化提交与验证**：
    *   **步骤**：编写代码 -> 运行测试/预览 -> **确认无误** -> 提交。
    *   **禁止**：禁止在未经用户验证（或测试失败）的情况下直接提交代码。
4.  **自我审查**：代码生成后，必须进行一次 Self-Review，检查是否符合上述代码风格。

---

## 交互准则
- **严谨性**：规范必须具体、可执行，不能模棱两可。
- **最终交付**：当文档内容被用户确认后，请将其保存到 `specs/4_开发规范.md`。
