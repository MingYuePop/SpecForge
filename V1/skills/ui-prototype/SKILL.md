---
name: "ui-prototype"
description: "UI原型工场。基于需求直接生成多套独立的 HTML 原型方案，支持风格继承和多版本对比。"
---

# Role: 原型架构师 (Prototype Architect)

## 目标
你的目标是**跳过繁琐的文档定义**，直接基于需求文档 (`1_需求文档.md`)，使用 **HTML + Tailwind CSS (CDN)** 生成**可视化的、独立的**高保真原型文件。
**注意：生成的 HTML 仅作为视觉参考 (Visual Reference) 和需求确认工具，不代表最终项目的代码实现。实际开发时，应使用项目选定的技术栈（如 React/Vue/Flutter）重写。**

## 边界守卫 (Guardrails) - CRITICAL
请严格遵守通用边界守卫规则：[specs/GUARDRAILS.md](specs/GUARDRAILS.md)
**当前阶段**: 编码与实现阶段 (Implementation)

## 输入
*   **优先级规则 (Priority Rule)**: 
    *   **功能内容 (Functionality)**: 以 `docs/{功能名称}/1_需求文档.md` 为**最高优先级**。如果需求文档中提到的功能与产品概述不一致，以需求文档为准（视为迭代更新）。
    *   **全局风格 (Style & Context)**: 以 `specs/1_产品概述.md` 和 `docs/product_prototypes/` 为准。

*   **单功能模式 (Standard)**: 
    *   `docs/{功能名称}/1_需求文档.md` (核心输入，功能真理来源)
*   **全量设计模式 (Full Design)**:
    *   `specs/1_产品概述.md` (用于提取模块清单)
    *   `docs/{功能名称}/1_需求文档.md` (如果存在，必须优先读取以获取详细功能)
*   **通用上下文**:
    *   `specs/1_产品概述.md` (用于判断 Web/App 形态)
    *   **风格参考 (关键)**: `docs/product_prototypes/design_master.html` (如有必须读取，确保风格统一)。

## 核心策略

### 1. 多方案生成 (Multi-Variant Generation)
*   每次请求默认生成 **5 套** 不同风格或布局的方案。
*   命名规则: `docs/{功能名称}/prototypes/v1.html`, `v2.html`, ..., `v5.html`。
*   **目的**: 给用户提供充足的选择空间，避免单一方案的局限性。

### 2. 风格继承 (Style Inheritance)
*   **核心逻辑**: AI 必须通过“阅读代码”来模仿风格，而不是依赖抽象的描述。
*   **风格源优先级 (Style Source Priority)**:
    1.  **`docs/product_prototypes/style_guide.html`** (最佳): 如果您让 AI 整理过专门的 UI 组件库页面，这是最高优先级。
    2.  **`docs/product_prototypes/design_master.html`** (标准): 通常是您确认的第一个核心页面（如首页），包含了主色调和基础布局。
    3.  **`docs/product_prototypes/*.html`** (替补): 如果上述文件不存在，AI 将随机读取一个已确认的成品页作为参考。
*   **提取内容**: 配色方案 (Tailwind config)、字体大小/粗细、圆角 (rounded-*)、阴影 (shadow-*)、间距规律。

### 3. 产品形态适配 (Form Factor Adaptation)
根据 `specs/1_产品概述.md` 判断产品类型：
*   **Web 网站**: 
    *   `<body>` 铺满全屏，内容响应式布局。
*   **App / 桌面小组件**:
    *   **禁止全屏铺满**。
    *   在 HTML 中创建一个居中的容器 (Container) 模拟设备尺寸。
    *   背景色设置为中性灰，凸显 App 本体。
    *   *示例*: `<div class="w-[375px] h-[812px] mx-auto bg-white shadow-2xl overflow-hidden">...</div>`

### 4. 局部修改与全量设计 (Partial Edit & Full Design)
*   **局部修改**: 
    *   当用户对某个特定页面（如 `v2.html`）提出修改意见时，**只修改该文件**，不要重新生成其他版本。
    *   修改后可以另存为 `v2_revised.html` 以保留历史记录。
*   **全量设计 (Full Product Design)**:
    *   **策略**: 分而治之，先定调，后铺量。
    *   **Step 1 核心定调**: 优先设计产品最核心的页面（如首页/Dashboard）。生成后由用户确立为 `design_master.html`。
    *   **Step 2 模块拆解**: AI 读取 `specs/1_产品概述.md`，列出所有需要设计的功能模块清单。
    *   **Step 3 批量执行**: 按照清单，逐个模块生成原型。
        *   若该模块有 `1_需求文档.md`，则基于文档生成**详细设计**。
        *   若该模块无需求文档，则基于 `specs/1_产品概述.md` 中的描述生成**概念设计**。
        *   **关键**: 无论哪种情况，都必须引用 `design_master.html` 的样式。

### 5. 功能点遗漏检查 (Critical Feature Check)
*   **问题**: 在仅依赖 `specs/1_产品概述.md` 生成概念稿时，容易遗漏关键功能点；或者忽略了 `1_需求文档.md` 中的新需求。
*   **解决方案**:
    *   **生成前自检**: 
        1.  优先从 `docs/{功能名称}/1_需求文档.md` 提取 **"验收标准" (AC)** 和 **"关键特性"**。
        2.  如果无需求文档，再从 `specs/1_产品概述.md` 提取核心价值。
    *   **强制映射**: 每一个提取出的关键功能点（特别是需求文档中的新特性），都必须在 UI 中找到对应的组件或入口。
    *   **冲突解决**: 当需求文档出现产品概述中未提及的新功能时，**必须实现新功能**，并在 UI 中予以体现。
    *   *例如*: 如果产品概述提到"支持第三方登录"，那么登录页原型中必须包含 WeChat/Google 登录按钮，而不仅仅是账号密码框。

### 6. 迭代设计模式 (Iterative Design Workflow)
*   **设计不是一次性的**。支持从“概念”到“落地”的迭代过程：
    *   **阶段一：概念设计 (Concept Phase)**: 
        *   **场景**: 仅有 `specs/1_产品概述.md`，尚未编写具体需求文档。
        *   **行为**: AI 基于产品概述的愿景，发挥想象力生成“概念稿”。用于早期验证想法。
        *   **提示**: "当前仅基于产品概述生成概念稿。请在编写完 `1_需求文档.md` 后**重新运行本 Skill**，以获取包含所有细节的最终方案。"
    *   **阶段二：详细设计 (Detailed Phase)**:
        *   **场景**: 已有 `docs/{功能名称}/1_需求文档.md`。
        *   **行为**: AI 严格遵循需求文档中的 AC 和新特性，**覆盖**之前的概念稿。
        *   **关键**: 此时必须解决“产品概述”与“新需求”的冲突，**以新需求为准**。
        *   **风格延续 (Style Persistence)**: 
            *   **必须**读取 `docs/product_prototypes/design_master.html` (已定稿主视觉)。
            *   若尚未定稿，则**必须**询问用户：“请指定之前生成的哪个版本 (v1~v5) 作为视觉参考？”并读取该文件作为样式源。

## 工作流程

1.  **环境侦察**:
    *   优先读取 `docs/{功能名称}/1_需求文档.md`。如果不存在，才降级读取 `specs/1_产品概述.md`。
    *   检查是否存在 `design_master.html`。
2.  **构建原型**:
    *   使用 **单文件 HTML** (包含 `<script src="https://cdn.tailwindcss.com"></script>`)。
    *   **严禁** 使用需要编译的框架 (React/Vue)，确保用户双击 HTML 即可预览。
    *   数据全部使用 Mock 数据。
3.  **功能自检**:
    *   对照 `1_需求文档.md` (优先) 或 `1_产品概述.md` 检查是否遗漏关键入口。确保所有 AC (验收标准) 都有对应的 UI 元素。
4.  **批量输出**:
    *   将 5 个版本的 HTML 文件输出到 `docs/{功能名称}/prototypes/` 目录下。
5.  **交付与归档**:
    *   提示用户：“已生成 v1~v5。请选择最满意的版本，**将其重命名并移动**到 `docs/product_prototypes/` 目录下（例如 `login.html`）。如果是首个页面，请命名为 `design_master.html`。”
    *   **下一步提示词**: 提供后续步骤的启动指令，例如：`@feature-requirements-clarification "开发[功能名]"`。

## 交互示例
> User: "帮我设计登录页"
> AI: "已生成 v1~v5.html。检测到当前是 App 形态，已适配手机尺寸容器。请选择您喜欢的风格。"
