# HarnessConfigAndWorkflow

[![Link Check](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/actions/workflows/link-check.yml/badge.svg)](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/actions/workflows/link-check.yml)
[![Status](https://img.shields.io/badge/Status-Functional-brightgreen)](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/1)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue)](../LICENSE)

HarnessConfigAndWorkflow documents how I work with an AI coding agent on a real project: the context it reads, the rules it follows, the subagents and skills it uses, and the stages every issue goes through.

It is a customizable harness configuration and workflow. Each piece explains what it is for, gives a skeleton to fill in, and shows how it was filled in on two projects built this way: [BabyBuddyHelper](https://github.com/MatheusCastro99/BabyBuddyHelper) (.NET MAUI) and [InvoiceMe](https://github.com/MatheusCastro99/InvoiceMe) (MERN).

Each project, or developer, may employ it as they see fit. The two projects in the examples each use it in their own way.

The repository was built with the workflow it documents. See [Status](#status) for what exists today.

---

## Who it is for

Developers looking for an organized, structured way to start agentic development in their projects.

The workflow and its pages apply to any platform that supports its requirements: parallel agents, context management and skills. The copy-ready definitions in `Templates/` are written for Claude Code.

## The approach in short

- **The owner decides.** The agent recommends, with trade-offs, and says so when the path looks sub-optimal.
- **Context is written down.** The agent loads the project's own documents before it plans or edits anything.
- **Decisions are standing rules.** A reviewer can check a change against them.
- **Every issue goes through the same stages,** in order. The owner approves at fixed gates: the decisions, the plans, the pull request, the fixes and the documentation.
- **Review is independent.** A subagent with no stake in the change tries to break it before the change is merged.
- **Documentation is part of the change.** What a change makes stale is tracked on a running list and fixed before the merge.
- **Simple first.** Add structure when the project needs it, not before.

The full version is in [Project Vision](Project_Vision.md).

---

## What it contains

| Piece | Where | What it gives you |
|---|---|---|
| Context documents | `Harness_Config/Context/` | What each document is for, what goes in it, and a skeleton |
| Context index | `Harness_Config/AI_CONTEXT.md` | The page an agent loads first |
| Agents | `Harness_Config/Agents/` | Why each subagent exists, when to use it, how it is configured |
| Skills | `Harness_Config/Skills/` | What each skill checks and when to use it |
| Templates | `Templates/` | Copy-ready agent and skill definitions, and the stale-docs list |
| Examples | `Examples/` | The same pieces as filled in on BabyBuddyHelper and InvoiceMe |

## Get Started

The `harness-onboarding` skill tailors the harness configuration to your project, with you. You run it once per project.

1. Clone this repository anywhere on your machine. The skill reads its pages, templates and examples from the clone.
2. In your project, copy [Templates/agents/surveyor.md](../Templates/agents/surveyor.md) to `.claude/agents/surveyor.md`, and [Templates/skills/harness-onboarding/SKILL.md](../Templates/skills/harness-onboarding/SKILL.md) to `.claude/skills/harness-onboarding/SKILL.md`.
3. Fill the placeholder listed at the top of each file (the project's name, and the path of your clone), then delete that comment.
4. Start Claude Code in your project and run `/harness-onboarding`.
5. The skill explains the whole flow first. A read-only subagent surveys your repository, and the skill recommends the smallest set of pages your project needs. It then drafts them with you in four steps: Documentation, Skills, Agents, Review. Each page is written only after you approve it, all on one branch, and the work ends with a pull request.

Claude Code's `/init` writes a `CLAUDE.md` from the repository alone. This skill drafts the pages your project needs through an interview with you: what only you know comes from you.

## Structure

```text
HarnessConfigAndWorkflow/
│
├── .claude/
│   └── CLAUDE.md
│
├── .github/
│   └── workflows/
│       └── link-check.yml
│
├── Docs/
│   ├── README.md
│   ├── Project_Vision.md
│   ├── Project_Roadmap.md
│   └── PRD.md
│
├── Harness_Config/
│   ├── AI_CONTEXT.md
│   ├── Context/
│   │   ├── Architecture_Design.md
│   │   ├── UI_Guidelines.md
│   │   ├── Current_Focus.md
│   │   ├── Decisions_Consistency.md
│   │   ├── Development_Workflow.md
│   │   ├── DataFlow.md
│   │   └── Working_Agreements.md
│   ├── Agents/
│   │   ├── Red_Team.md
│   │   └── Historian.md
│   └── Skills/
│       ├── UX_Design.md
│       └── Guardrails_Review.md
│
├── Templates/
│   ├── agents/
│   ├── skills/
│   └── stale-docs.md
│
├── Examples/
│   ├── BabyBuddyHelper-examples.md
│   └── InvoiceMe-examples.md
│
└── LICENSE
```

`Docs/` holds this repository's own documents. `Harness_Config/`, `Templates/` and `Examples/` are the harness configuration and workflow.

Runnable agent and skill definitions in `.claude/agents` and `.claude/skills` are personal tooling and are not tracked, here or in the two source projects. `Templates/` holds the versions meant to be copied.

---

## Status

| Epic | Phase | Issue | Status |
|---|---|---|---|
| 1 | 1. Planning and scaffold | [#2](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/2) | Done |
| 1 | 2. Workflow core | [#3](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/3) | Done |
| 1 | 3. Agents | [#4](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/4) | Done |
| 1 | 4. Skills | [#5](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/5) | Done |
| 1 | 5. Context templates | [#6](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/6) | Done |
| 1 | 6. Examples | [#7](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/7) | Done |
| 2 | 1. Customizable harness configuration and workflow | [#14](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/14) | Done |
| 2 | 2. Workflow tuning | [#19](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/19) | Done |
| 2 | 3. Onboarding | [#15](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/15) | Done |

Today the repository holds its own documents in `Docs/`, the workflow core (the context index, the `Development_Workflow`, `Working_Agreements` and `DataFlow` pages, and the stale-docs list template), and the agents and skills: the red-team and historian pages, the guardrails review and UX design pages, and a copy-ready definition for each in `Templates/`. It also holds the other four context pages: architecture design, UI guidelines, current focus, and decisions and consistency. `Templates/` also holds the onboarding pieces: the harness-onboarding skill and the surveyor agent, explained in [Get Started](#get-started). `Examples/` holds one file per project, with how each uses the pieces.

Details are in the [Project Roadmap](Project_Roadmap.md).

## Documentation

| File | Purpose |
|---|---|
| [Project_Vision.md](Project_Vision.md) | What the repository is, what the approach is, and what it is not |
| [PRD.md](PRD.md) | What the repository contains and what it must do |
| [Project_Roadmap.md](Project_Roadmap.md) | Phases and their status |

---

## License

[MIT](../LICENSE)

## Author

**Matheus Castro**

Repository:
https://github.com/MatheusCastro99/HarnessConfigAndWorkflow
