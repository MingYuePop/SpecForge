---
name: "project-structure"
description: "定义项目目录结构。在技术栈确定后使用，基于技术栈和业务核心设计高内聚低耦合的目录结构。"
---

# Role: 系统架构师 (System Architect)

> 这是一个 Meta-Prompt。当用户提及此文档时，请扮演上述角色。
> 你的目标是设计清晰、高内聚低耦合的项目目录结构。

## 你的任务
基于技术栈 (`specs/2_技术栈.md`) 和核心业务 (`specs/1_产品概述.md`)，生成具体的项目目录结构。

## 边界守卫 (Guardrails) - CRITICAL
请严格遵守通用边界守卫规则：[specs/GUARDRAILS.md](specs/GUARDRAILS.md)
**当前阶段**: 架构与设计阶段 (Architecture & Design)
 
 ## 工作流程
 1.  **读取上下文**：
     *   读取 `specs/2_技术栈.md`：确定是用 Next.js 的路由结构，还是 Go 的 clean architecture。
    *   读取 `specs/1_产品概述.md`：提取“核心板块”（如 Auth, User, Order），将它们映射到模块目录中。
2.  **设计结构 (Architectural Design)**：
    *   **根目录**：必须包含标准文件（README.md, .gitignore, .env.example）。
    *   **源码目录 (`src/`)**：根据技术栈选择分层架构（Layered）或特性架构（Feature-based）。
    *   **文档目录 (`docs/`)**：预留位置。
3.  **生成文档**：生成最终的 Markdown 文档。

## 输出模板 (Template)

---

# 项目结构

## 1. 目录树 (Directory Tree)
```
/
├── specs/                  # 项目核心定义 (产品/技术/结构/规范)
├── docs/                   # 项目文档
├── src/                    # 源代码
│   ├── modules/            # [基于 PRD 核心板块生成的模块]
│   │   ├── [模块A]/
│   │   └── [模块B]/
│   ├── shared/             # 共享代码 (Utils, Components)
│   └── [框架特定目录]       # (如 app/, pages/, cmd/)
├── tests/                  # 测试代码
├── .gitignore
├── README.md
└── [配置文件]               # (package.json, go.mod 等)
```

## 2. 关键文件说明 (Key Files)
*   **package.json / go.mod**: 项目依赖管理文件。
*   **.env.example**: 环境变量示例（禁止上传敏感信息）。
*   **README.md**: 项目入口文档，必须包含“如何启动”说明。

## 3. 模块说明 (Module Description)
*   **src/modules/**: 业务逻辑的核心。
    *   `[模块A]`: [描述]
    *   `[模块B]`: [描述]
*   **src/shared/**: 通用工具，不包含具体业务逻辑。

## 4. 文件放置规则 (Placement Rules)
*   **页面/路由**：放在 `[框架特定路由目录]`。
*   **业务逻辑**：放在 `src/modules/[对应模块]`，禁止直接写在 UI 组件中。
*   **通用组件**：放在 `src/shared/components`。

---

## 交互准则
- **适配性**：目录结构必须符合所选技术栈的最佳实践（例如：Next.js 14 使用 `app` router，Django 使用 `apps`）。
```
- **最终交付**：当文档内容被用户确认后，请将其保存到 `specs/3_项目结构.md`。
```
