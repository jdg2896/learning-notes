# AI Hero: AI Coding for Real Engineers - Cohort 3

## Day 1: Fundamentals

### The Constraints of LLMs

- tokens/context scale quadratically
- smart vs dumb zone
  - model starts to struggle as context grows larger
  - the 40% mark can be considered the cutoff from smart to dumb zone
    - 80k if max context is 200k
    - for 1M max context, the smart zone is ~100k
- Context:
  - skills consume context
    - don't install skills globally, unless they're used for all projects
    - only install required skills per project
- models have knowledge cutoff dates
  - all of human knowledge up until a certain date
- LLMs are stateless

### What Are Subagents

- new context window, subagent does the task and reports a summary to the orchestrator agent
- orchestrator can spawn multiple subagents
- Claude Code uses subagents aggressively

### Codebase Exploration

- The course codebase is a course platform for students and instructors.
- Key tech: React, TypeScript, SQLite
- Users and permissions are cumulative: students have least privilege, instructors inherit student access and have more, admins have all permissions.
- React Router is in framework mode since the app is full stack. Other React Router modes are client-side routing with or without external API servers.

### Build A Feature

- Spawned a subagent
- It first read `package.json` and `tsconfig.json`
- Asked clarifying questions before building, e.g.:
  - Who should be allowed to submit a star rating for a course? → Enrolled students only
  - How should the average rating be displayed? → Stars + number + count
  - When a course has no ratings yet, what should appear? → "No ratings yet"
  - Can a student change their rating after submitting? → Yes, update anytime

### Non-Determinism

- agents are non-deterministic, not the same every time

### Showing Context in the Status Line

- https://www.aihero.dev/workshops/fundamentals~bfkce/status-line-context~p2bfk

### Why Plan Mode Sucks

- Agent can't write files by default
- Agent creates a wall of text and asks few questions, so the user is forced to review the plan and might skip over some design issues.
- use `/grill-me` instead
- `/grill-me` observations:
  - it usually provides three options, with one recommended approach
  - could be improved with more pros and cons between each approach. It gives a brief explanation of the differences, which is okay, but a more nuanced breakdown would help. The skill works well as it is.
- `/grill-me` tips:
  - drive the conversation as needed, don't only answer A, B, or C
  - saying "correct" means accepting the recommended answer

### Compaction

- `/compact <optional guidelines>`
- auto-compacting affects output in unpredictable ways; compacting creates "sediment", data that is not fully reliable
- `/clear` is better than `/compact`

## Day 2: Steering

### What is an AGENTS.md File

- AGENTS.md consumes context, keep it as few lines as possible
- `/init` is not recommended, because it generates a larger file than needed
  - commands can just be inferred from `package.json`, etc.
- agents may ignore text not relevant to the current task
- AGENTS.md is global

### Steering an Agent with AGENTS.md

- `/memory` to inject an updated CLAUDE.md into Claude's active context
- Add patterns you want the agent to consistently follow in AGENTS.md

### Progressive Disclosure

- split instructions from CLAUDE.md into separate files: `architecture.md`, `testing.md`, etc.

### Agent Skills

- agent sees the name and description of each skill
- allows progressive disclosure of instructions
- skills can be shared more easily
- add skills to fix common issues
- `/skills` to list skills
- add `disable-model-invocation: true` to prevent the model from invoking a skill
- add `user-invocation: false` to only allow the LLM to invoke a skill

### Using Skills for Steering

- `/write-a-skill`
- Review created skills, and remove irrelevant text

### Automatic Memory

- Claude supports automatic memory
- Check `memory.md` every so often to make sure there aren't weird or irrelevant instructions
- `/memory`, then open the auto-memory folder

## Day 3: Planning

### How to Tackle Massive Tasks

- PRD/specs

### Write Great PRDs with a Skill

- `/to-prd`
- Generated a PRD with `/to-prd`
  - user stories were clear and accurate to what was discussed
  - the PRD contains a lot of information and takes time to review and fully verify. Tendency to skim/skip/gloss over parts can happen.

### Split Features Across Multiple Context Windows with Multi-Phase Plans

- `@prd turn this into a multi-phase plan and save it as a local markdown file`
- The plan doesn't seem to reference the user stories, and some implementation details might get stale.

### What Are Tracer Bullets

- Tracer bullets come from _The Pragmatic Programmer_
- Systems have layers
  - Database, API, Frontend, etc.
  - Layers might be different deployable units or different modules within the system
- Tracer bullets are vertical slices

### Use Tracer Bullets in a Multi-Phase Plan

- `/prd-to-plan`
- Default plan vs tracer bullets:
  - the default plan shows specific implementation/changes, while tracer bullets define what to build with detailed acceptance criteria
  - tracer bullets go end to end; the default plan is per component/service and doesn't touch end to end
  - tracer bullets catch issues earlier; the default plan builds out components first before fully testing end to end

### Executing a Multi-Phase Plan

- `@prd/prd.md @plan/plan.md do phase X`

### AskUserQuestion

- enable or disable the AskUserQuestion tool depending on preference in CLAUDE.md: "Use/Don't use the AskUserQuestion tool."

## Day 4: Feedback Loops

### Is Code Cheap?

- Software quality matters more
- code is cheap, AI can generate code faster, but technical debt and issues can also be generated faster
- Is the codebase easy to change?
  - _A Philosophy of Software Design_ by John Ousterhout
- Software Entropy (_The Pragmatic Programmer_)
  - software quality degrades over time
  - minimizing/preventing software entropy is one of the hardest tasks for an engineer
- AI in a bad codebase has fewer feedback loops to rely on
  - AI is more susceptible to a bad codebase

### Steering Agents to Use Feedback Loops with Skills

- Steering with AGENTS.md and skills
- Typed code is better for agent feedback loops, errors are caught earlier in the loop
- `/do-work` skill

### Building a Do Work Skill

- `/write-a-skill`: plan, implement, feedback loop, commit

### Using the Do Work Skill

- Agent follows the steps
- Ran feedback loops
- It didn't pause, since I instructed it not to pause unless needed
- Incorporated feedback in the loop
- It correctly flagged an inconsistency between the skill and the actual file names (`tests.ts` vs `test.ts`)

### Fixing Agents' Broken Formatting with Pre-Commit

- husky + lint-staged for JS/TS projects

### What is Red-Green-Refactor

- from _Extreme Programming Explained_
- Test-driven development
  - **Red**: write a failing test
  - **Green**: write the minimal implementation to make it pass
  - **Refactor**: improve code quality
- Tracer bullets + RGR work well together

### Red-Green-Refactor with Agents

- `/do-work` with RGR for backend code only
- frontend is too dynamic/fluid for RGR to be effective

## Day 5: AFK Agents

### What is an AFK Agent

- "Do phase N"
- HITL: Human in the Loop
- Already have a PRD (destination) and plan (journey)
- Ralph loop / AFK agent

### Sandcastle

- improves upon the Claude Docker sandbox setup

### Trying HITL Agents

```sh
npx tsx .sandcastle/interactive.ts
```

### Sandboxing

```sh
pnpm sandcastle docker build-image
npx tsx .sandcastle/test.ts
```

- sandbox setup took 0.4s
- context window is 25k tokens

### Setting Up and Trying AFK Agents

```sh
npx tsx ./.sandcastle/main.ts ./prd/admin-analytics.md ./plans/admin-analytics-plan.md
```

- it built based on the PRD/plan
- the feedback loop caught type errors

### Using Backlogs to Queue Tasks for AFK Agents

- updated prompt to include GitHub issues
- can also use any task manager: GitLab, Linear, etc.
- agents prioritize tasks in order of importance
- tracer bullets/vertical slices

### Setting Up a Repo for GitHub Issues

- Create GitHub issues, then run sandcastle

## Day 6: Human in the Loop Patterns

### HITL and AFK Tasks

- What needs HITL:
  - planning
  - QA
    - is it fast?
    - does it feel good?
    - does it do the job/purpose?
  - taste
    - feel
    - opinion
- Agents apply human taste

### Don't Plan Kanban

- issues as dependency graphs

### Using the Kanban Skill

- `/prd-to-issues`
- sandcastle

### Research

- `RESEARCH.md`
- Research should be HITL
  - audit research files, stale files hurt LLM performance
- Research keeps the explore phase small, so implementation and testing can use the valuable context

### Prototyping

- Where prototyping shines:
  - FE design
  - testing new tools
  - testing new services
- `/do-work`, then test the prototype
- `/prototype`
  - UI
  - logic

### Designing Codebases AI Loves

- Humans design software architecture
- AI recreates relationships/code knowledge from scratch
- Can restructure a codebase into deep modules (from _A Philosophy of Software Design_)
- Easier for AI with deep modules, and it can also do TDD more effectively
- `/improve-codebase-architecture`
- Added deep module analysis to `/to-prd`

### Final Workflow

1. `/grill-with-docs`
2. Optional:
   - research
   - `/prototype`
3. `/to-prd`
4. `/to-issues`
5. implement: sandcastle, HITL
6. review, QA

### Appendix: Greenfield Projects

- greenfield: nothing built yet
- brownfield: existing codebase, legacy codebase
- How to start from a blank page:
  - grill
  - capture research as md files
  - prototype based on grill and research findings
  - create PRD
  - focus on both AX and UX (agent experience and user experience)
  - AX:
    - feedback loops
    - technology choice
    - module shape
    - testing strategies

### Appendix: `/grill-with-docs`

- Context:
  - code
  - commit history
  - GitHub (issues, PRs, history)
  - user messages
- Why was it done this way?
  - documented using ADRs (Architecture Decision Records)
- ADRs cannot answer "what on earth is an X" (jargon)
- A glossary answers what X is
  - `CONTEXT.md`
- Comes from Domain-Driven Design

## Q&A

- **Security with agents**: What are the key security considerations and best practices when working with AI agents?
  - Security of the codebase
  - Data exfiltration (`fetch(evil.com)`)
  - Mitigate by sandboxing (Docker sandbox)
  - Only allow certain links
- **Managing the pace of learning**: AI is moving fast, and it's overwhelming (MCPs, evals, deeper understanding of agents and models, etc.). How do I prioritize without burning out?
  - focus on your own steps as a developer: improving your workflow, focusing on the harness
  - AI has converged on the harness; models update every X interval
  - focus on your own skills
  - AI is tactical, humans are strategic
- **Reviewing dense PRDs**: A PRD often contains a lot of information that takes time to review and fully verify. How can I review dense documents more thoroughly and reliably?
- Skills vs Superpowers:
  - Superpowers are skills meant for agents (abilities)
  - Matt's skills are more like commands, more HITL

## Claude Code Cheatsheet

| Shortcut        | Action                                                                |
| --------------- | --------------------------------------------------------------------- |
| `Ctrl + S`      | stash/unstash prompt                                                  |
| `Ctrl + C`      | clear prompt                                                          |
| `Ctrl + C` (2x) | exit Claude                                                           |
| `/context`      | check context usage                                                   |
| `/usage`        | check Claude subscription usage                                       |
| `/clear`        | clear context                                                         |
| `/resume`       | resume previous session                                               |
| `/ide`          | show diffs in VS Code                                                 |
| `@`             | select files to add to context                                        |
| `!`             | enter bash/shell mode                                                 |
| `Tab`           | autocomplete; on a permission prompt, "no" + add instructions instead |
| `Shift + Enter` | new line                                                              |
| `Esc + Esc`     | revert/restore (code and/or conversation)                             |
| `Ctrl + B`      | send command to background                                            |
| `Ctrl + Z`      | hide Claude (`fg` to bring it back)                                   |

## Books Mentioned

- _The Pragmatic Programmer_ - Andy Hunt and Dave Thomas
- _A Philosophy of Software Design_ - John Ousterhout
- _Extreme Programming Explained_ - Kent Beck
- _Domain-Driven Design_ - Eric Evans

## Resources

### Agents

- https://www.aihero.dev/a-complete-guide-to-agents-md
- https://www.aihero.dev/building-effective-agents
- https://github.com/mattpocock/skills
- https://github.com/addyosmani/agent-skills
- https://github.com/owainlewis/youtube-tutorials/tree/main/tutorials/spec-driven-development
- [The Complete Guide to AI Agent Memory Files (CLAUDE.md, AGENTS.md, and beyond)](https://medium.com/data-science-collective/the-complete-guide-to-ai-agent-memory-files-claude-md-agents-md-and-beyond-49ea0df5c5a9)

### AI Ops

From an [OpenAI talk](https://www.youtube.com/watch?v=XGJNo8TpuVA) on taking LLM apps to production:

1. User Experience
2. Model Consistency
3. Evaluating Performance
   - https://github.com/openai/evals
4. Managing Latency & Cost
   - Semantic caching
   - Route to cheaper models
