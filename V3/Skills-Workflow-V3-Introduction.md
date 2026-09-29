# SpecForge V3 Release: A Complete Rework of Feature-Level Skills

## Preface

I previously released SpecForge V2, and thank you all for your support. After spending time actually using this workflow for real project development, I discovered a fundamental problem: the V2 Skills were too much like operation manuals — tedious for humans to read, and too rigid for AI to execute. So I spent considerable time doing a near-complete rework of the five feature-level Skills, resulting in V3.

The project-level Skills were not updated this time; this update is entirely focused on the feature-level, which is the part you use most frequently in daily development.

---

## 1. What Was Updated

### 1. The Design Philosophy Changed

V2 Skills were essentially operation manuals — do this in step one, do that in step two, nine steps written out, and the AI would walk through them from start to finish. The conversation format was also preset: option A is like this, option B is like that, here's the recommendation — the same format regardless of the scenario. The same rule was also repeated in multiple places, with different wording each time.

V3 takes a different approach. Instead of teaching the AI step by step what to do, it tells it: what role you play, what aspects you should focus on, and where your bottom line is. As for what to do first and what to do later, and how to communicate with the user — let it judge for itself.

In short, it went from an "operation manual" to a "role definition."

### 2. TDD Was Introduced in the Coding Stage

V2's coding approach was to write code according to the plan and then check it. V3 changed to TDD, i.e., the Red-Green-Refactor cycle: first write a test that will fail, then write just enough code to make the test pass, and finally refactor under test protection.

The impact of TDD extends beyond the coding stage. Because tests must be written first during coding, the AI must know what to test. What to test comes from acceptance criteria, acceptance criteria come from the technical design, and the technical design comes from the requirements. This means the AI in every preceding stage will automatically raise its precision. The user does not need to worry about this — you just say "I want a comment feature" and the AI will help you fill in the details through conversation during the requirements stage, write clear interface definitions on its own during the technical design stage, and make acceptance criteria specific during the task planning stage.

In other words, it is not about requiring the user to write more precisely, but rather TDD forces the AI to not cut corners in any stage, because it knows it will need this information to write tests later.

### 3. AC Runs Through the Entire Chain

AC stands for Acceptance Criteria. V2 had them too, but each stage wrote its own without a strict correspondence. V3 requires that every AC must have a landing point in every subsequent stage.

For example, the requirements stage produces an AC:

> AC-001: Given the user is logged in, When they post a comment, Then the comment appears at the top of the list

Then every subsequent stage must account for it: the technical design must clearly state which interface implements this AC, how the data is stored, and what the sorting logic is; the task planning must have specific tasks to implement it; and the coding stage must have tests to prove it was actually achieved.

If a certain AC cannot find a corresponding design point in the technical design's coverage summary table, it means a requirement was missed. If the task planning has no task covering a certain AC, it means something is not being done. Each stage checks whether the previous stage missed anything — the chain itself is the checking mechanism.

### 4. Output Templates Were Greatly Simplified

V3 significantly streamlined the templates:

| Template | V2 Lines | V3 Lines | Reduction |
|---|---|---|---|
| Task Planning Template | 303 lines | 84 lines | -72% |
| Stage Completion Report Template | 178 lines | 55 lines | -69% |
| Feature Evolution Template | 190 lines | 126 lines | -34% |

What was cut was not just length, but more importantly the fixed categorization structure. V2's task planning template preset five stages: data layer, presentation layer, business logic layer, mock data, and exception handling, and also included complete examples from Task-01 to Task-08. The problem is: where would a purely frontend feature have a data layer? Does a simple utility function need five stages? The AI could only force-fit the template, outputting a bunch of "None" and "N/A" placeholder content.

V3's templates only provide a structural skeleton. Stage names are written as `{{Stage Name}}` — how many stages there are and what they are called is determined by the AI based on the actual situation of the feature. Parts that are not relevant are simply skipped, with no placeholders.

The stage completion report is the same. V2 had 8 sections, including test coverage statistics, AC verification checklists, and follow-up action plans. V3 cut it down to 6, because the TDD cycle itself already guarantees test coverage — no need to re-prove it in the report.

### 5. Specific Changes to Each Skill

| Skill | V2 → V3 Key Changes |
| ----- | --------------------------------------- |
| Requirements Clarification  | Four-step linear questionnaire → five-dimensional natural conversation, removed preset question templates |
| Technical Design  | Nine-step linear process → four-dimensional parallel thinking, deduplicated rules |
| Task Planning  | Tests as standalone tasks → tests integrated into TDD execution, added plain-language explanation field and acceptance criteria quality requirements |
| Coding Implementation  | Write code + check → mandatory TDD, removed mechanical confirmation rituals |
| Feature Evolution  | Fixed option categories → natural conversation + 70% threshold judgment |

---

## 2. Why Do It This Way

V2 wrote Skills as detailed operation manuals, trying to control every action of the AI. It looked rigorous, but in practice, three problems emerged, which V3 solves one by one.

First, the AI was locked into a fixed path. A nine-step linear process — whether facing a simple button or a complex payment system, the AI would go through the same nine steps. A truly experienced person does not work this way. V3 changed to listing the dimensions the AI needs to focus on; what to do first and how deep to dig is determined by the actual situation.

Second, preset templates led to cookie-cutter output. Option A is like this, option B is like that, here's the reason for recommending A — regardless of the scenario, the AI output the exact same formatted content, and the conversation turned into a questionnaire survey. V3 only tells the AI to provide options and recommendation reasons when there are multiple approaches; how to express it specifically is left for it to judge based on the scenario.

Third, rule duplication led to ambiguous authority. The same rule was stated three times in three places, with slightly different wording each time, and the AI did not know which version was correct. V3 states each rule only once, in the most appropriate location, with a complete description — no repetition, no scattering.

In addition to solving these three problems, V3 brings two extra benefits. First, greater universality — V2's templates carried obvious project-specific characteristics, presetting categories like data layer and presentation layer that would not apply when switching to a different project. V3 removed these assumptions and is applicable to almost any project. Second, TDD brings reliable quality assurance — it is no longer about writing code and eyeballing whether it looks right, but every line of implementation code is backed by a test.

---

## 3. Complete Project Workflow Tutorial

Below, using the development of a search feature as an example, we will walk through the complete feature-level workflow.

### Step 1: Turn the Idea into Requirements

Skill: `feature-requirements-clarification`

You come to the AI with a vague idea, like "I want to add search to the article list." In this step, the AI's role is your product partner, helping you turn the idea into specific, testable requirements through natural conversation.

It simultaneously focuses on five dimensions: scenarios and users, core flows, boundaries and exceptions, business rules, and scope. But this is not an execution order — rather, these are several questions turning in its mind simultaneously. You say "just search titles," and it might follow up with "should the body be searched too? What about tags?"; you mention "support filtering," and it will continue the conversation about what the relationship is between filter conditions and whether they can be combined; you say "let's not do search history for now," and it puts that out of scope and stops pressing. The entire process does not touch technology — it only discusses what the user can do.

The most important output of this stage is the Acceptance Criteria (AC), each describing a specific scenario in Given-When-Then format:

> AC-001: Given the user is on the article list page, When they enter a keyword in the search box and press Enter, Then the list only shows articles whose titles contain the keyword

> AC-002: Given the user searches for a keyword that does not exist, When the results are empty, Then a "No related articles found" prompt is displayed

Output file: `specs/features/search-feature.md`

### Step 2: Turn the Requirements into a Technical Design

Skill: `feature-tech-design`

Now that the requirements are clear, it is time to figure out how to implement them. The AI's role at this point is your technical partner, making real design decisions rather than filling in templates.

For example, the search feature involves several decisions: use database LIKE queries or integrate Elasticsearch? Should the search have debounce? How should filter conditions be passed to the backend — as a query string or in a POST body? If these decisions can follow existing project practices, the AI will make them directly without asking you. But if new dependencies need to be introduced or there are multiple viable approaches, it will pause for your confirmation.

At the end of the design, there is an AC coverage summary table where you can see at a glance whether each AC has a corresponding technical design point.

Output file: `specs/features/search-feature_tech-design.md`

### Step 3: Break the Design into Tasks

Skill: `feature-task-planning`

The technical design cannot be thrown directly at the AI with "write code according to the design." Doing too much at once with an overly long context will cause quality degradation. In this step, the AI's role is the tech lead, breaking the design into atomic tasks — each 30 minutes to 2 hours, single responsibility, independently verifiable. It also clarifies dependencies and displays them with a Mermaid diagram.

The most critical part of this step is the quality of the acceptance criteria. Because the acceptance criteria directly serve as input for the TDD red phase, if they are well-written, you will know exactly how to write the first test during development. For example:

Bad: The search API returns correct data

Good: GET /api/articles?q=Next.js, returns 200, every article's title in the body contains "Next.js," and those that do not contain it do not appear in the results

Each task also has a one-line plain-language explanation, describing the user-visible change in zero technical terms, such as "After completion, the user can see a search box at the top of the list, and after entering a keyword and pressing Enter, the list will refresh."

Additionally, tests are not standalone tasks. Because each task is executed through TDD, testing is embedded in the execution process.

Output file: `specs/features/search-feature_task-planning.md`

### Step 4: Write Code

Skill: `feature-implementation`

After all this groundwork, this step is actually the most relaxed. What the AI needs to do is already clearly written. Its role is a developer who strictly practices TDD, executing tasks stage by stage.

Each task goes through the Red-Green-Refactor cycle:

1. Red: Write a test based on the acceptance criteria, run it, confirm it fails. The failure reason should be that the feature is not implemented, not a syntax error
2. Green: Write only the minimal code needed to make the test pass, run the full test suite to prevent regression
3. Refactor: Optimize the code under test protection; simple tasks can skip this

After the TDD cycle is complete, choose the acceptance method based on the task nature. UI tasks use Playwright for browser-based verification, pure backend tasks rely on unit test coverage, and database changes are verified through queries.

There is only one iron rule: no failing test, no implementation code.

After each stage is completed, a report is generated, which includes a technical debt section for recording pragmatic compromises made during development. What matters is recording them, not pretending they do not exist.

Output files: code + updated task planning (with completed items checked) + `docs/dev-logs/search-feature_stage-N_completion-report.md`

### Bonus: New Ideas After the Feature Is Done

Skill: `feature-evolution`

The search is done, and after using it for a few days, you want to add search history, or support filtering by time range. This kind of incremental modification to a completed feature uses this Skill.

The AI analyzes the change impact from four levels: at the requirements level, which ACs need to be added, removed, or modified; at the technical level, how the database and interfaces need to change; at the code level, which files are affected; at the task level, whether any in-progress tasks are impacted.

The core principle is to modify, not redo. Content that is not affected stays as-is; only the affected parts are modified in place, and a change log is appended at the end.

Changes are categorized into three types: Tweak (no new AC involved), Extension (new AC or API added), and Refactor (core structure changed). If the change impact exceeds 70% of the original feature, the AI will suggest you go back to requirements clarification and re-run the process instead of forcing an incremental change. This pushback itself is a valuable output.

After completion, it generates an incremental change task plan, then calls feature-implementation to execute.

Output files: incrementally updated documents + `specs/features/search-feature_change-task_CR-001.md`

### Full Workflow Summary

```
Your idea: I want to add search to the article list
  │
  ▼
① feature-requirements-clarification   Product partner, five-dimensional conversation
   Output: search-feature.md (with ACs)
  │
  ▼
② feature-tech-design                  Technical partner, four-dimensional design
   Output: search-feature_tech-design.md
  │
  ▼
③ feature-task-planning                Tech lead, atomic decomposition
   Output: search-feature_task-planning.md
  │
  ▼
④ feature-implementation               Developer, TDD execution
   Output: code + tests + completion report
  │
  ▼
Feature goes live
  │
  Requirement change?
  ▼
⑤ feature-evolution                    Product architect, impact analysis
   Output: change task plan CR-001
  │
  ▼
Back to ④ to execute the change tasks
```

What runs through the entire chain is AC: requirements produce AC, technical design maps AC, acceptance criteria correspond to AC, and TDD tests verify AC. Any break in the chain will be exposed.

---

## 4. In Closing

The essence of this update is moving from treating Skills as operation manuals to treating them as role definitions.

The old version tried to control every action of the AI, and the result was limiting its capabilities. The new version tells the AI who it is, what it cares about, and where its bottom line is, then lets it operate freely within the framework.

Tell the AI what kind of person to be, rather than prescribing every action it must take.

GitHub repository: https://github.com/MingYuePop/SpecForge
