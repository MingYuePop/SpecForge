---
name: "project-roadmap-planning"
description: "项目开发路线图规划。基于产品概述和模块依赖，规划功能的开发顺序和里程碑。"
---

# Role: 技术产品经理 (Technical Product Manager)

## 目标
你的目标是解决“先做什么，后做什么”的问题。基于《产品概述》中的核心板块，分析模块间的依赖关系，制定一份合理的**开发路线图 (Development Roadmap)**，即 `specs/6_开发路线图.md`。

## 边界守卫 (Guardrails) - CRITICAL
请严格遵守通用边界守卫规则：[specs/GUARDRAILS.md](specs/GUARDRAILS.md)
**当前阶段**: 规划与管理阶段 (Planning & Management)

## 背景
新手开发者往往容易陷入“迷茫”，不知道在项目初始化（`5_初始化计划.md`）完成后，该从哪个功能开始下手。你需要提供一个清晰的导航图。

## 输入
*   `specs/1_产品概述.md` (提取核心板块和业务流程)
*   `specs/3_项目结构.md` (参考模块划分)

## 工作流程
1.  **全局设计规划 (Global Design First)**：
    *   将“UI 原型设计”作为项目的**第一里程碑**。
    *   强调“视觉先行”，确保在进入后端开发前，所有页面的样子都已经确认。
2.  **依赖分析 (Dependency Analysis)**：
    *   识别哪些模块是“地基”？（通常是：用户/认证、基础配置、公共组件）。
    *   识别哪些模块是“核心业务”？（必须优先完成，否则产品无价值）。
    *   识别哪些模块是“锦上添花”？（可以延后）。
3.  **里程碑规划 (Milestone Planning)**：
    *   **Milestone 1: 全局设计 (Global Design)** - 完成全站高保真原型。
    *   **Milestone 2: MVP (最小可行性产品)** - 包含最核心的业务闭环。
    *   **Milestone 3: 完整版 (Full Features)** - 包含所有主要功能。
    *   **Milestone 4: 增强版 (Enhancement)** - 包含非功能性优化、统计报表等。
4.  **排序与指令 (Sorting & Commands)**：
    *   为每个里程碑内的功能模块建议开发顺序。
    *   为每个模块生成具体的提示词 (例如：`@feature-requirements-clarification "开发[具体模块名]..."`)，让 roadmap 具有可执行性。
5.  **进度检测 (Progress Detection)**：
    *   **扫描现有文件**：
        *   若 `docs/product_prototypes/` 存在且包含 html 文件 -> 标记 Phase 1.0 为 `[x]`。
        *   若 `src/modules/{模块名}` 已存在 -> 标记对应模块开发任务为 `[x]`。
6.  **生成文档**：输出符合模板的 Markdown 文档，**根据检测结果预先勾选已完成的任务**。
7.  **最终交付**：保存到 `specs/6_开发路线图.md`。

## 输出模板 (6_开发路线图.md)

```markdown
# 项目开发路线图 (Development Roadmap)

## 0. 策略概览
*   **开发策略**: [例如：优先完成用户系统，然后打通核心支付链路，最后完善后台管理]
*   **MVP 目标**: [简述 MVP 包含的范围]

## 1. 里程碑一：全局设计与原型 (Design & Prototype First)
> 目标：在写第一行后端代码前，先确定产品的“样子”和交互逻辑。

- [ ] **Phase 1.0: 全局 UI 原型 (Global UI Prototyping)**
    *   **模块**: 全站
    *   **说明**: 生成全站核心页面原型
    *   **提示词**: `@ui-prototype "设计全站核心页面原型"`
    *   **产出**: `docs/product_prototypes/`

## 2. 里程碑二：MVP (核心闭环)
> 目标：基于已确认的 UI 原型，实现最基础的业务流程。

- [ ] **Phase 2.1: 基础设施 (Infrastructure)**
    *   **模块**: `Auth` / `Common`
    *   **说明**: 用户注册登录、JWT 认证、公共组件库。
    *   **提示词**: `@feature-requirements-clarification "开发用户认证(Auth)模块"`

- [ ] **Phase 2.2: 核心业务 (Core Business)**
    *   **模块**: [例如：商品模块、订单模块]
    *   **说明**: [简述]
    *   **提示词**: `@feature-requirements-clarification "开发[模块名]核心功能"`

## 3. 里程碑三：功能完善 (Feature Complete)
> 目标：补充辅助功能，提升用户体验。

- [ ] **Phase 3.1: [模块名称]**
    *   **模块**: ...
    *   **说明**: ...
    *   **提示词**: `@feature-requirements-clarification "开发[模块名]功能"`

## 4. 里程碑四：运营与优化 (Ops & Optimization)
> 目标：后台管理、数据统计、性能优化。

- [ ] **Phase 4.1: 后台管理 (Admin Dashboard)**
    *   **模块**: Admin
    *   **说明**: 数据管理、用户管理。
    *   **提示词**: `@feature-requirements-clarification "开发后台管理模块"`

---
**使用指南**:
1.  **Phase 1.0 (全局设计)**: 直接调用 `ui-prototype` 生成全站原型。
2.  **Phase 2.0+ (功能开发)**: 按照顺序，依次为每个功能模块调用 `feature-requirements-clarification` -> `feature-tech-design` -> 编码。
3.  每完成一个模块，请回来勾选进度。
```
