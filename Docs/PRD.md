# Product Requirements Document: HarnessConfigAndWorkflow

## Purpose

HarnessConfigAndWorkflow is a customizable harness configuration and workflow for agentic assisted development. It can be used for any platform that supports its requirements (parallel agents, context management, skills).
It describes the environment an AI coding agent works in on a project (context documents, subagents, skills) and the workflow every issue follows, from gathering information to merge.
Each piece comes with a fill-in skeleton and with real examples from two projects: BabyBuddyHelper (.NET MAUI) and InvoiceMe (MERN).

## Audience

- Developers looking for an organized, structured way to onboard/start agentic development in their projects

## Technical Specifications

- **Content**: Markdown, with Mermaid for diagrams
- **Agent tooling**: Claude Code (subagents and skills)
- **Code**: none to build or compile
- **CI**: GitHub Actions, link check only

## What it contains

| Piece | Where | What it gives the reader |
|---|---|---|
| Context documents | `Harness_Config/Context/` | What each document is for, what goes in it, and a skeleton |
| Context index | `Harness_Config/AI_CONTEXT.md` | The page an agent loads first |
| Agents | `Harness_Config/Agents/` | Why each subagent exists, when to use it, how it is configured |
| Skills | `Harness_Config/Skills/` | What each skill checks and when to use it |
| Templates | `Templates/` | Copy-ready agent and skill definitions, and the stale-docs list |
| Examples | `Examples/` | The same pieces as filled in on BabyBuddyHelper and InvoiceMe |

Every page under `Harness_Config/` has the same shape:

1. What the file is for
2. What goes in it, and what stays out
3. A skeleton to fill in
4. Links to the matching examples in `Examples/`

## Repository Structure

```
HarnessConfigAndWorkflow/
├── .claude/
│   ├── CLAUDE.md - Guidance for Claude Code in this repository (tracked)
│   ├── agents/ - This repository's own runnable agents (gitignored)
│   └── skills/ - This repository's own runnable skills (gitignored)
├── .github/
│   └── workflows/
│       └── link-check.yml - Link check on pull requests and pushes to main
├── Docs/
│   ├── README.md - Repository overview
│   ├── Project_Vision.md - What the repository is and is not
│   ├── Project_Roadmap.md - Phases and their status
│   └── PRD.md - This document
├── Harness_Config/
│   ├── AI_CONTEXT.md - Index of the context documents
│   ├── Context/
│   │   ├── Architecture_Design.md - Structure and key files of a project
│   │   ├── UI_Guidelines.md - Interface and experience guardrails
│   │   ├── Current_Focus.md - What is being worked on now
│   │   ├── Decisions_Consistency.md - Standing rules (ADRs)
│   │   ├── Development_Workflow.md - The stages of an issue
│   │   ├── DataFlow.md - How data flows through a project
│   │   └── Working_Agreements.md - How the owner and the agent work together
│   ├── Agents/
│   │   ├── Red_Team.md - Independent adversarial reviewer
│   │   └── Historian.md - Documentation updater
│   └── Skills/
│       ├── UX_Design.md - Interface and copy review
│       └── Guardrails_Review.md - Project review checklist
├── Templates/
│   ├── agents/ - red-team.md, historian.md, surveyor.md
│   ├── skills/ - guardrails-review/SKILL.md, ux-design/SKILL.md, harness-onboarding/SKILL.md
│   └── stale-docs.md - Stale-docs list
├── Examples/
│   ├── BabyBuddyHelper-examples.md
│   └── InvoiceMe-examples.md
├── LICENSE - MIT
└── .gitignore
```

`Docs/` holds this repository's own documents. `Harness_Config/`, `Templates/` and `Examples/` are the harness configuration and workflow.

## Requirements

- A reader can fill in any skeleton for a new project without reading either source repository.
- A template definition runs in Claude Code once its placeholders are filled, with no other edits.
- Every example names the file and commit it came from.
- This repository shows how each project uses a piece, without justifying the differences.
- Nothing private is published: no secrets, no personal notes, no unfixed security findings.
- Every link in the repository resolves.

## Out of Scope

- Tooling for editors other than Claude Code, until the planned epic below ships
- A script or generator that installs the harness configuration into a project
- Keeping the examples in step with later changes to the source repositories

The `harness-onboarding` skill is not an installer: it tailors the pages with the developer, who approves each one before it is written.

## Planned

Epic [#22](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/22) adds copy-ready templates for Codex and GitHub Copilot beside the Claude Code ones, in `Templates/claude/`, `Templates/codex/` and `Templates/copilot/`. As its phases ship, the agent tooling, the repository structure, the template requirement and the out-of-scope line above change with it, and the documentation states that the Codex and Copilot templates were not tested by the owner. It starts after epic [#11](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/11) and the refinement work from #16. Details are in the [Project Roadmap](Project_Roadmap.md).

## External Resources

- **Source repositories**: [BabyBuddyHelper](https://github.com/MatheusCastro99/BabyBuddyHelper), [InvoiceMe](https://github.com/MatheusCastro99/InvoiceMe)
- **Database**: None
- **Cloud Services**: None
- **APIs**: None
