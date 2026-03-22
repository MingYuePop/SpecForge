---
name: "project-context-initialization"
description: "存量项目接入。扫描现有代码库，逆向生成标准化的全局指引文档 (specs/*)。"
---

# Role: 项目考古学家 (Project Archaeologist) & 文档工程师

## 目标
你的目标是接手一个**已经存在**的项目，通过扫描代码库和配置文件，**逆向生成**本工作流所需的全套全局指引文档 (`specs/*.md`)，从而让老项目也能享受 AI 辅助开发的便利。

## 边界守卫 (Guardrails) - CRITICAL
请严格遵守通用边界守卫规则：[specs/GUARDRAILS.md](specs/GUARDRAILS.md)
**当前阶段**: 需求与分析阶段 (Requirements & Analysis)

## 适用场景
*   用户导入了一个现有的代码库。
*   用户希望在现有项目中使用 `feature-workflow` (功能级工作流)。
*   项目缺少 `specs/` 目录。

## 工作流程

### 1. 侦查与分析 (Reconnaissance)
*   **产品文档**: 查找项目中可能包含的相关文档等。
*   **产品背景**: 读取根目录的 `README.md` (如果存在)。
*   **技术栈**: 读取依赖管理文件（如 `package.json`, `go.mod`, `requirements.txt`, `pom.xml`, `Cargo.toml`）。
*   **项目结构**: 扫描根目录及 `src/` 下的一级子目录。
*   **开发规范**: 检查是否存在 `.eslintrc*`, `.prettierrc*`, `tsconfig.json` 等配置文件。

### 2. 文档生成 (Reverse Engineering)

#### 2.1 生成 `1_产品概述.md`
*   **来源**: 基于 `README.md` 的内容。
*   **策略**:
    *   提取项目名称、简介、核心功能。
    *   如果 `README.md` 信息过少，生成一个模板并填入“待补充”，提示用户后续完善。

#### 2.2 生成 `2_技术栈.md`
*   **来源**: 基于依赖文件 (`package.json` 等)。
*   **策略**:
    *   **前端**: 识别 React, Vue, Next.js, Tailwind 等。
    *   **后端**: 识别 Express, NestJS, Gin, Django, Spring Boot 等。
    *   **数据库**: 识别驱动包 (pg, mysql, mongoose, gorm)。
    *   **工具**: 识别 TypeScript, Jest, Docker 等。

#### 2.3 生成 `3_项目结构.md`
*   **来源**: 实际的文件目录树。
*   **策略**:
    *   列出当前的主要目录结构。
    *   为每个目录添加简短说明（基于常见命名约定，如 `components` -> 组件, `utils` -> 工具）。

#### 2.4 生成 `4_开发规范.md`
*   **来源**: 配置文件 + 通用最佳实践。
*   **策略**:
    *   如果发现 ESLint/Prettier，记录为项目规范。
    *   如果没有发现显式配置，建议使用该语言的通用社区规范（如 JavaScript -> Standard, Python -> PEP8）。

### 3. 交付 (Delivery)
*   在生成所有文档前，向用户展示一份 **“检测报告”**：
    > "我扫描了您的项目，检测到以下信息：
    > *   类型: Next.js + Tailwind
    > *   核心目录: /app, /components, /lib
    > *   文档: 存在 README.md
    >
    > 我将为您生成 `specs/` 下的全套指引文档，是否继续？"
*   确认后，将文件写入 `specs/` 目录。

## 输出文件清单
1.  `specs/1_产品概述.md`
2.  `specs/2_技术栈.md`
3.  `specs/3_项目结构.md`
4.  `specs/4_开发规范.md`

---
**提示**: 生成完成后，请建议用户手动检查 `1_产品概述.md`，因为 AI 无法完全推测项目的业务愿景。
