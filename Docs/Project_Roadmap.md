# Project Roadmap

## Epic 1: [#1](https://github.com/MatheusCastro99/HarnessEngineering101/issues/1)

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

## Epic 2: [#11](https://github.com/MatheusCastro99/HarnessEngineering101/issues/11)

- Starts after epic 1 closes. One issue and one pull request per phase, worked in this order.

## Phase 1: Customizable harness configuration and workflow (#14): CONCLUDED

- A directional change: the repository is reframed as a customizable harness configuration and workflow, which each project or developer adapts as they see fit

## Phase 2: Workflow tuning (#19): CONCLUDED

- The approval gates redesigned, loops added, stages 7 and 8 condensed into one, and the workflow diagram redrawn

## Phase 3: Onboarding (#15): CONCLUDED

- A skill that surveys a project through a read-only subagent and drafts its pages with the developer, starting from the smallest set the project needs
- Both as copy-ready definitions in `Templates/`, explained in a "Get Started" section of the README

## Phase 4: Validation (#16): CONCLUDED

- A run of the onboarding skill on InvoiceMe with its documentation removed. The result is merged into InvoiceMe
- The comparison with the documents written by hand, the findings and their triage, recorded on the issue
- The "Get Started" steps expanded from the run

## Epic 3: [#24](https://github.com/MatheusCastro99/HarnessEngineering101/issues/24)

- Refines the onboarding skill and the surveyor agent with what the InvoiceMe run showed in #16's findings.
- One issue and one pull request per phase, worked in this order. The kickoff settled three phases.
- Ends with a second validation run of the refined skill.

## Phase 1: Step cadence, checkpoints and scope guardrails (#26): CONCLUDED

- Approval once per step at a checkpoint, with a digest of every page, and a surveyor Check of the step's pages before each checkpoint
- A follow-up document for what the owner has not confirmed and what is noticed outside the onboarding, and a "Never" section that keeps pages to what their skeleton asks for

## Phase 2: Survey and owner questions (#27): CONCLUDED

- The harness's Development Workflow and Working Agreements recommended as they are, with Working Agreements among the core pages; a surveyor brief without git history, and surveyor briefs split above about 16,000 tokens; a `.gitignore` step, and a question about rules not yet in the code
- The clone looked for at the default path `../HarnessEngineering101`, and the path asked for only when it is not there

## Phase 3: Validation run (#28): CONCLUDED

- A second run of the refined skill on InvoiceMe, from the same stripped snapshot as #16, compared with #16 and merged into InvoiceMe

## Reframe and rename (#32): CONCLUDED

- A standalone issue, outside the epics. The repository describes itself as study material for harness configuration and development workflow, for developers studying harness engineering, and the Vision says it is not a production workflow
- The repository renamed from HarnessConfigAndWorkflow to HarnessEngineering101, with the onboarding skill's default clone path

## Planned epic: [#22](https://github.com/MatheusCastro99/HarnessEngineering101/issues/22)

- Copy-ready templates for Claude Code, Codex and GitHub Copilot, side by side.
- Starts after epic 2 closes and after the refinement work that comes out of #16's findings ([#24](https://github.com/MatheusCastro99/HarnessEngineering101/issues/24)), so it translates templates that are stable.
- The Codex and Copilot templates are translations of the Claude Code ones, not tested by the owner. Colleagues who use those platforms test them and report their findings.
- The phases below are proposed; they are settled at the epic's kickoff.

## Phase 1: Restructure: PLANNED

- The current templates move to `Templates/claude/`, and every link to them is updated
- The pages that apply to any platform are worded for any platform, and the PRD and content rules change to cover three platforms

## Phase 2: Copilot templates: PLANNED

- Templates in `Templates/copilot/`, and their steps in the README's "Get Started" section

## Phase 3: Codex templates: PLANNED

- Templates in `Templates/codex/`, and their steps in the README's "Get Started" section

---

## After the epics

Nothing is scheduled. Each of these was left out of the epics on purpose (at least for now):

- A script that installs the harness configuration into a project
- A Claude pull request review workflow for this repository

The roadmap is directional; planned items should not be read as available today.
