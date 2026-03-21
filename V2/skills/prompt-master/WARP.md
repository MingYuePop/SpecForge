# Prompt Master — Warp Variant

A Warp-optimized version of Prompt Master. Generates surgical, credit-efficient prompts for any AI tool directly from your terminal workflow.

Same core skill as `SKILL.md` — with additional context blocks and templates tailored for developers working inside the terminal.

---

## Installation

### Recommended

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/nidhinjs/prompt-master.git ~/.claude/skills/prompt-master
```

### Warp AI Custom Prompt

1. Clone or download this repo
2. Copy the full contents of `WARP.md`
3. In Warp: open **AI Settings → Custom Prompt** → paste content

For all installation options, see the main [README](README.md).

---

## Why a Separate Warp Variant

Warp AI lives inside your terminal, which changes the context entirely.

Terminal users are almost always working with code, files, and CLI tools rather than writing or design tasks. The most common prompt targets are Claude Code, shell scripts, git workflows, and build pipelines. Every prompt generated in this context needs to account for the current working directory, shell environment, installed tools, and recent command output.

The standard SKILL.md does not capture that environment automatically. This variant adds it.

---

## What This Variant Adds

Every prompt generated inside Warp includes an Environment Block:

```
## Environment
- OS: [macOS / Linux / Windows WSL]
- Shell: [zsh / bash / fish]
- Working directory: [relevant path]
- Tools installed: [node, python, git, docker, etc.]
```

When the target is a CLI-based AI tool (Claude Code, Aider, Cursor CLI), a Current State block is also added:

```
## Current State
[Output of `ls` or `git status` if relevant]
[Any recent error message from the terminal]
```

These two blocks alone eliminate the most common cause of wrong output when using AI from the terminal: the AI does not know what environment it is operating in.

---

## Quick Invocations

**Fix a failing command or error:**
```
/prompt-master — write a Claude Code prompt to fix this error: [paste error]
```

**Scaffold a new project from scratch:**
```
/prompt-master — Claude Code prompt to scaffold a [type] project with [stack]
```

**Automate a repetitive shell task:**
```
/prompt-master — prompt for Claude Code to write a bash script that [task]
```

**Stop a runaway agent loop:**
```
/prompt-master — my Claude Code agent is looping, write a stop-condition prompt
```

**Debug a broken build or CI pipeline:**
```
/prompt-master — prompt to fix this GitHub Actions error: [paste error]
```

**Refactor a specific file without touching anything else:**
```
/prompt-master — Cursor prompt to refactor [file] without modifying any other file
```

---

## Agentic Template — Full Version for Terminal Users

This is the most important template for Claude Code and other autonomous agents. Runaway agent loops are the single biggest credit killer in terminal-based AI workflows, and this template prevents them.

```
## Objective
[Single, unambiguous goal in one sentence]

## Environment
- OS: [your OS]
- Shell: [zsh / bash / fish]
- Working directory: [path]
- Tools available: [node, python, git, docker, etc.]

## Starting State
[Current file structure — paste output of `ls -la` or `git status`]
[Any relevant error messages from the terminal]

## Target State
[What the directory or codebase should look like when the agent is done]

## Allowed Actions
- Read and edit files inside [specific directory] only
- Run [specific commands — be explicit]
- Install packages listed in [requirements.txt / package.json] only

## Forbidden Actions
- Do NOT modify files outside [directory]
- Do NOT run the dev server or any long-running process
- Do NOT push to git or make any remote changes
- Do NOT delete files without showing a diff first
- Do NOT create files not explicitly mentioned in the task

## Stop Conditions
Pause and ask for human review when:
- A file would be permanently deleted
- A new external API or service needs to be integrated
- Two valid implementation approaches exist and the choice affects architecture
- An error cannot be resolved within 2 attempts
- Any action would affect files outside the stated scope

## Checkpoints
After each step, output one line: ✅ [what was completed]
At the end, output a full summary of every file that was created or modified.
```

---

## Why Stop Conditions Matter

Claude Code and similar agentic tools can edit files, run commands, install packages, and loop indefinitely. Without explicit stop conditions, they will.

The three most common failure modes in terminal-based agent workflows are:

| Failure Mode | What Happens | Fix |
|-------------|-------------|-----|
| **Scope creep** | Agent edits files you never mentioned | Add forbidden actions list |
| **Runaway loop** | Agent retries the same failing action repeatedly | Add "stop after 2 failed attempts" condition |
| **Silent architecture decisions** | Agent picks an approach without asking | Add "stop when two valid approaches exist" condition |

All three are addressed in the Agentic Template above.

---

## Framework Selection for Terminal Workflows

Most terminal tasks fall into one of three categories. Use the right framework for each.

| Task Type | Framework | When to Use |
|-----------|-----------|-------------|
| **Autonomous file editing** | ReAct + Stop Conditions (Template H) | Claude Code, Devin, any agent that runs autonomously |
| **Single file code edit** | File-Scope Template (Template G) | Cursor, Windsurf, Copilot — targeted edits only |
| **Shell scripting or automation** | RTF (Template A) | Writing bash scripts, cron jobs, CI/YAML configs |

For the full template library and all 9 frameworks, see [SKILL.md](SKILL.md).

---

## Pattern Reference — Terminal-Specific

These are the most common credit-killing patterns for terminal and agent workflows.

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 1 | **No starting state** | "build me a REST API" | "Empty Node.js project, Express installed, `src/app.js` exists" |
| 2 | **No target state** | "add authentication" | "`/src/middleware/auth.js` with JWT verify middleware exists. `POST /login` and `POST /register` exist in `/src/routes/auth.js`" |
| 3 | **No stop condition** | "build the whole feature" | Explicit stop conditions added, checkpoint output after each step |
| 4 | **Unlocked filesystem** | No file restrictions stated | "Only edit files inside `src/`. Do not touch `package.json`, `.env`, or any config file." |
| 5 | **No environment context** | Agent guesses OS and shell | Always include OS, shell, working directory, and installed tools |
| 6 | **Silent agent** | No progress output | "After each step output: ✅ [what was completed]" |
| 7 | **No human review trigger** | Agent makes all decisions | "Stop and ask before: deleting any file, adding any dependency, or changing the database schema" |
| 8 | **Missing error context** | "fix the build" | Paste the full error message and the command that produced it |

---

## Version History

- **1.0.0** — Initial release: Warp-optimized variant with Environment Block, Current State block, Agentic Template, and terminal-specific pattern reference
