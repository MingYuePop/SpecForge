# {{Feature Name}} — Change Record CR-{{Number}}

## 1. Change Overview

**Change title**: {{Brief description}}
**Change type**: {{Tweak / Extension / Refactor}}
**Change reason**: {{Why this change is being made}}
**Initiation date**: {{YYYY-MM-DD}}
**Related feature**: {{Original feature name}}

---

## 2. Impact Analysis

> Only list the affected parts. Unaffected areas do not need a "no impact" placeholder.

### Requirements Impact

| AC ID | Operation | Notes |
|---------|------|------|
| AC-{{new number}} | Added | {{New acceptance criteria summary}} |
| AC-{{existing number}} | Modified | {{Original content → new content}} |
| AC-{{existing number}} | Removed | {{Reason}} |

### Technical Impact

| Impact Area | Change Details |
|---------|---------|
| {{e.g., Database}} | {{e.g., Add avatar field to users table}} |
| {{e.g., API}} | {{e.g., Add PUT /api/users/avatar}} |
| {{e.g., Component}} | {{e.g., Modify UserProfile component to add avatar upload}} |

### Code & Test Impact

| File | Operation | Notes |
|------|------|------|
| `{{path}}` | {{Added/Modified}} | {{Specific changes}} |
| `{{test path}}` | {{Added/Modified/Needs adjustment}} | {{Test change description}} |

**Regression risk**: {{Which existing features may be affected; whether existing tests provide coverage}}

---

## 3. Change Details

### Added/Modified Acceptance Criteria

> Given-When-Then format, consistent with the requirements document.

- **AC-{{number}}**: {{Scenario name}}
  - **Given** {{precondition}}
  - **When** {{user action}}
  - **Then** {{expected result}}

### Technical Changes (if applicable)

> Only write the parts that changed: SQL for database changes, interface definitions for API changes, design notes for component changes. Skip areas with no changes.

{{Fill in based on actual change content; don't use a fixed "Database/API/Component" three-section template}}

### Compatibility Notes (if applicable)

> If the change may break existing data or interfaces, describe the migration plan. Delete this section if there are no compatibility issues.

{{Migration steps}}

---

## 4. Incremental Tasks

> Task numbers continue after the last number in the original task plan. Phases are divided based on actual change content; don't use a fixed structure.
>
> Each task follows the TDD cycle: RED → GREEN → REFACTOR

### {{Phase name}}

#### Task-{{N+X}}: {{Task title}}

**Plain-language explanation**: {{One sentence describing the perceptible change after completion}}

**What to do**: {{Specific content}}

**Files involved**: `{{path}}`

**Reference**: This document {{Section}} → AC-{{XXX}}

**Dependencies**: {{Preceding task numbers; write "None" if there are none}}

**Estimated effort**: {{N}} minutes

**Validation criteria** (TDD RED phase basis):
- [ ] {{Specific input → expected output}}
- [ ] {{Boundary/exception scenarios}}

---

{{Add more tasks and phases as needed}}

---

#### Task-{{last}}: Regression Verification

**What to do**: Run all existing tests to ensure the change hasn't broken existing functionality

**Dependencies**: All of the above incremental tasks

**Validation criteria**:
- [ ] All existing tests pass
- [ ] All newly added tests pass
- [ ] Test coverage has not decreased

---

## 5. AC Coverage Summary

| AC ID | Operation | Assigned Task | Verification Method |
|---------|------|---------|---------|
| AC-{{XXX}} | {{Added/Modified}} | Task-{{XX}} | {{How to verify}} |

---

## 6. Change Summary

**New task count**: {{N}}
**Estimated total effort**: {{X}} minutes (about {{Y}} hours)
**Risk level**: {{Low/Medium/High}} — {{Risk description; can be omitted for low risk}}
