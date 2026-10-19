---
name: harness-onboarding
description: Onboards this project into the HarnessConfigAndWorkflow harness configuration and workflow. Surveys the repository through the read-only surveyor agent, recommends the smallest set of pages the project needs, and drafts each page with the developer, writing it only once approved. Run it once per project, with /harness-onboarding.
disable-model-invocation: true
---

<!--
Template. Copy this file to `.claude/skills/harness-onboarding/SKILL.md` in your project,
fill the placeholder, then delete this comment. The frontmatter must stay on line 1.

It briefs the `surveyor` agent, so that agent must exist in `.claude/agents/surveyor.md`
(template: Templates/agents/surveyor.md). Install both before you start the session that
runs this skill.

Placeholders:
- <harness-repo-path>   the absolute path of your local clone of HarnessConfigAndWorkflow

`disable-model-invocation: true` means the skill runs only when you type
/harness-onboarding. It writes many files, so it never starts on its own.
-->

# Harness Onboarding

You onboard this project into the harness configuration and workflow kept in the clone at `<harness-repo-path>`. You tailor it with the developer; you do not install it. Every page is drafted with the developer and written only once they approve it.

You recommend; the developer decides. When a path looks sub-optimal, say so, and still let them choose.

## Sources

| Source | What you take from it |
|---|---|
| `<harness-repo-path>/Harness_Config/` | For each page: what it is for, what goes in and what stays out, and the skeleton your draft starts from |
| `<harness-repo-path>/Templates/` | The copy-ready agents and skills, and the stale-docs list |
| `<harness-repo-path>/Examples/` | How two projects filled the pages in: the level of detail to aim for. Never copy their content. |
| `<harness-repo-path>/.claude/CLAUDE.md` | The model for the agent guidance file, which has no skeleton of its own |
| The surveyor's reports | What this repository shows |
| The developer | Everything only the owner knows |

Read the clone; never edit it. Leave out what belongs to HarnessConfigAndWorkflow itself: its issue numbers, its own decisions, its file paths.

## 1. Explain the whole flow first

Before anything else, tell the developer, in one short message:

- **The flow:** a survey of the repository, a recommended set of pages, then four steps (Documentation, Skills, Agents, Review), then a pull request.
- **Their approval:** every page is shown as a draft and written only after they approve it. Nothing is copied into the project unreviewed.
- **What you will ask them:** what only they know: the vision, the intent behind the interface, how they work with the agent, and what they are working on now.
- **Where it happens:** on its own branch, with a commit at the end of each step, each one confirmed first.

Ask whether to start, and wait.

## 2. Prepare

1. Check that `<harness-repo-path>/Harness_Config/AI_CONTEXT.md` exists. If it does not, stop: the placeholder must point at a local clone.
2. Check that the `surveyor` agent is available. If it is not, stop and say where its template is.
3. Propose a branch from the default branch (`docs/harness-onboarding`), and create it once the developer confirms.
4. Ask whether any paths should be skipped. Brief the surveyor: kind Survey, the branch and its commit, the paths to skip.

## 3. Present the survey

- Summarize the report group by group, in plain words, keeping the file references.
- Show the gaps as the report states them. Never smooth one over or fill it with a guess.
- Keep the surveyor's recommendations apart from the facts, and say whose they are.
- Ask the owner-only questions for every topic the repository does not state explicitly: the vision, the intent behind the interface, how they work with the agent, the current focus.
- For a question about something the report covers, send the surveyor a follow-up (kind Follow-up, through `SendMessage`) instead of a new survey.

## 4. Recommend the page set

The core, recommended for every project:

| Page | Starts from |
|---|---|
| Agent guidance file (`CLAUDE.md`) | `.claude/CLAUDE.md` in the clone, as a model |
| AI Context | `Harness_Config/AI_CONTEXT.md` |
| Architecture Design | `Harness_Config/Context/Architecture_Design.md` |
| Development Workflow | `Harness_Config/Context/Development_Workflow.md` |
| Decisions and Consistency | `Harness_Config/Context/Decisions_Consistency.md` |
| Current Focus | `Harness_Config/Context/Current_Focus.md` |
| guardrails-review skill | `Templates/skills/guardrails-review/SKILL.md` |
| red-team agent | `Templates/agents/red-team.md` |

Offer a further page only where the survey found evidence for it:

| Page | Offer it when |
|---|---|
| Data Flow | A request crosses several layers, such as an interface, an endpoint and storage |
| UI Guidelines, and the ux-design skill | The project has a user interface |
| Working Agreements | The developer wants the agent's authority written down, or the repository already states such rules |
| historian agent, and the stale-docs list | The project keeps documentation that a change can make untrue |
| Project documents: vision, requirements, roadmap | The repository has none of its own, and the AI Context page needs them to link to |

For each offer, write three lines: the value for the project, the value for the AI tool, and what the developer must supply. A page the developer declines is left out; don't offer it again. The developer may also decline a core page; say what it costs, and respect the choice.

Then settle where the pages go. Propose the clone's layout (`Harness_Config/` for the context pages, `Docs/` for the project documents) and adapt it to documentation folders the project already has. Ask whether `.claude/agents/` and `.claude/skills/` are tracked in git.

Sum it up as the onboarding plan: the pages, their paths, and the order. Wait for the developer's approval.

## 5. Step 1: Documentation

Draft the chosen pages one at a time, in this order: Architecture Design, Data Flow, Decisions and Consistency, UI Guidelines, Working Agreements, Development Workflow, Current Focus, the project documents, AI Context, and the agent guidance file last, since it points to the others.

For each page:

1. Read its page in `Harness_Config/`, and the matching example in `Examples/`.
2. Draft it from the skeleton, with the survey's facts and the developer's answers only. Ask before drafting what neither of them gives you. A section with nothing confirmed is deleted, as the skeletons say.
3. Show the draft. Write it once the developer approves, then go on to the next page.

Page by page:

- **Decisions and Consistency:** turn the patterns the survey found into candidate rules. The developer decides each rule and its status. The rules are theirs.
- **Development Workflow:** start from the clone's stages and ask which the developer keeps, changes or drops. Leave out the clone's references to its own issues.
- **Current Focus:** name the onboarding as the current work, with its four steps, and list the steps not done yet as unfinished on purpose. Link to this skill rather than repeating its process. The page is rewritten at the close.

At the end of the step, list the pages written and commit them once the developer confirms.

## 6. Step 2: Skills

1. Copy `Templates/skills/guardrails-review/SKILL.md` to `.claude/skills/guardrails-review/SKILL.md`, and the ux-design skill if it was chosen.
2. Fill every placeholder its opening comment lists, from the pages just written and the survey. A known regression trap comes only from the developer or the repository; if there is none, write "None recorded yet." If the developer declined a page the skill loads, remove that line.
3. Delete the opening comment, show the filled skill, and write it once approved.

Commit the step once the developer confirms.

## 7. Step 3: Agents

1. Copy `Templates/agents/red-team.md` to `.claude/agents/red-team.md`, and the historian and the stale-docs list if they were chosen.
2. Fill the placeholders, delete the opening comment, show each file, and write it once approved.

Claude Code picks up a new agent file within seconds, as long as `.claude/agents/` existed when the session started. If it did not, ask the developer to restart the session and resume it before the review.

Commit the step once the developer confirms.

## 8. Step 4: Review

Brief the red-team, if it was written:

- **Goal:** the onboarding pages for this project, as the developer approved them
- **Target:** the branch's changes against the default branch, reviewed as a design document
- **Constraints:** owner-only content is the developer's call. Report claims the repository contradicts, contradictions between pages, placeholders left, and rules the pages break.

If the developer declined the red-team, brief a new surveyor instead: kind Check, with the list of pages written.

Triage each finding with the developer: recommend a fix or decline it, with your reasoning. Apply the fixes they approve, and commit once they confirm.

## 9. Close

1. Ask the developer what the project is working on now that the onboarding is done, and rewrite Current Focus with their answer. Commit once approved.
2. Tell them what was written (each path), what was declined, and what comes next: the next issue follows the Development Workflow they approved.
3. Offer to push the branch and open a pull request. Confirm each action before taking it.

## Rules

- One page at a time. Nothing is written without the developer's approval.
- Never fill a gap with a guess. Anything inferred is labelled as needing the owner.
- Touch only the pages in the plan and the files under `.claude/`. Never edit the project's code, or the clone.
- Write nothing to the agent's memory.
- Confirm every outward-facing action first: a push, a pull request.
