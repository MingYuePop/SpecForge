I am currently using a self-developed workflow called **SpecForge**

I have used most of the AI workflows on the market, but the experience often fell short of what I wanted. The initial idea came from Kiro Spec mode, but after using it, I found it was not perfect enough, so I redesigned a set myself. After real-world testing across multiple projects and repeated optimization, I found it to be exceptionally useful, especially for someone like me with almost no programming background.

This post will not walk through the internal implementation of each Skill one by one. Instead, it will take you through the **methodology and complete workflow** of this system — why it is designed this way, what problem each step solves, and the tips I have accumulated from actual use. The article will be fairly long, but after reading it, your understanding of AI programming will be completely different.

The workflow and tips will continue to iterate with development practice, and I will keep sharing them with everyone. If you find areas for improvement, feel free to submit a PR on [GitHub](https://github.com/MingYuePop/SpecForge) — my perspective alone is far from enough. I need everyone's feedback and suggestions to polish it better.

---

## About Me

I am someone with almost no programming background, with only a middle school education. I previously learned Python basics but did not go deep — because that was exactly the era when AI programming was exploding. The programs I worked so hard to write, AI could knock out in a few minutes. At that time, there were no real AI programming tools yet; you could only use them on web pages, manually copying and pasting. Later, Cursor, Trae, Claude Code, and others came along.

I have used AI to write multiple programs and applications, and this year I earned my first 10,000 yuan. It is not a lot, but I am only 16 years old, and I am really happy. My goal is to save up for an iPhone 18 Pro, because my current phone is really too laggy. If I am going to use something, I use the best — that is my principle.

Why mention all this in the self-introduction? I want to prove one thing: **everyone now has the opportunity; you just need to do it.** But why do many people fail to produce results when developing with AI? That is the problem this post aims to solve.

---

## Development Sequence: How Most People Fail

Suppose you have an idea: **I want to develop a personal blog.**

How would you tell the AI? Most people either just throw out "I want to make a blog," or they add some feature points like "it needs an article publishing feature and a user registration feature."

This is really just the first two stages of development: **what to build** and **what features it has**. But there are many more stages after that — what registration method to use? Email or phone number? What API to integrate for phone numbers? How to design the database?

For people without a technical background, the further along you go, the less you know how to answer. And the AI? It does not know you at all. You say "develop a blog," and it knows to build a blog, but it does not know what specific features the blog should have. It can only guess. What it guesses will differ from what you have in mind, and the further along you get in development, the more it drifts, until the entire project becomes a mess.

**The root cause is: there is no systematic planning process.**

---

## Workflow Overview: Look at the Map Before Hitting the Road

Before introducing each Skill one by one, let me give you a panoramic view so you know what the entire workflow looks like.

This workflow consists of **13 Skills**, divided into three layers:

**Layer 1: Project-Level (used once at startup)**

From a vague idea to a project skeleton ready for coding, go through these 7 steps:

```
Requirements Clarification → Product Overview → Tech Stack Selection → Directory Structure → Development Standards → Roadmap Planning → Project Initialization
```

The output of each step is the input of the next, linked together like an assembly line. After completing them, the `specs/` directory will contain a complete set of project documentation, and the project directory structure will be set up.

**Layer 2: Feature-Level (used repeatedly)**

After the project skeleton is set up, you develop feature by feature according to the roadmap. Each feature goes through these 4 steps:

```
Feature Requirements Clarification → Technical Design → Task Planning → Coding Implementation
```

The roadmap has 10 features? Then you run this 10 times. If a completed feature needs changes, there is a dedicated evolution Skill:

```
Feature Evolution → Coding Implementation
```

**Layer 3: Universal (use anytime)**

Encountered a bug? Directly invoke the bug fix Skill — it works regardless of which stage you are in.

**One-sentence summary**: Project-level runs once to lay the foundation, feature-level loops to build the floors, universal-level is on call to patch things up.

### Two Core Mechanisms That Make This Process Actually Work

Having 13 Skills is not enough. If the AI does not follow the rules — secretly writing code when it should be doing requirements analysis, or completely forgetting your project when switching to a new window — then no matter how good the process is, it is all for nothing.

So this workflow has two core mechanisms that are "invisible but always at work." Every Skill automatically loads them when executing:

**Mechanism 1: Guardrails (GUARDRAILS)**

AI has an instinct: whatever you ask, it wants to do for you. This sounds like a good thing, but in a workflow, it is actually the biggest hidden danger.

For example, while using the requirements clarification Skill, you casually mention "how would this feature be implemented?" The AI's instinctive reaction is to write code for you directly. But at this point, the requirements have not been thought through yet, so any code written is wasted, and it might even lead you astray — you might think "well, the code is already written, let's just go with these requirements," and end up with pitfalls everywhere down the line.

The guardrails exist to manage exactly this. It draws a hard line for each Skill: **you can only do what this stage requires in this stage.** The requirements stage only discusses requirements, the design stage only produces designs, and the coding stage is the only time code gets written. The AI tries to cross the line? It gets blocked directly, and then tells you "this is not the time for that; let's first think through the current stage."

This is not the AI refusing to help you — quite the opposite. **Doing the wrong thing at the wrong stage is doing a disservice.** The guardrails force the AI to do the right thing at the right time.

**Mechanism 2: Project Context Protocol (PROJECT-CONTEXT)**

What is the AI's biggest problem? **No memory.** You chat with it for two hours in one window, switch to a new window, and it knows nothing about your project.

What happens without this protocol? The AI writes Vue + JavaScript code in a project using Next.js + TypeScript; the project already has an existing utility function, and the AI writes another one from scratch; the development standards say to use Tailwind, and the AI writes a bunch of inline styles.

The project context protocol's rule is simple: **before executing any Skill, the AI must first read all documents in the `specs/` directory to build a complete understanding of the project.** It cannot start working until it has finished reading.

This is why I said earlier "opening a new window does not lose context" — because no matter how many new windows you open, the AI is forced to re-read the project documentation every time. Your tech stack, development standards, and existing feature designs — it knows them all. As long as the documents exist, the memory exists.

Now let me introduce each Skill one by one.

---

## Skill 1: project-requirements-clarification (Requirements Clarification)

This Skill exists to solve the "no systematic planning process" problem.

When you have a vague idea, it uses **Socratic-style guided questioning** to help you dig into the idea from multiple dimensions — what is the core value, who are the target users, what are the key features — ultimately generating a standardized project description.

Why "guided" rather than having you fill out a form yourself? Because for people who do not know the details, if you ask them to tell you themselves, they cannot. They need someone to guide them, asking step by step, and the answers naturally emerge.

The most powerful thing about this Skill is that it acts like a **curious partner** chatting with you, rather than a cold form-filling machine. Just like when you tell a partner "I want to make a blog," the partner will definitely follow up with many questions — that is the role the AI plays here.

And you can call this Skill repeatedly. For example, after the first result is generated, if you feel it is not refined enough, just tell the AI "I want to add more features," and it will use the same guided approach to help you dig deeper.

I use this Skill 100% of the time when starting a new project. For beginners, I strongly recommend starting here.

**Example**

Your message:
`/project-requirements-clarification I want to develop a personal blog`

AI's response:

> That is an interesting idea! Let me help you think it through. Let me ask a few key questions first:
>
> **Why do you want to build a blog?**
> - A: To document your own tech learning journey, for yourself
> - B: To write articles and attract readers, building a personal brand
> - C: Purely for practice, learning full-stack development
> - Or some other reason?
>
> Tell me this first, and then I will ask you about target users and core features. One step at a time, no rush.

---

## Skill 2: project-product-overview (Product Overview)

After requirements clarification is done, you have a project description in hand. But this description is more like a "summary of the chat" — the information is there, but it is not structured enough. It is still a bit short of being used for tech stack selection or architecture design.

What happens without this Skill? You might take the vague requirements and start having the AI write code directly. Halfway through, you discover: which module does this feature belong to? What are the acceptance criteria? Who are the target users exactly? Then you start going back to fill in the gaps, and as you fill them in, you find the earlier code does not match the new plan, and you have to change it again.

What this Skill does is **upgrade the requirements clarification results into a formal product document**. It helps you clarify: what is the project vision, where is the core value, who are the target users, what are the core modules, and how to define acceptance criteria.

The AI plays the role of **Chief Product Officer** here. Where information is missing, it uses guided questioning to help you fill it in — the questions are very specific, giving you examples to choose from, rather than asking confusing open-ended big questions.

The final output is a `specs/product-overview.md`, which serves as the "foundation" for all subsequent Skills.

**Example**

Your message:
`/project-product-overview Please generate a product overview based on the requirements clarification results`

AI's response:

> I have read your project description. Most of the information is clear, but there are a few key points that need to be supplemented:
>
> **1. The core value is not clear enough**
> What is the biggest difference between your blog and other blogs on the market?
> - A: Focus on the Markdown writing experience, as smooth as Typora
> - B: Focus on SEO and traffic acquisition, helping you get your articles out there
> - C: Focus on minimalist deployment, one-click launch with zero ops
> - Or do you have other ideas?
>
> **2. Acceptance criteria need to be quantified**
> What is the standard for the first version launch? I suggest defining at least two:
> - Feature level: e.g., "can publish articles, can categorize by tags, has basic reading statistics"
> - Performance level: e.g., "homepage loads in < 2 seconds"
>
> Please tell me your choices, and I will generate the complete product overview document.

---

## Skill 3: project-tech-stack (Tech Stack Selection)

With the product overview set, the next question is: **what technology should be used to build it?**

Many people either go search for "the hottest frontend framework" or just tell the AI "you pick for me." Both approaches have problems — chasing what is trendy easily leads to pitfalls (new frameworks have incomplete ecosystems, insufficient documentation, and less AI training data). If you leave it entirely to the AI, it does not know your specific constraints either, and might recommend a solution that is "technically perfect but practically unusable for you."

This Skill's AI role is **CTO**, and its selection logic is **"most suitable" rather than "most popular."** It first reads your product overview, analyzes key constraints like project scale, user volume, and real-time requirements, and then proactively recommends a complete technology combination — not having you pick one by one, but giving you a pre-packaged solution.

For people who do not understand technology, the most considerate design here is: when you need to make a choice, it will always **give options, give explanations, and give recommendations.** It will not coldly ask you "what database to use"; instead, it tells you what scenario each option is suited for and then says "I recommend this one, because...".

The final output is `specs/tech-stack.md`.

**Example**

Your message:
`/project-tech-stack Please perform tech stack selection`

AI's response:

> I have read your "Product Overview." This is a personal blog project with core requirements of Markdown writing + SEO-friendly + low ops cost. Based on the analysis, I recommend the following solution:
>
> **Recommended Solution: Next.js + Supabase + Vercel**
> - **Frontend/Backend**: Next.js 14 (App Router) — SSR is naturally SEO-friendly, handles both frontend and backend in one, no need to maintain a separate backend
> - **Database**: Supabase (PostgreSQL) — the free tier is sufficient for a personal blog, with built-in user authentication
> - **Deployment**: Vercel — Next.js's native platform, push and it runs, zero ops
> - **Styling**: Tailwind CSS — fast development, and the AI is most comfortable writing it
>
> One detail to confirm: **Do you need a comment feature?**
> - A: No, keep it minimal
> - B: Yes, use a third-party service (e.g., Giscus, based on GitHub Discussions, zero cost)
> - C: Yes, build a custom comment system (will add significant work)
> - *My suggestion*: If you want one, choose B — zero cost and it does not affect the core development pace.

---

## Skill 4: project-structure (Directory Structure)

The tech stack is chosen, but you cannot just start writing code, right? Where does the code go? How are files organized? How are modules divided?

What happens without planning the directory structure? At first, you might not feel it — when there are few files, you can put them anywhere. But once the project grows, you will find: components mixed with pages, utility functions scattered in every corner, code for one feature spread across five or six unrelated folders. Later on, whether it is you or the AI, modifying a feature means searching all over the project for files.

This Skill's AI role is **System Architect**. It reads both the product overview and the tech stack document simultaneously, maps "core modules" to code modules, and then designs the directory according to the tech stack's best practices. The core principle is just one: **high cohesion, low coupling** — related code goes together, unrelated code is strictly isolated.

The final output is `specs/project-structure.md`.

**Example**

Your message:
`/project-structure Please design the project directory structure`

AI's response:

> Based on the tech stack (Next.js 14 + Supabase) and the three core modules from the product overview (content management, user system, reading experience), I designed the following directory structure:
>
> ```
> blog-project/
> ├── src/
> │   ├── app/                  # Next.js App Router pages
> │   │   ├── (auth)/           # Login/registration related pages
> │   │   ├── (blog)/           # Blog frontend pages
> │   │   └── admin/            # Admin dashboard pages
> │   ├── modules/              # Business modules (core)
> │   │   ├── auth/             # User authentication
> │   │   ├── posts/            # Article management
> │   │   └── analytics/        # Reading statistics
> │   ├── shared/               # Shared components and utilities
> │   └── lib/                  # Third-party service wrappers
> ├── specs/                    # Project specification documents
> ├── docs/                     # Development documentation
> └── public/                   # Static assets
> ```
>
> **Design rationale**: Using a feature-based architecture, where each module under `modules/` is an independent business unit. During subsequent development, the AI only needs to focus on the corresponding module directory.
>
> Does this structure look OK to you? Let me know if anything needs adjusting.

---

## Skill 5: project-dev-standards (Development Standards)

The directory structure is in place, but how should the code be written? How should variables be named? How should Git commits be formatted?

If these are not defined upfront, the consequence is — you have the AI write ten files, and each file has a different style. Some use camelCase, some use snake_case; some components use arrow functions, some use function declarations; Git commit messages are all over the place. The pain of fixing this afterward is far greater than defining it upfront.

This Skill's AI role is **Technical Committee**. It generates a complete set of development standards based on your tech stack, covering code style, naming conventions, Git workflow, error handling, and even including an **AI collaboration protocol** — telling the AI "what rules you must follow when writing code in this project."

There is an important design here: **every rule is specific enough to be directly executable.** There is no nonsense like "follow best practices"; instead, it explicitly tells you "component files use PascalCase, utility functions use camelCase," with correct and incorrect examples side by side for comparison.

The final output is `specs/dev-standards.md`.

**Example**

Your message:
`/project-dev-standards Please establish development standards`

AI's response:

> I have read the tech stack and project structure documents. Here are the customized development standards (excerpt):
>
> **Naming Conventions**
>
> | Element | Style | Example |
> |------|------|------|
> | Component files | PascalCase | `PostCard.tsx` |
> | Utility function files | camelCase | `formatDate.ts` |
> | Directory names | kebab-case | `user-profile/` |
>
> **TypeScript Strict Rules**
>
> ```typescript
> // Wrong - using any is prohibited
> const data: any = await fetchPost()
>
> // Correct - explicit type definition
> const data: PostDetail = await fetchPost()
> ```
>
> **Git Commit Conventions**
> ```
> feat(posts): add article tag filtering feature
> fix(auth): fix login state loss issue
> ```
>
> The complete standards have 15 sections, all generated. Please confirm and I will save them to `specs/dev-standards.md`.

---

## Skill 6: project-roadmap-planning (Roadmap Planning)

At this point, you have the product overview, tech stack, directory structure, and development standards — "how to build" is clear. But there is still one question: **what to do first?**

This question is more important than you might think. Many people's approach is "do whatever comes to mind," or "start from the first page." The result? When they get to user management, they find the login system is not set up yet; when they get to the article detail page, they find the data model has not been defined. They get stuck on dependencies everywhere.

This Skill's AI role is **Technical Product Manager**. It does three things:

1. **Analyzes module dependencies** — which are foundational (e.g., user authentication, shared components), which are core business, and which are nice-to-haves
2. **Divides milestones** — what goes in the MVP, what goes in the full version, what goes in the enhanced version
3. **Generates the development sequence** — each module comes with specific development instructions; check one off when done

Once you have the roadmap, you no longer need to agonize over "what to do next" — just follow the order.

The final output is `specs/dev-roadmap.md`.

**Example**

Your message:
`/project-roadmap-planning Please plan the development roadmap`

AI's response:

> Based on the product overview and project structure, I analyzed the dependency relationships between modules and planned as follows:
>
> **Milestone 1: MVP (Core Loop)**
> - [ ] Phase 1.1: Infrastructure — `auth` + `shared` (foundation, all business modules depend on it)
> - [ ] Phase 1.2: Core Business — `posts` (article creation, editing, publishing, Markdown rendering)
> - [ ] Phase 1.3: Frontend Display — article list page, detail page, tag filtering (MVP is usable after this step)
>
> **Milestone 2: Full Version**
> - [ ] Phase 2.1: Reading Statistics (`analytics`)
> - [ ] Phase 2.2: Admin Dashboard (`admin`)
>
> **Milestone 3: Enhanced Version**
> - [ ] Phase 3.1: SEO Optimization (sitemap, Open Graph)
> - [ ] Phase 3.2: Performance Optimization (image lazy loading, ISR)
>
> I suggest starting from Phase 1.1. Come back to check off progress after completing each Phase.

---

## Skill 7: project-initialization (Project Initialization)

The first six Skills are all "planning" — they all generate documents. At the seventh, it is finally time to **take action**.

This is the only "execution-type" Skill in the entire workflow. Its responsibility is simple: **strictly follow the previously generated documents to create the project skeleton.** Note "strictly follow" — it will not do anything that is not defined in the documents, will not take it upon itself to add a framework or change a configuration.

It reads your tech stack, project structure, and development standards documents, then: creates all directories, generates configuration files (`.gitignore`, `.env.example`, `README.md`, etc.), and initializes the Git repository. When done, it outputs an initialization record.

If there is already code in the project directory (e.g., you are using this workflow on an existing project), it will automatically detect it and skip, without overwriting anything.

Final output: project skeleton code + `docs/dev-logs/initialization-record.md`.

**Example**

Your message:
`/project-initialization Initialize the project`

AI's response:

> Starting project initialization.
>
> **Environment Check**
> - specs/tech-stack.md ......... Ready
> - specs/project-structure.md ........ Ready
> - specs/dev-standards.md ........ Ready
> - Current directory ................ Empty directory, ready to initialize
> - Node.js v20.11.0 ........ Installed
>
> **Executing...**
> 1. `npm init -y` .................. Done
> 2. Install core dependencies ................... Done (next, react, typescript, tailwindcss...)
> 3. Create directory structure (14 directories total)..... Done
> 4. Generate configuration files ................... Done (.gitignore, .env.example, tsconfig.json...)
> 5. `git init` + first commit .......... Done
>
> **Initialization complete.** Detailed log saved to `docs/dev-logs/initialization-record.md`.
>
> Next step: Please start development following Phase 1.1 in `specs/dev-roadmap.md`.

---

## Feature-Level Workflow: Developing Specific Features (V3 Rework)

After project initialization is complete, you have a full set of documents and a project skeleton. Now you enter the real development phase: **building features one by one.**

The feature-level workflow is similar to the project-level — first clarify requirements, then design the approach, then break down tasks, and finally write code. The difference is that it is a **closed loop for a single feature**, and you will use it repeatedly. The roadmap lists 10 features? Then you run this process 10 times.

**V3 did a near-complete rework of the five feature-level Skills.** There are three core changes: first, Skills went from operation manuals to role definitions — no longer teaching the AI step by step what to do, but telling it who you are, what to focus on, and where the bottom line is; second, TDD (Test-Driven Development) was introduced in the coding stage — write tests first, then write code; third, Acceptance Criteria (AC) run through the entire chain, from requirements to coding, every stage must be traceable to AC.

---

## Skill 8: feature-requirements-clarification (Feature Requirements Clarification)

You might be thinking: did we not already do requirements clarification? Why do it again?

Because the project-level requirements clarification is a "global perspective" — what product you want to build and what the major modules are. But when it comes to a specific feature, the details are far more nuanced.

For example, you say "I want to add search to the article list." Sounds simple, right? But have you thought about these questions: search titles or search body text? Can filter conditions be combined? What to display when nothing is found? Should search history be saved? How do you define "done"?

If you do not think these through, the AI can only guess, and what it guesses will be completely different from what you have in your head.

In V3, this Skill's role is your **product partner**. It will not give you a list of A/B/C/D to choose from; instead, it chats with you like a real partner. You say "just search titles," and it might follow up with whether the body should be searched too, what about tags; you mention "support filtering," and it will continue the conversation about what the relationship is between filter conditions. The entire process does not touch technology — it only discusses what the user can do.

The most important output of this stage is **Acceptance Criteria (AC)**, each describing a specific scenario in Given-When-Then format. The quality of the AC determines everything that follows — how the technical design is done, how tasks are broken down, how tests are written.

Finally, it outputs a feature requirements document to the `specs/features/` directory.

**Example**

Your message:
`/feature-requirements-clarification I want to add search to the article list`

AI's response:

> Search feature, got it. Let me ask a few basics first — when you say search, do you mean searching only titles, or the body too? What about tags?
>
> Also, does your article list currently have categories or filters? If so, what is the relationship between search and filtering? For example, if I first select a tag and then search, does it search within that tag or search everything?
>
> Tell me roughly what effect you want, and we will take it step by step.

---

## Skill 9: feature-tech-design (Technical Design)

The requirements document is written; now it is time to think about "how to implement it."

Without this Skill, many people just let the AI start writing code directly. The result is the AI picks an implementation approach at random, gets halfway through, finds it is not suitable, and starts over. Or worse — the feature is done, but it conflicts with the existing code architecture, and fixing it is more painful than rewriting.

In V3, this Skill's role is your **technical partner**. It first looks at what can be reused in your project, then works backward from the AC to determine what data models, interfaces, and core logic are needed. Decisions that follow existing project practices are made directly without asking you; but when new dependencies need to be introduced or there are multiple viable approaches, it pauses for your confirmation.

At the end of the design, there is an AC coverage summary table where you can see at a glance whether each requirement has a corresponding technical design. If a certain AC cannot be technically implemented, it must say so explicitly — it cannot pretend it is covered.

**Example**

Your message:
`/feature-tech-design Search feature`

AI's response:

> I have finished reading the requirements document. There is a decision for you to make on the search — your current article volume is not large, so using the database's LIKE query is sufficient, simple and straightforward. But if the article volume grows later, you might need to switch to something like Elasticsearch.
>
> I suggest using LIKE for now and migrating when you actually hit a performance bottleneck — lowest cost. What do you think?
>
> Also, should the search box have debounce? That means when the user is typing, it does not send a request on every keystroke; it waits until they stop typing before searching. I recommend adding this — the experience will be much better, and the implementation is not complicated.

---

## Skill 10: feature-task-planning (Task Planning)

The technical design is done, but you cannot just throw it at the AI and say "write code according to the technical design." A feature might involve a dozen files and five or six modules. If you have the AI do it all at once, it will likely get confused and miss things, because the overly long context causes quality degradation.

In V3, this Skill's role is **Tech Lead**, breaking the technical design into atomic tasks — each 30 minutes to 2 hours, single responsibility, independently verifiable. It also clarifies dependencies and displays them with a Mermaid diagram.

V3 has two important changes. First, **tests are no longer standalone tasks.** In V2, there would be a separate "write unit tests" task; V3 removed this, because every task is executed through TDD, and testing is embedded in the execution process. Second, **the quality of acceptance criteria became the core output.** Acceptance criteria directly serve as input for the TDD red phase — if they are well-written, you know exactly how to write the first test during development. For example, "the search API returns correct data" is a bad acceptance criterion; "GET /api/articles?q=Next.js returns 200, every article's title contains Next.js" is a good one.

Each task also has a one-line plain-language explanation, describing the user-visible change in zero technical terms, such as "After completion, the user can see a search box at the top of the list."

**Example**

Your message:
`/feature-task-planning Search feature`

AI's response:

> I have finished reading the technical design and broken it down into 5 tasks across 2 stages.
>
> Stage 1: Backend
> - Task-01: Search API implementation [45min]
>   Plain-language: After completion, the backend has the ability to find articles by keyword
>   Acceptance criteria: GET /api/articles?q=Next.js, every returned article's title contains Next.js
> - Task-02: Filtering and pagination [40min] ← depends on Task-01
>   Plain-language: After completion, search results support tag filtering, 10 items per page
>   Acceptance criteria: GET /api/articles?q=Next.js&tag=frontend&page=2, returned results satisfy both keyword and tag conditions
>
> Stage 2: Frontend
> - Task-03: Search box component [40min]
> - Task-04: Search results list and empty state [35min] ← depends on Task-03
> - Task-05: Debounce and loading state [30min] ← depends on Task-04
>
> Note that there are no separate test tasks here. Each task will write tests first then code through TDD during execution.

---

## Skill 11: feature-implementation (Coding Implementation)

Finally, the coding part.

After all the groundwork — requirements, technical design, task planning — this step is actually the most relaxed. Because what the AI needs to do is already clearly written. It does not need to guess or improvise; it just follows the documents and executes task by task.

The biggest change in V3 is here: **TDD was introduced as the only coding method.** Each task goes through the Red-Green-Refactor cycle — first write a failing test based on the acceptance criteria, then write just enough code to make it pass, and finally refactor under test protection. There is only one iron rule: no failing test, no implementation code.

In V2, before each task started, a prompt would pop up asking "Continue?" — seven tasks, seven prompts, and you could only keep replying "continue." V3 removed this mechanical confirmation; the AI proceeds smoothly like a real developer.

After the TDD cycle is complete, the acceptance method is chosen based on the task nature: UI tasks use Playwright for browser-based verification, pure backend tasks rely on unit test coverage, and database changes are verified through queries.

After each stage is completed, a report is generated, which includes a technical debt section for recording pragmatic compromises made during development. What matters is recording them, not pretending they do not exist.

Why go stage by stage instead of doing it all at once? The AI's context window is limited; stuffing too much in causes quality degradation. After completing each stage, you can check it and catch problems early.

**Example**

Your message:
`/feature-implementation Complete the search feature tasks, Stage 1`

AI's response:

> I have read all three documents. Stage 1 has 2 tasks with no dependency blockers. Let's begin.
>
> Task-01: Search API implementation
>
> First, write the test. Based on the acceptance criteria, the first test is: request GET /api/articles?q=Next.js, assert it returns 200 and every article's title contains Next.js. The second test is the empty result case: q=a-nonexistent-word, assert it returns 200 and the array is empty.
>
> Let's run it — both tests failed, because the API does not exist yet. This is expected. Now starting to write the implementation code...

(The AI will proceed through each task following the TDD cycle, update the task planning document upon completion, and generate a stage report.)

---

## Skill 12: feature-evolution (Feature Evolution)

The feature is done, launched, and used for a while — then you have new ideas. "Can search remember history?" "Can it filter by time range?"

At this point, if you directly tell the AI "add a history feature to search," it will likely mess up the existing code — because it does not know what was written in the previous requirements document and technical design. It only sees the current code and then does reckless surgery.

This Skill's role is **Product Architect**, specifically handling incremental modifications to completed features. It first reads all previous documents to understand the current state, then analyzes the impact from four levels: at the requirements level, which ACs need to be added, removed, or modified; at the technical level, how interfaces and data need to change; at the code level, which files are affected; at the task level, whether any in-progress tasks are impacted.

The core principle is to modify, not redo. Content that is not affected stays as-is; only the affected parts are modified in place, and a change log is appended at the end.

Changes are categorized into three types:

- **Tweak**: Small changes, like adjusting the sort order, no new AC involved
- **Extension**: Adding new things, like search history, requires new ACs
- **Refactor**: Changing core structure, like switching the search engine from LIKE to Elasticsearch

V3 added a key judgment: if the change impact exceeds 70% of the original feature, the AI will suggest you go back to requirements clarification and re-run the process, rather than forcing an incremental change. This pushback itself is a valuable output.

**Example**

Your message:
`/feature-evolution Add search history to the search feature`

AI's response:

> I have read the full set of documents for the search feature. Adding search history is an extension-type change — it requires new ACs but does not affect the existing search logic.
>
> Impact analysis: At the requirements level, 2 new ACs are added (auto-record after search, click a history term to search directly). At the technical level, a new search_history table and corresponding API are needed. On the frontend, a history dropdown panel needs to be added below the search box. The existing search API and result display do not need changes — regression risk is low.
>
> 3 new development tasks are needed, estimated at 80 minutes. I will generate the change document first, then you can execute it with feature-implementation.

---

## Skill 13: bugfix-workflow (Bug Fix)

What do you do when you encounter a bug? Most people throw the error message at the AI and say "fix it." The AI looks at the error, guesses a cause, changes a few lines of code, and tells you "it should be fixed."

Is it fixed? Sometimes yes, sometimes no, and sometimes the old bug is gone but a new one appears. Where is the problem? **No reproduction before fixing.** The AI does not know under what conditions this bug is triggered; it just guessed a possible cause based on the error message.

This Skill enforces a strict fix process: **Reproduce → Locate → Fix → Unit Test → Verify → Report**.

The most critical hard rule: **if it has not been reproduced, no code changes.** Not enough information to reproduce? It will follow up — which page? What operation? Expected result? Actual result? It keeps asking until it can reproduce.

After the fix, it does not just say "it is done" and move on. It must give you a step-by-step manual verification process — specific to "open which page, click which button, enter what content, see what result." It also automatically writes a unit test for this bug to prevent the same issue from popping up again. Finally, it generates a fix report saved to `docs/bug-fix-docs/` for traceability.

**Example**

Your message:
`/bugfix-workflow After posting a comment, the page does not refresh and still shows the old comment list`

AI's response:

> Got it. I need to confirm a few pieces of information to reproduce this problem:
>
> 1. Which page does it occur on? (Article detail page? Personal center?)
> 2. What operations did you perform? (Be as detailed as possible, step by step)
> 3. After posting the comment, did the page not change at all, or did it refresh after a delay?
> 4. Open the browser console — are there any error messages?
>
> Please answer these questions first. I will not start locating and fixing until I can reproduce it.

---

## Practical Tips: Pitfalls I Have Hit and Lessons Learned

After introducing all the Skills, let me share some tips I have accumulated from actual development. These are all problems that the documentation will not tell you about, but that you will encounter repeatedly in practice.

### Tip 1: For feature-level development, separate planning and coding into different windows

The feature-level workflow has 4 steps: Requirements Clarification → Technical Design → Task Planning → Coding Implementation.

The first three steps (requirements clarification, technical design, task planning) are closely related, and **it is recommended to do them all in the same window**. Because the details discussed in requirements directly affect the technical design, and the technical design directly determines how tasks are broken down — in the same window, the AI remembers this context most clearly.

But when it comes to the coding implementation stage, the approach is different: **follow the tasks in the task plan, one task per new window.** Do not do multiple tasks consecutively in one window; too much context buildup will noticeably degrade the AI's response quality.

Of course, it also depends on task complexity — if they are a few particularly simple small tasks, doing them in one window is fine. But for complex tasks, definitely give it a clean window.

You might worry: will opening a new window lose context? No. Because the documents generated by each Skill are saved in the `specs/` directory. When a new window opens, the Skill forces the AI to read these documents first and rebuild a complete understanding of the project.

**As long as the documents exist, the context exists.** So do not be stingy with opening new windows — open them when you need to.

### Tip 2: For project-level planning, try to complete it in one window

In contrast to the feature-level, the 7 project-level Skills (requirements clarification through roadmap planning) I recommend **completing in one window** — provided your model's context window is large enough.

Why? Because the project-level Skills are closely interrelated, and the discussion details from one step directly affect the next step's judgment. For example, if you mentioned "need to support offline use" during requirements clarification, this information is critical during tech stack selection. In the same window, the AI remembers these details clearly; in a new window, although the documents will have a record, the subtle context from the conversation (your preferences, the points you deliberated over) is lost.

Of course, if your model's context is not large enough, or the conversation got too long and the AI noticeably became sluggish, then decisively open a new window — do not force it.

### Tip 3: Polish your prompts first, then save them for reuse

Every sentence you send to the AI is essentially a prompt. The same intent, expressed differently, can produce vastly different quality results from the AI.

My approach: **before sending to the AI, first throw what you want to say into a web-based AI (like ChatGPT, Claude) for polishing.** Let it help you turn vague descriptions into clear, structured expressions. You will find that polished prompts are understood more accurately by the AI, and output quality improves noticeably.

More importantly: **create a document specifically for storing the prompts you have used.** Why? Because as you develop further, you will find that many tasks are actually similar — making another list page, writing another API. But the prompt you wrote this time might not be as good as last time. If you have a record, you can directly take the better-performing prompt from last time, tweak it, and use it.

Once you develop this habit, your prompt library will grow stronger and stronger, and your efficiency will get higher and higher.

### Tip 4: How to choose between feature-evolution and starting over?

After a feature is done, when you need to change requirements, should you use feature-evolution for incremental changes, or go through the whole process again from feature-requirements-clarification?

The judgment criteria is simple: **scope of change.**

- Change does not exceed 30% of the original feature → use feature-evolution (incrementally update documents + append new tasks)
- Change exceeds 70% → basically a redo, use feature-requirements-clarification to re-run the process
- Between 30%-70% → depends on complexity; if unsure, try feature-evolution first — it will automatically determine the change type and give you a recommendation

### Tip 5: What if you finish a stage and find something is wrong?

For example, you completed Stage 1 of coding implementation, but then find a design flaw in the technical design.

Do not panic, and do not directly change the code. The correct approach is:

1. **Go back to the technical design** — use feature-evolution to propose the change and let it analyze the impact scope
2. **Update the documents** — it will incrementally update the technical design and task planning
3. **Execute the change tasks** — use feature-implementation to execute the newly generated incremental tasks

The benefit of this approach is that all changes are traceable, and documents and code always stay in sync. Directly changing code is faster, but later the AI reads documents that do not match the actual code, and things get increasingly messy.

### Tip 6: Ask when you do not understand, and do not idle while waiting for the AI

Let me share a real experience. When I first started developing with AI, I did not understand anything — I did not know what a backend was, did not know what a database was for, did not know the difference between Next.js and Vue, did not even know what an API meant. A complete beginner.

But think about it — you are already using AI now. While the AI is working for you, what are you doing? Scrolling your phone? Waiting?

**Why not use this time to ask about the things you do not understand.** For example, the AI is writing code for you, and you notice the technical design mentions "middleware" — you do not know what that is. Just open a new window and ask the AI: "What is middleware? Explain it to me in plain language." Then have it organize this knowledge into a document for future reference. Next time you encounter the same concept, just look it up in the document instead of asking again.

The more you understand, the more efficient your communication with the AI becomes, the more precise your requirements become, and the better the final product. This is a positive loop — **while the AI works for you, you are also growing.** Do not waste this free teacher.

### Tip 7: When documents are out of sync, manually have the AI sync them

You will definitely encounter this problem; I encounter it often myself.

What happens? While the AI is writing code according to the task plan, you temporarily add a requirement — like "change this button to red" or "add a search box to the list." The AI does it, the code is changed, but the requirements document and technical design under `specs/` are still the old ones. **The documents and the actual code are out of sync.**

If this problem is ignored, when you open a new window later, the AI reads the old documents and thinks the project is still in its previous state, which will conflict with the actual code.

My solution is simple and direct: **manually tell the AI to sync the documents.** For example, say "I just added XX feature on the side; please update the requirements document and technical design accordingly." The AI will compare the current code with the documents and fill in the gaps.

You might ask: why not make a dedicated sync Skill? Because this situation is too flexible — what you added might be a small change or a big adjustment, involving different documents and different amounts of content each time. After trying it, I found that directly telling the AI in natural language is actually the most efficient way — more flexible than a fixed process.

**The core principle is just one: if you changed code, sync the documents. If you find them out of sync, fix it immediately. The longer you wait, the harder it gets.**

### Tip 8: Spend two minutes reviewing AI-generated documents

Do not just skip past AI-generated documents. Even if you cannot understand the technical details, it does not matter — **just spend two minutes scanning through.**

You do not need to understand every line, but the parts you can understand are often the most important — is the feature description correct? Is the flow what you want? Did it miss any requirement you mentioned? These are all written in plain language that even beginners can judge.

Why is this step important? Because documents are the input for all subsequent Skills. If the requirements document is wrong, the technical design follows suit; if the technical design is wrong, the task planning follows suit; and the code written at the end will naturally be wrong too. **The earlier you catch a problem, the cheaper it is to fix.** Changing one sentence at the document stage is a hundred times easier than rewriting code after it is done.

So every time the AI generates a document, do not rush to the next step — scan it first.

### Tip 9: The golden rules for communicating with AI

When using this workflow, there are a few techniques for talking to the AI that can significantly improve results:

- **Actively invoke Skills yourself**: For example, manually type `/feature-requirements-clarification comment feature` instead of throwing out "I want to make a comment feature" and waiting for the AI to find the right Skill on its own. The AI might not accurately identify your intent; invoking it yourself is the most reliable
- **Do one thing at a time**: Do not say "help me make a comment feature, and also fix the login page" in one message. Each feature follows its own process, without interfering with each other

### Tip 10: For tasks the AI cannot handle, try in this order

When developing with AI, you will definitely encounter tasks it cannot handle. I have run into this many times myself. Do not keep banging your head against it — try step by step in this order:

**Step 1: Switch models.** Different models excel at different things. What Claude cannot handle, GPT might solve in a snap, and vice versa. Switching models has the lowest cost.

**Step 2: Optimize your prompt.** Sometimes it is not that the AI is incapable, but that you did not explain clearly. Reorganize your requirements, describe them more specifically and more structuredly, and it might work.

**Step 3: Break the task into smaller pieces.** If the AI cannot do a large task, it might be too complex. Try breaking it into two or three smaller tasks, complete them separately, then combine them yourself.

**Step 4: Look for references on GitHub.** Have the AI search GitHub for similar features and see how other people's open-source projects implemented them. With reference code, it is much easier for the AI to adapt than to start from scratch.

**Step 5: Figure out exactly where it is stuck.** If you have tried all the above and it still does not work, stop and think: where does the AI's result differ from your expectation? Is the logic wrong? Or is the entire direction off? Ask the AI to analyze the reason for failure. Once you understand it, decide — try a different approach to get around it, or set it aside for now and come back when a stronger model comes out.

**Do not spend too long stuck in a dead end.** AI technology is advancing rapidly. A task that cannot be done today might be a one-liner when a new model comes out in a few months. Do what you can first, note down what you cannot, and come back later.

---

## About Efficiency and Future Plans

There is one thing I want to be honest about: **the development efficiency of this workflow is currently not fast.**

Because tasks are completed serially — finish Task-01 before starting Task-02, finish Task-02 before starting Task-03. I feel this clearly when using it myself, especially when there are many tasks — the wait time is long.

It is not that I have not thought about solving this. I previously tried having the AI create multiple Agents to develop multiple tasks simultaneously — for example, if Task-01 and Task-02 have no dependency, they could run in parallel. But after trying, I discovered a fatal problem: **without a review mechanism, I simply did not dare to let go.**

Why? Because multiple Agents writing code at the same time — A drifts a little, B drifts a little, and by the time you notice, both sides have problems. You go to fix A and find B also needs changes; after fixing B, A has a new issue. Without an automated review step to check for you, parallel development is actually more troublesome than serial.

So a review Skill is a must, and it needs to be reliable enough — it needs to automatically check code quality, verify compliance with the technical design, and have the Agent self-correct when issues are found, forming a closed loop. But it is very token-intensive.

**This workflow was originally designed for myself.** With no funding support and no vendor sponsorship, AI subscriptions are paid out of my own pocket. So I chose the most cost-effective approach — work a bit harder myself, develop one task at a time. It is slow, but every step is controllable.

But from the moment I shared it, this is no longer just my own business. People using this set of Skills might have more ample budgets or higher efficiency requirements. **Serial development is tolerable for me, but it should not be a limitation for everyone.**

So going forward, I will seriously work on these things:

- **Review Skill**: Let the AI automatically review code quality, forming a "develop → review → correct" closed loop
- **Parallel development support**: After the review mechanism is reliable, support simultaneous development of multiple tasks
- **Companion tutorials**: Each new capability will come with a detailed usage tutorial

These are not empty promises; they are pain points I have genuinely felt during my own development. Once they are done, I will share them with everyone right away.

---

## In Closing

Looking back at this entire workflow, the core philosophy comes down to three words:

**Document-driven** — all decisions are captured in documents. The AI does not "amnesia" when switching windows, and you can understand why things were done a certain way even a month later.

**Stage separation** — each Skill does only one thing. The product manager does not touch code, the architect does not write implementations, the developer does not change requirements. There is no chaotic situation of "starting to write code while discussing requirements."

**Guided interaction** — you do not need to be an expert. You just need to answer questions and make choices. The AI lays out the options, tells you which one it recommends and why, and you just nod.

Simply put, this workflow takes the classic software engineering process of "requirements → design → development → testing" and solidifies it using Skills, letting the AI play the corresponding professional role in each stage. V3 goes further by moving testing to the front of the development process (TDD) and making AC the verification thread that runs through the entire process. You do not need to understand technology; you just need to know what you want — leave the rest to the process.

SpecForge's Skill files are open source. GitHub address: [https://github.com/MingYuePop/SpecForge](https://github.com/MingYuePop/SpecForge)

The repository has V1, V2, and V3 versions. **Just use the latest V3 version.** V1 is an early experimental version, V2 is the first refactor, and V3 is a complete rework of the feature-level Skills — from operation manuals to role definitions, introducing TDD, with AC running through the entire chain.

Thank you for reading this far. I hope this workflow can help you.
