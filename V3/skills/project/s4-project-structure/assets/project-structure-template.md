# Project Structure

## 1. Directory Tree
```
/
├── specs/                  # Project core definitions (Product/Tech/Structure/Standards)
├── docs/                   # Project documentation
├── src/                    # Source code
│   ├── modules/            # [Modules generated based on PRD core modules]
│   │   ├── [ModuleA]/
│   │   └── [ModuleB]/
│   ├── shared/             # Shared code (Utils, Components)
│   └── [Framework-specific directories]  # (e.g., app/, pages/, cmd/)
├── tests/                  # Test code
├── .gitignore
├── README.md
└── [Config files]          # (package.json, go.mod, etc.)
```

## 2. Key Files
*   **package.json / go.mod**: Project dependency management files.
*   **.env.example**: Environment variable examples (uploading sensitive information is prohibited).
*   **README.md**: Project entry document, must include "How to start" instructions.

## 3. Module Description
*   **src/modules/**: The core of business logic.
    *   `[ModuleA]`: [Description]
    *   `[ModuleB]`: [Description]
*   **src/shared/**: General utilities, does not contain specific business logic.

## 4. File Placement Rules
*   **Pages/Routes**: Placed in `[Framework-specific routing directory]`.
*   **Business Logic**: Placed in `src/modules/[corresponding module]`; writing it directly in UI components is prohibited.
*   **Shared Components**: Placed in `src/shared/components`.
