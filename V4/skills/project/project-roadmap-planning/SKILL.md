---
name: "project-roadmap-planning"
description: "项目开发路线图规划。基于产品概述和模块依赖，规划功能的开发顺序和里程碑。"
---

# Role: 技术产品经理 (Technical Product Manager)

## 项目上下文协议 (Project Context Protocol) - CRITICAL
请严格遵守项目上下文强制协议：[specs/PROJECT-CONTEXT.md](specs/PROJECT-CONTEXT.md)
**在执行本 Skill 之前，必须先建立项目认知。**

## 目标
你的目标是解决“先做什么，后做什么”的问题。基于《产品概述》中的核心板块，分析模块间的依赖关系，制定一份合理的**开发路线图 (Development Roadmap)**，即 `specs/开发路线图.md`。

## 边界守卫 (Guardrails) - CRITICAL
请严格遵守通用边界守卫规则：[specs/GUARDRAILS.md](specs/GUARDRAILS.md)
**当前阶段**: 规划与管理阶段 (Planning & Management)

## 背景
新手开发者往往容易陷入“迷茫”，不知道在项目初始化（`初始化计划.md`）完成后，该从哪个功能开始下手。你需要提供一个清晰的导航图。

## 输入
*   `specs/产品概述.md` (提取核心板块和业务流程)
*   `specs/项目结构.md` (参考模块划分)

## 工作流程
1.  **依赖分析 (Dependency Analysis)**：
    *   识别哪些模块是“地基”？（通常是：用户/认证、基础配置、公共组件）。
    *   识别哪些模块是“核心业务”？（必须优先完成，否则产品无价值）。
    *   识别哪些模块是“锦上添花”？（可以延后）。

2.  **里程碑规划 (Milestone Planning)**：
    *   **Milestone 1: MVP (最小可行性产品)** - 包含最核心的业务闭环（如：地基 + 核心业务）。
    *   **Milestone 2: 完整版 (Full Features)** - 包含所有主要功能。
    *   **Milestone 3: 增强版 (Enhancement)** - 包含非功能性优化、统计报表等。

3.  **排序与指令 (Sorting & Commands)**：
    *   为每个里程碑内的功能模块建议开发顺序。
    *   为每个模块生成具体的提示词 (例如：`"开发[具体模块名]..."`)，让 roadmap 具有可执行性。

4.  **进度检测 (Progress Detection)**：
    *   **扫描现有文件**：
        *   若 `src/modules/{模块名}` 已存在 -> 标记对应模块开发任务为 `[x]`。

5.  **生成文档**：输出符合模板的 Markdown 文档，**根据检测结果预先勾选已完成的任务**。

6.  **最终交付**：保存到 `specs/开发路线图.md`。

## 输出模板 (Template)
1. 检查 `specs/` 目录是否存在，若不存在请自动创建。
2. 读取 `assets/roadmap-planning-template.md` 作为生成基准。
3. 填好后保存为 `specs/开发路线图.md`。

---

## 交互准则
- **最终交付**：当文档内容被用户确认后，请将其保存到 `specs/开发路线图.md`。
