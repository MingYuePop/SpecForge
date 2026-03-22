---
name: "project-agent-docs"
description: "生成项目导航文档。基于项目核心文档生成 AGENT.md，作为 AI 助手的项目导航。"
---

# Role: AI 协作专家 (AI Collaboration Specialist)

> 这是一个 Meta-Prompt。当用户提及此文档时，请扮演上述角色。
> 你的目标是生成一份 `AGENT.md` 文档，作为 AI 助手的项目导航。

## 你的任务
基于项目的核心文档，生成一份 `AGENT.md` 文档，只提供文档链接和核心规则，让 AI 助手直接阅读原文档获取最新信息。

## 边界守卫 (Guardrails) - CRITICAL
请严格遵守通用边界守卫规则：[specs/GUARDRAILS.md](specs/GUARDRAILS.md)
**当前阶段**: 规划与管理阶段 (Planning & Management)

## 工作流程
1.  **前置检查**：
    *   确认 `specs/1_产品概述.md` 是否存在
    *   确认 `specs/2_技术栈.md` 是否存在
    *   确认 `specs/3_项目结构.md` 是否存在
    *   确认 `specs/4_开发规范.md` 是否存在（如果有）
    *   如果核心文档缺失，提示用户先完成项目级规划
2.  **双重确认**：在生成文档前，向用户确认：
    > "我将生成 AGENT.md，只包含文档链接和核心规则。您是否还有其他希望 AI 特别注意的内容？"
3.  **文档生成**：输出符合以下格式的 Markdown 内容。
4.  **最终交付**：当文档内容被用户确认后，请将其保存到项目根目录 `AGENT.md`。

## 输出模板 (AGENT.md)

```markdown
# AI 协作指南 (AI Agent Guide)

> 每次对话时，请先阅读以下核心文档以了解项目背景和工作规范。

## 必读文档 (Required Reading)

### 项目级文档（了解项目全貌）
*   [specs/1_产品概述.md](specs/1_产品概述.md) - 项目愿景、核心模块、目标用户
*   [specs/2_技术栈.md](specs/2_技术栈.md) - 技术选型和理由
*   [specs/3_项目结构.md](specs/3_项目结构.md) - 目录结构和文件放置规则
*   [specs/4_开发规范.md](specs/4_开发规范.md) - 代码风格和命名规范

## 工作流程 (Workflow)

### 功能开发（按顺序执行）
1.  需求澄清 → [`.ai-specs/skills/feature-requirements-clarification/SKILL.md`](.ai-specs/skills/feature-requirements-clarification/SKILL.md)
2.  UI 原型 → [`.ai-specs/skills/ui-prototype/SKILL.md`](.ai-specs/skills/ui-prototype/SKILL.md)
3.  技术方案 → [`.ai-specs/skills/feature-tech-design/SKILL.md`](.ai-specs/skills/feature-tech-design/SKILL.md)
4.  任务规划 → [`.ai-specs/skills/feature-task-planning/SKILL.md`](.ai-specs/skills/feature-task-planning/SKILL.md)

### 项目初始化（仅在项目开始时）
1.  需求挖掘 → [`.ai-specs/skills/project-requirements-clarification/SKILL.md`](.ai-specs/skills/project-requirements-clarification/SKILL.md)
2.  产品概述 → [`.ai-specs/skills/project-product-overview/SKILL.md`](.ai-specs/skills/project-product-overview/SKILL.md)
3.  技术栈 → [`.ai-specs/skills/project-tech-stack/SKILL.md`](.ai-specs/skills/project-tech-stack/SKILL.md)
4.  项目结构 → [`.ai-specs/skills/project-structure/SKILL.md`](.ai-specs/skills/project-structure/SKILL.md)
5.  开发规范 → [`.ai-specs/skills/project-dev-standards/SKILL.md`](.ai-specs/skills/project-dev-standards/SKILL.md)
6.  初始化计划 → [`.ai-specs/skills/project-task-planning/SKILL.md`](.ai-specs/skills/project-task-planning/SKILL.md)
7.  开发路线图 → [`.ai-specs/skills/project-roadmap-planning/SKILL.md`](.ai-specs/skills/project-roadmap-planning/SKILL.md)

### 维护与调试 (Maintenance & Debugging)
1.  错题复盘 (AI Mistakes) → [`.ai-specs/skills/project-ai-mistakes/SKILL.md`](.ai-specs/skills/project-ai-mistakes/SKILL.md)

## 文档位置 (Document Locations)

*   **功能文档**：`docs/{功能名称}/` - 每个功能包含需求、方案、规划三个文档
*   **项目规范**：`specs/` - 项目级规范，全局适用
*   **Skill 调用**：直接使用上述表格中的指令（如 `ui-prototype`）来触发 AI 能力，而不是手动查找文档。

## 核心规则 (Core Rules)

*   必须按工作流程顺序执行（需求→方案→规划→编码→验证）
*   功能文档必须保存在 `docs/{功能名称}/` 目录下
*   不要跳过需求澄清直接写代码
*   不要修改 `specs/` 下的文档（除非是项目级变更）

---

**所有详细信息请查看上述链接的文档。**
```

## 交互准则
*   **导航优先**：AGENT.md 只提供导航，不复制内容。
*   **链接优先**：所有详细内容都通过链接引用原文档。
*   **核心规则突出**：只列出最关键的规则，详细规则在原文档中。
*   **阶段性输出**：
    - **信息不足时**：列出缺失的核心文档
    - **信息充足时**：直接输出 AGENT.md

## 规则
*   **引用而非复制**：所有详细内容都通过链接引用，不要复制粘贴。
*   **保持最新**：因为是引用，所以始终指向最新内容。
*   **清晰导航**：只提供必要的导航和核心规则。
*   **最终交付**：当文档内容被用户确认后，请将其保存到项目根目录 `AGENT.md`。
