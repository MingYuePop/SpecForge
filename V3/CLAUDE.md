# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一套 AI 辅助软件开发工作流系统，通过结构化的 Skill（技能）引导 AI 完成从需求到实现的全过程。灵感来自 Kiro Spec 模式，适用于 Trae/Kiro 等 AI IDE。所有内容使用中文。

核心理念：**文档驱动开发 + TDD** — 每个阶段产出文档，文档是后续阶段的输入，确保可追溯性和一致性。编码实现阶段强制使用 TDD（测试驱动开发），按 Red-Green-Refactor 循环执行每个任务。

## 架构：三层 Skill 体系

### 项目级（启动时用一次）— `skills/project/`
执行顺序固定，每个 Skill 的输出是下一个的输入：
```
project-requirements-clarification → project-product-overview → project-tech-stack
→ project-structure → project-dev-standards → project-roadmap-planning → project-initialization
```
产出物保存在目标项目的 `specs/` 目录（产品概述.md、技术栈.md、项目结构.md、开发规范.md、开发路线图.md）。

### 功能级（反复使用）— `skills/feature/`
```
feature-requirements-clarification → feature-tech-design → feature-task-planning → feature-implementation
```
迭代路径（已完成功能的增量修改）：
```
feature-evolution → feature-implementation
```
产出物保存在 `specs/features/` 目录，命名模式：`{功能名}.md`、`{功能名}_技术方案.md`、`{功能名}_任务规划.md`、`{功能名}_变更任务_{CR序号}.md`。

### 通用级 — `skills/`（根目录）
- `bugfix-workflow`：强制 复现→定位→修复→单元测试→验证→报告 闭环

## Skill 文件结构

```
skills/
├── project/          # 项目级技能
│   ├── project-requirements-clarification/
│   ├── project-product-overview/
│   ├── project-tech-stack/
│   ├── project-structure/
│   ├── project-dev-standards/
│   ├── project-roadmap-planning/
│   └── project-initialization/
├── feature/          # 功能级技能
│   ├── feature-requirements-clarification/
│   ├── feature-tech-design/
│   ├── feature-task-planning/
│   ├── feature-implementation/
│   ├── feature-evolution/
│   └── feature-auto-pipeline/
├── bugfix-workflow/   # 通用级技能
├── docs-update/
└── prompt-master/
```

每个 Skill 目录包含：
- `SKILL.md`：主定义文件（frontmatter 含 name/description + 角色定义 + 工作流程 + 输出模板 + 交互准则 + 边界规则）
- `assets/`：输出模板文件（Markdown 模板，Skill 执行时读取并填充）

## 核心机制

### 边界守卫 (`specs/GUARDRAILS.md`)
严禁 AI 越过当前 Skill 职责范围。非编码阶段的 Skill 禁止输出代码，非规划阶段的 Skill 禁止修改文档。每个 SKILL.md 都声明了 `当前阶段` 来约束行为。

### 项目上下文协议 (`specs/PROJECT-CONTEXT.md`)
强制 AI 在执行任何 Skill 前先读取 `specs/` 目录下的所有文档，建立项目认知。每个 SKILL.md 开头都引用此协议。

### 通用 Agent 规则 (`通用Agent.md`)
所有 AI 必须遵守的基本行为准则：中文交流、确认优先（禁止直接开干）、文档与代码同步、强制使用最新文档、代码复用优先。

## 修改 Skill 时的注意事项

- 每个 SKILL.md 必须包含：frontmatter（name/description）、项目上下文协议引用、边界守卫引用、输出模板引用
- Skill 之间通过 `specs/` 目录下的文档传递上下文，修改产出物路径会影响下游 Skill
- `assets/` 中的模板是 Skill 的输出格式定义，修改模板会影响所有使用该 Skill 生成的文档
- 变更分类（Tweak/Extension/Refactor）定义在 `feature-evolution` 中，影响文档更新策略
