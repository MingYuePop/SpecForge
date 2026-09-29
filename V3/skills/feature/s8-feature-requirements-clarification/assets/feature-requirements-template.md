# {{Feature Name}} — Feature Requirements Specification

## 1. Background & Value

**Why build it**: {{What problem does this feature solve? What is the user's current pain point?}}

**What it should achieve**: {{Describe the expected outcome of the feature in one sentence}}

**Related**: {{Related Issue / Roadmap Phase; delete this line if none}}

---

## 2. Scope

### Included This Time

- {{Feature point 1}}
- {{Feature point 2}}

### Not Included This Time

- {{Feature point A}} — {{Reason or plan, e.g., "Next phase" / "Decide after user feedback"}}
- {{Feature point B}} — {{Reason or plan}}

---

## 3. Users & Stories

**Roles involved**: {{Role A (e.g., regular user)}}, {{Role B (e.g., admin)}}

| ID | User Story | Related AC |
|------|---------|---------|
| US-001 | As a **{{role}}**, I want to **{{action}}** so that **{{value}}** | AC-001, AC-002 |
| US-002 | As a **{{role}}**, I want to **{{action}}** so that **{{value}}** | AC-003, AC-004 |

---

## 4. Requirements Details

### 4.1 Core Flow

> This section only describes the **global perspective of the main path** — where the user starts, what key nodes they pass through, and where they end up. The details of each node (inputs, validations, expected results) are carried by the AC and should not be elaborated here.

1. {{Step 1 — brief description}}
2. {{Step 2 — brief description}}
3. {{Step 3 — brief description}}

### 4.2 Interaction Rules

> Only record key interaction decisions that affect user experience. Pure visual details (colors, font sizes) do not belong here.

- {{e.g., Delete operations require a confirmation dialog}}
- {{e.g., Submit button is disabled after form submission to prevent duplicate submissions}}
- {{e.g., Input fields validate in real-time on blur and display error messages}}

### 4.3 Business Rules

> Hard constraints that must always be satisfied. Each rule has a corresponding AC in Section 5 to verify it.

| ID | Rule |
|------|------|
| BR-001 | {{e.g., Username must be 2-20 characters, allowing only letters, numbers, and underscores}} |
| BR-002 | {{e.g., Each person can post a maximum of 10 comments per day}} |

---

## 5. Acceptance Criteria

> AC are the core deliverable of this document. The subsequent technical solution, task breakdown, and TDD test cases are all derived from here.
>
> **Reading guide**:
> - Happy Path corresponds to the **specific expected behavior** of each key step in the flow in Section 4.1
> - Business Rules correspond to the **testable expression** of each rule in Section 4.3
> - The two have different perspectives: the flow and rules tell you "what it is," while the AC tell you "how to verify"

### 5.1 Happy Path

- [ ] **AC-001**: {{Scenario name}}
  - **Given** {{precondition}}
  - **When** {{user action}}
  - **Then** {{expected result — describe the change the user can see}}

- [ ] **AC-002**: {{Scenario name}}
  - **Given** {{precondition}}
  - **When** {{user action}}
  - **Then** {{expected result}}

### 5.2 Edge & Error Cases

- [ ] **AC-XXX**: {{Scenario name}}
  - **Given** {{precondition / error state}}
  - **When** {{user action}}
  - **Then** {{how the system responds, what the user sees}}

### 5.3 Business Rules Verification

- [ ] **AC-XXX**: {{Scenario name}} ← BR-{{XXX}}
  - **Given** {{precondition}}
  - **When** {{action that triggers the rule}}
  - **Then** {{observable result of the rule taking effect}}

---

## Appendix: Change Log

| Date | Change | Reason |
|------|---------|------|
| {{YYYY-MM-DD}} | Initial version | — |
