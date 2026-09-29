# {{Feature Name}} — Development Task Plan

## 1. Task Overview

**Total tasks**: {{N}}
**Estimated total effort**: {{X}} minutes (about {{Y}} hours)
**Development method**: TDD — each task follows the RED → GREEN → REFACTOR cycle

**Key markers**:
- 🔒 Blocking task: depended on by multiple tasks; recommended for early completion
- ⚠️ Risk task: high technical difficulty; may require additional time

### Dependency Graph

```mermaid
graph LR
    %% Generate based on actual tasks; mark blocking tasks (red) and risk tasks (orange)
    {{Dependency graph}}
```

### Parallelizable Task Groups

| Parallel Group | Tasks | Notes |
|--------|------|------|
| {{Group number}} | {{Task numbers}} | {{Why they can be parallelized}} |

---

## 2. Development Tasks

> Organized by vertical slice. Each phase corresponds to an independently runnable and verifiable user behavior (plus an optional infrastructure layer). Tasks within a slice are arranged in the natural technical order.
>
> Each task follows the TDD cycle: RED (write tests based on validation criteria) → GREEN (write minimal implementation to pass tests) → REFACTOR (refactor)

### {{Phase name (named after user behavior)}}

**Phase completion criteria**: {{After this slice is done, what complete behavior can the user perform}}

---

#### Task-{{XX}}: {{Task title}} {{🔒/⚠️ if applicable}}

**Plain-language explanation**: {{One sentence without technical terms describing what perceptible change the user or system will experience after completion}}

**What to do**: {{Specific work to be done}}

**Files involved**: `{{File path}}`

**Reference**: Technical solution {{Section}} → AC-{{XXX}}

**Dependencies**: {{Preceding task numbers; write "None" if there are none}}

**Estimated effort**: {{N}} minutes

**Validation criteria** (directly converted to test cases in the TDD RED phase):
- [ ] {{Specific input → expected output, directly writable as a test assertion}}
- [ ] {{Cover normal cases}}
- [ ] {{Cover boundary cases}}
- [ ] {{Cover exception cases}}

---

{{Continue with more tasks using the format above; add more phases as needed}}

---

## 3. AC Coverage Summary

> Final check: Does every AC have a task assigned to it? This is the only AC mapping summary in the entire document.

| AC ID | Acceptance Criteria Summary | Assigned Task | Verification Method |
|---------|-------------|---------|---------|
| AC-{{XXX}} | {{Summary}} | Task-{{XX}} | {{How to verify this AC is satisfied}} |

---

## 4. Definition of Done

> Final confirmation before overall feature delivery after all tasks are complete. Only list checklist items relevant to this feature; don't use generic checklists.

- [ ] All task validation criteria (test cases) pass
- [ ] The verification method for each AC in the AC coverage summary has been executed and passed
- [ ] {{Feature-specific checklist item, e.g., database migration script verified in test environment}}
- [ ] {{Feature-specific checklist item, e.g., real endpoint integration passed (if mock replacement is involved)}}
