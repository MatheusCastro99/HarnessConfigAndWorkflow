# Project Roadmap

## Epic 1: [#1](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/1)

- One issue and one pull request per phase, worked in this order.
- Phases 3 and 4 were delivered together in one pull request, because the red-team template preloads the guardrails skill.

## Phase 1: Planning and scaffold (#2): CONCLUDED

- `.gitignore` and MIT `LICENSE`
- This repository's own documents: README, Project Vision, Project Roadmap, PRD
- `.claude/CLAUDE.md`
- A link-check workflow in GitHub Actions

## Phase 2: Workflow core (#3): CONCLUDED

- `AI_CONTEXT`: the index an agent loads first
- `Development_Workflow`: the stages of an issue, from gathering information to the memory flush
- `Working_Agreements`: who decides, how recommendations are made, how findings are triaged, where decisions are recorded
- `DataFlow`: how data flows through a project, from component to endpoint and back
- The stale-docs list template

## Phase 3: Agents (#4): CONCLUDED

- Documentation for the red-team and historian subagents
- Copy-ready definitions for both in `Templates/agents/`

## Phase 4: Skills (#5): CONCLUDED

- Documentation for the guardrails review and UX design skills
- Copy-ready skills for both in `Templates/skills/`

## Phase 5: Context templates (#6): CONCLUDED

- `Architecture_Design`, `UI_Guidelines`, `Current_Focus`, `Decisions_Consistency`
- Each with its purpose, what goes in it, what stays out, and a skeleton

## Phase 6: Examples (#7): CONCLUDED

- One examples file per project, for BabyBuddyHelper and InvoiceMe
- Links from every `Harness_Config/` page to its examples
- README pass and close-out of the epic

## Epic 2: [#11](https://github.com/MatheusCastro99/HarnessConfigAndWorkflow/issues/11)

- Starts after epic 1 closes. One issue and one pull request per phase, worked in this order.

## Phase 1: Customizable harness configuration and workflow (#14): CONCLUDED

- A directional change: the repository is reframed as a customizable harness configuration and workflow, which each project or developer adapts as they see fit

## Phase 2: Workflow tuning (#19): CONCLUDED

- The approval gates redesigned, loops added, stages 7 and 8 condensed into one, and the workflow diagram redrawn

## Phase 3: Onboarding (#15): PLANNED

- A skill that surveys a project through a read-only subagent and drafts its pages with the developer, starting from the smallest set the project needs
- Both as copy-ready definitions in `Templates/`, explained in a "Get Started" section of the README

## Phase 4: Validation (#16): PLANNED

- A run of the onboarding skill on a snapshot of InvoiceMe with its documentation removed, compared with the documents written by hand

---

## After the epics

Nothing is scheduled. Each of these was left out of the epics on purpose (at least for now):

- A script that installs the harness configuration into a project
- A Claude pull request review workflow for this repository

The roadmap is directional; planned items should not be read as available today.
