# {{Feature Name}} — {{Slice Name}} Completion Report

**Slice (phase)**: {{Slice name, named after user behavior, e.g., "Post comment", "Comment list"}}
**Completion time**: {{YYYY-MM-DD HH:mm}}
**Slice completion criteria**: {{What complete behavior the user can perform, e.g., "The user can enter a comment on the page and submit it, and see a success prompt"}}

---

## Completed Tasks

| Task | Tests | Acceptance Method | Status |
|------|------|---------|------|
| Task-{{XX}}: {{Title}} | {{N}} tests all passed | {{TDD / Manual acceptance}} | ✅ |
| Task-{{XX}}: {{Title}} | {{N}} tests all passed | {{TDD / Manual acceptance}} | ✅ |

---

## Manual Acceptance Summary (if applicable)

> Summary of manual acceptance results for tasks with UI changes in this slice. If this slice has no UI tasks, delete this section.

| Task | Acceptance Checklist | Result | Expectation Adjustments |
|------|---------|------|---------|
| Task-{{XX}} | `docs/acceptance-checklists/{{feature-name}}_Task-{{XX}}_checklist.md` | ✅ All passed | ⬜ None / ⬜ Yes |

**Expectation adjustments summary**: ⬜ None / ⬜ Yes → To be handled by feature-evolution later

---

## File Changes

### Added
- `{{path}}` — {{One-sentence description}}

### Modified
- `{{path}}` — {{What was changed}}

### Deleted (if applicable)
- `{{path}}` — {{Why it was deleted}}

---

## AC Coverage Progress

| AC ID | Status | Notes |
|---------|------|------|
| AC-{{XXX}} | ✅ Satisfied | Implemented and tested by Task-{{XX}} |
| AC-{{XXX}} | ⏳ Pending subsequent slice | Requires {{slice name}} to complete |

---

## Issues & Decisions (if applicable)

> Only record unexpected situations encountered during development, non-obvious decisions made, and matters that affect subsequent slices. If everything went smoothly, this section can say "None."

### {{Issue/Decision topic}}

**Situation**: {{What happened}}
**Handling**: {{How it was resolved}}
**Impact**: {{Impact on subsequent work; omit if none}}

---

## Technical Debt (if applicable)

> Optimizations intentionally skipped during development, temporary solutions, and known but temporarily unaddressed issues. Delete this section if there are none.

- {{Description}} — Recommended to address {{when}}
