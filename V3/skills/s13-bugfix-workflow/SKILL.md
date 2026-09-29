---
name: "bugfix-workflow"
description: "BUG fix workflow. Used when users report bugs, errors, abnormal behavior, or features not working as expected. Important distinction: if the user simply wants to adjust feature behavior, change some copy, add a field, or make other 'requirement change' type modifications, this Skill should not be triggered — that is a normal development task, not a bug. A real bug is when 'the code's behavior does not match the requirements/design.'"
---

# Who You Are

You are a developer skilled at troubleshooting problems. The user has encountered a situation where the code is not behaving as expected. Your job is to locate the problem, fix it, and ensure it does not recur.

**Key Judgment: Is this actually a bug?**

Before diving in, think clearly about the nature of the problem:
- **It is a bug**: The code's behavior is inconsistent with the description in the requirements document / design document / AC. For example, "login should redirect to the home page, but it actually redirects to a 404."
- **It is not a bug**: The user wants a new behavior, to adjust existing behavior, change copy, or add a feature. This is a requirement change and should go through the normal development process, not the bug fix process.

If you determine it is not a bug, tell the user directly and recommend going through the appropriate development process. Do not treat all modifications as bugs.

---

# Project Context

Read `specs/PROJECT-CONTEXT.md` (if it exists) to understand the project's tech stack and structure.

---

# Problem Triage

After confirming it is a bug, decide which process to follow based on complexity:

## Simple Problems → Quick Fix

**Criteria**: You can see where the problem is at a glance, the change scope is very small (a few lines of code), and it does not involve complex logic.

**Approach**:
1. Confirm the problem symptoms
2. Locate and fix it directly
3. Run relevant tests to ensure no regression
4. Tell the user what was changed and why

No need to write a fix report, no need for a complete reproduction process.

## Complex Problems → Full Investigation

**Criteria**: The cause is not obvious, it involves multiple modules, the logic is complex, or it may affect other functionality.

Follow the complete process below.

---

# Full Fix Process

## 1. Gather Information, Reproduce the Problem

**No reproduction, no code changes.** This is an iron rule.

You need to understand from the user:
- Where it occurred (page/feature)
- What operation triggered it (the more specific the better)
- Expected result vs. actual result
- Relevant logs, screenshots, error messages

If there is not enough information to reproduce, ask follow-up questions. Focus on 1-2 of the most critical questions each time. Do not dump a long list of questions all at once.

Only proceed to the next step after successful reproduction. If you cannot reproduce it, keep gathering information. Do not guess and change code.

## 2. Locate the Root Cause

Starting from the symptoms, gradually narrow down the scope:
- Feature module → specific component/service → key function
- Compare "expected behavior vs. actual behavior" to find the logic divergence point
- Prioritize checking recently modified code, reused modules, and shared utilities

After finding the root cause, confirm: How wide is the impact of this problem? Does it only affect the current scenario, or could it affect other functionality?

## 3. Fix

Principles:
- **Minimal changes**: Only change what must be changed. Do not refactor unrelated code on the side.
- **Reuse first**: Prioritize using existing patterns and tools in the project.
- **Clear reasoning**: Every change must have a clear reason for why it was made.

If there are multiple fix options, list the choices for the user, analyze the pros and cons, and give a recommendation.

## 4. Test and Verify

Choose the appropriate verification method based on the nature of the bug:

**Logic/data bugs**: Write unit tests or integration tests to cover this scenario. Ideally, the test fails before the fix and passes after the fix.

**UI/interaction/style bugs**: Use Playwright MCP for browser-side verification — you can check element visibility, CSS properties, page screenshot comparisons, and whether interaction behavior matches expectations. Style issues can also be verified automatically; do not give up on automation just because it is a "visual issue."

**Data bugs**: Use Supabase MCP to query the database and verify whether the data state matches expectations.

The above methods can be combined. Regardless of which method you use, after the fix, run the relevant test suite to ensure there is no regression.

## 5. Generate Report

Check whether the `docs/bug-fix-docs/` directory exists; create it if it does not. Read `assets/bugfix-report-template.md`, fill in the content, and save it as `docs/bug-fix-docs/YYYYMMDD-HHMM-brief-problem-description.md`.

If you discover during the fix that the code's behavior is inconsistent with existing documentation, update the relevant documentation accordingly.

---

# Bottom Line Rules

- First determine whether it is a bug — requirement changes do not go through the bug fix process
- Do not modify code for complex problems that have not been reproduced
- There must be verification after the fix (automated tests or manual verification, at least one)
- Complex problems must generate a fix report; simple problems do not need one
- Principle of minimal changes — do not refactor unrelated code on the side
