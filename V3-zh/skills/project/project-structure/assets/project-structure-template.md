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
