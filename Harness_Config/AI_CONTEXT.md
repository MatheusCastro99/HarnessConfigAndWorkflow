# AI Context

## What this file is for

It is the page an agent loads first. It says in a few lines what the project is, then points to every context document with one line on what that document holds.

The agent's guidance file (for Claude Code, `CLAUDE.md`) tells it to read this page before planning or editing anything. From here it reaches the rest.

## What goes in it, and what stays out

Goes in:

- A short summary of the project: what it is and who it is for
- A link to each context document, with one line on what it answers
- Links to the project's own documents (vision, requirements, roadmap)
- The date it was last updated

Stays out:

- Anything that has its own document. Link to it; do not repeat it, or the two copies drift apart.
- Rules about how the main session behaves in the repository. They are in the agent's guidance file.
- The state of the current issue. That lives in the issue.

## The index

This is the index of this repository.

### This repository

- [README](../Docs/README.md): overview and status
- [Project Vision](../Docs/Project_Vision.md): what the repository is and is not
- [PRD](../Docs/PRD.md): what the repository contains and what it must do
- [Project Roadmap](../Docs/Project_Roadmap.md): phases and their status

### Context documents

| Page | What it answers |
|---|---|
| [Development Workflow](Context/Development_Workflow.md) | Which stages does an issue go through, and which of them end with the owner's approval? |
| [Working Agreements](Context/Working_Agreements.md) | Who decides, how is a recommendation made, how is a finding triaged, where is a decision recorded? |
| [Data Flow](Context/DataFlow.md) | How does data move from a component to an endpoint and back, and what happens on an error? |
| [Architecture Design](Context/Architecture_Design.md) | How is the project structured, and which files matter? |
| [UI Guidelines](Context/UI_Guidelines.md) | What must the interface look and feel like? |
| [Current Focus](Context/Current_Focus.md) | What is being worked on now? |
| [Decisions and Consistency](Context/Decisions_Consistency.md) | Which standing rules must every change follow? |

### Agents and skills

| Page | What it answers |
|---|---|
| [Red Team](Agents/Red_Team.md) | Why is there an independent reviewer, and how is it configured and briefed? |
| [Historian](Agents/Historian.md) | Why is there a documentation updater, and how is it configured and briefed? |
| [Guardrails Review](Skills/Guardrails_Review.md) | What does the project review checklist check? |
| [UX Design](Skills/UX_Design.md) | What does the interface and copy review check? |

### Templates and examples

- [Stale-docs list](../Templates/stale-docs.md): the running list a change keeps for the documentation pass
- Copy-ready agent definitions: [red-team](../Templates/agents/red-team.md), [historian](../Templates/agents/historian.md), [surveyor](../Templates/agents/surveyor.md)
- Copy-ready skills: [guardrails-review](../Templates/skills/guardrails-review/SKILL.md), [ux-design](../Templates/skills/ux-design/SKILL.md), [harness-onboarding](../Templates/skills/harness-onboarding/SKILL.md)
- Examples: [BabyBuddyHelper](../Examples/BabyBuddyHelper-examples.md), [InvoiceMe](../Examples/InvoiceMe-examples.md): how each project uses the pieces

## Skeleton

```markdown
# AI Context

Last updated: <date>

## Project
<Two or three sentences: what the project is, who it is for, what it values.>

- [Project Vision](<path>)
- [Requirements](<path>)
- [Roadmap](<path>)

## Context documents
| Page | What it answers |
|---|---|
| [Architecture Design](<path>) | How is the project structured, and which files matter? |
| [Current Focus](<path>) | What is being worked on now? |
| [Decisions](<path>) | Which standing rules must every change follow? |
| [UI Guidelines](<path>) | What must the interface look and feel like? |
| [Development Workflow](<path>) | Which stages does an issue go through? |
| [Working Agreements](<path>) | Who decides, and how? |
| [Data Flow](<path>) | How does data move from a component to an endpoint and back? |

## Agents and skills
| Page | What it answers |
|---|---|
| [<agent or skill>](<path>) | <what it is for> |
```

## Examples

Examples: [BabyBuddyHelper](../Examples/BabyBuddyHelper-examples.md#ai-context).
