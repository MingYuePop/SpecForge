# {{Feature Name}} — Technical Design Document

## 1. Design Summary

**Feature description**: {{One-sentence description}}

**Impact scope**: {{Modules involved, e.g., user module, permission module, order module}}

**Technical challenges**: {{Key technical challenges; write "None" if there are none}}

**External dependencies**: {{Whether it depends on other features or external services; write "None" if there are none}}

---

## 2. Architecture Overview

> Choose the appropriate description method based on feature complexity:
>
> **Simple features** (single module, single API CRUD): 2-3 sentences explaining "who calls whom and where the data goes" is sufficient; no diagram needed.
>
> **Medium features** (cross 2-3 modules): A paragraph describing module interaction + one Mermaid sequence diagram showing the key chain.
>
> **Complex features** (cross-module, involving async/state machines/external services): Module responsibility table + Mermaid sequence diagram + data flow description; split into multiple diagrams if necessary.

{{Architecture description}}

---

## 3. Database Design

### New Tables

#### `{{table_name}}`

**Purpose**: {{Business meaning}}

| Field Name    | Type       | Constraints                | Description |
| ---------- | --------- | ------------------------- | ----------- |
| id         | BIGINT    | PK, AUTO_INCREMENT        | Primary key |
| {{field}}  | {{type}}  | {{constraints}}           | {{description}} |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Created time |

**Indexes**: {{Index design and reasoning}}

```sql
-- Table creation statement
{{SQL}}
```

### Modifying Existing Tables (if any)

#### `{{existing_table}}`

**Change details**: {{What was changed and why}}

```sql
{{Alter SQL}}
```

**Data migration**: {{Whether a migration script is needed; write "No migration needed" if not}}

---

## 4. API Design

> Follow the project's existing API style. The exception handling for each endpoint is written directly in the endpoint details; it does not get its own section.

### `{{METHOD}} {{/path}}`

**Description**: {{Endpoint functionality}} → AC-{{XXX}}

**Authentication**: {{Whether login/permissions are required}}

**Request**:
```json
{{Request body}}
```

**Response (success)**:
```json
{{Response body}}
```

**Error responses**:

| Scenario | Status Code | Response | Related AC |
|------|--------|------|---------|
| {{Parameter validation failed}} | 400 | {{Error message}} | AC-{{XXX}} |
| {{Insufficient permissions}} | 403 | {{Error message}} | AC-{{XXX}} |

---

{{Continue with more endpoints using the format above}}

---

## 5. Core Logic

> Describe key business logic that cannot be inferred from the API definition alone. Simple CRUD does not need this section.

### {{Logic name}} → AC-{{XXX}}

**Trigger condition**: {{When it executes}}

**Processing flow**:
1. {{Step 1}}
2. {{Step 2}}
3. {{Step 3}}

**Pseudocode** (only for complex logic):
```
{{Pseudocode}}
```

**State transitions** (if applicable):
```mermaid
stateDiagram-v2
    {{State diagram}}
```

---

## 6. Existing Code Changes

> Which existing code will this design touch? What is the reason for each change?

| Module / File | Change | Reason | Related AC |
|-------------|---------|------|---------|
| {{Module name}} | {{What was changed}} | {{Why it was changed}} | AC-{{XXX}} |

---

## 7. Technical Decisions

> Only record choices that were **genuinely deliberated**. Judgment criteria: if another approach also makes sense and a different person might choose it, then it's worth recording. Conversely, if the choice is obvious (using the project's existing tech stack, following existing design patterns), it doesn't need to be recorded.
>
> If this design has no decisions that required trade-offs, delete the entire Section 7.

### {{Decision topic}}

**Background**: {{What problem was encountered and why a choice was needed}}

**Options**:
- A: {{Option A}} — {{Advantages and costs}}
- B: {{Option B}} — {{Advantages and costs}}

**Conclusion**: {{Which one was chosen, with a one-sentence explanation of the core reason}}

---

## 8. Security & Performance (as needed)

> The following items should only be written when the feature actually involves them. Skip items that don't apply; don't write "None" as a placeholder.

**Input validation**: {{If there is additional validation logic beyond basic API layer validation}}

**Caching strategy**: {{If caching is introduced}}

**Rate limiting strategy**: {{If rate limiting is needed}}

**Sensitive data handling**: {{If passwords, payments, personal information, etc. are involved}}

**Performance considerations**: {{If there are explicit performance requirements or potential bottlenecks}}

---

## 9. AC Coverage Summary

> Final check: Does every AC have a place? This is the only AC mapping summary in the entire document; other sections use inline `→ AC-XXX` annotations.

| AC ID | Acceptance Criteria Summary | Implementation Location |
|---------|-------------|---------|
| AC-001 | {{Summary}} | {{e.g., API POST /api/upload + frontend validation}} |
| AC-002 | {{Summary}} | {{e.g., Core logic 5.1 + Error response 4.2}} |

---

## Appendix: Change Log

| Date | Change | Reason |
|------|---------|------|
| {{YYYY-MM-DD}} | Initial version | — |
