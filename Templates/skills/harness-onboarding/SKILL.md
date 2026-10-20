---
name: harness-onboarding
description: Onboards this project into the HarnessConfigAndWorkflow harness configuration and workflow. Surveys the repository through the read-only surveyor agent, recommends the smallest set of pages the project needs, and drafts the pages with the developer, who approves them once per step. Run it once per project, with /harness-onboarding.
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

The words in square brackets inside the follow-up document's skeleton are filled in as
the skill runs, not placeholders; leave them.

`disable-model-invocation: true` means the skill runs only when you type
/harness-onboarding. It writes many files, so it never starts on its own.
-->

# Harness Onboarding

You onboard this project into the harness configuration and workflow kept in the clone at `<harness-repo-path>`. You tailor it with the developer; you do not install it. The pages are drafted with the developer, and each step's pages are committed only once they approve the step.

You recommend; the developer decides. When a path looks sub-optimal, say so, and still let them choose.

## Sources

| Source | What you take from it |
|---|---|
| `<harness-repo-path>/Harness_Config/` | For each page: what it is for, what goes in and what stays out, and the skeleton your draft starts from |
| `<harness-repo-path>/Templates/` | The copy-ready agents and skills, and the stale-docs list |
| `<harness-repo-path>/Examples/` | How two projects filled the pages in: the level of detail to aim for. Never copy their content. |
| `<harness-repo-path>/.claude/CLAUDE.md` | The model for the agent guidance file, which has no skeleton of its own |
| `<harness-repo-path>/Docs/` | The model for the project documents (vision, requirements, roadmap), which have no skeleton of their own |
| The surveyor's reports | What this repository shows |
| The developer | Everything only the owner knows |

Read the clone; never edit it. Leave out what belongs to HarnessConfigAndWorkflow itself: its issue numbers, its own decisions, its file paths.

## The follow-up document

Never put in a page or a step report what the developer has not confirmed, or what you notice outside the onboarding's job. Write it in the follow-up document: one file, kept out of version control, that the developer takes into a later session. Its default path is `.claude/onboarding-follow-up.md`; the onboarding plan settles it. Create it at its first entry, from this skeleton. Never commit it, and no page links to it.

```markdown
# Onboarding follow-up

Left open by the harness onboarding on [date]. Kept out of version control.
Take it into a new session: answer each question, decide each note, and update the page it names.

## Questions for the owner
- Q1 · [page] · [what is not confirmed] · [the question]

## Noticed outside the onboarding
- N1 · [file:line] · [what was seen]
```

## Checkpoints

Steps 1 to 3 each end at a checkpoint, where the developer approves the step. By default it is the step's only stop. If the developer asks to approve page by page, at the start or at any time, show each page before going on to the next.

Before each checkpoint, brief a new surveyor, kind Check:

- the pages written in the step, by path;
- for each page, the page in `<harness-repo-path>/Harness_Config/` it starts from, or, for a page with none, its model under Sources, with no "Stays out" check;
- what the developer told you, in brief: it is their call and is not checked;
- the stale-docs list's placeholders stay until each pull request fills them; they are not reported.

Fix what it finds before the checkpoint: a contradiction between pages, a claim the repository contradicts, a placeholder left. Content outside a page's job moves to the follow-up document. What needs the developer becomes a decision at the checkpoint.

A checkpoint shows, in this order:

1. **A digest of every page written in the step,** 3 to 5 lines each: what the page covers, its key facts or rules (for Decisions and Consistency, each ADR's title and status), and the IDs of what it left in the follow-up document.
2. **The decisions left to the developer,** numbered, each with your recommendation.
3. **One line:** the number of entries added to the follow-up document in this step. Don't list them.

Show any page in full when the developer asks. Apply the decisions they make, then commit.

## 1. Explain the whole flow first

Before anything else, tell the developer, in one short message:

- **The flow:** a survey of the repository, a recommended set of pages, then four steps (Documentation, Skills, Agents, Review), then a pull request.
- **Their approval:** once per step. Each step ends at a checkpoint: a short digest of every page written in it, and the decisions left to them. Nothing is committed before they approve it. If they prefer to approve page by page, they can ask for it now or at any time.
- **What you will ask them:** what only they know: the vision, the intent behind the interface, how they work with the agent, and what they are working on now.
- **What stays open:** what they have not confirmed, and anything you notice outside the onboarding, goes into a follow-up document they take into a later session, not into the pages.
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
- To check a claim, send the surveyor a follow-up or read the few files the claim names, never the whole codebase.

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

Sum it up as the onboarding plan: the pages, their paths, the order, and the follow-up document's path. Wait for the developer's approval.

## 5. Step 1: Documentation

Draft the chosen pages in this order: Architecture Design, Data Flow, Decisions and Consistency, UI Guidelines, Working Agreements, Development Workflow, Current Focus, the project documents, AI Context, and the agent guidance file last, since it points to the others.

For each page:

1. Read its page in `Harness_Config/`, or its model under Sources, and the matching example in `Examples/` if there is one.
2. Draft it from its skeleton or model, with the survey's facts and the developer's answers only. What neither of them gives you stays out of the page: if the page needs it now, it is a decision at the checkpoint; otherwise it is a question in the follow-up document. A section with nothing confirmed is deleted, as the skeletons say.
3. Write it, then go on to the next page. Stop to show it only if the developer asked to approve page by page.

Page by page:

- **Decisions and Consistency:** turn the patterns the survey found into candidate rules. The developer decides each rule and its status. The rules are theirs. A candidate rule they have not decided is a numbered decision at the checkpoint; it goes into the follow-up document only if they put it off.
- **Development Workflow:** start from the clone's stages. Which the developer keeps, changes or drops is a decision at the checkpoint. Leave out the clone's references to its own issues.
- **Current Focus:** name the onboarding as the current work, with its four steps, and list the steps not done yet as unfinished on purpose. Link to this skill rather than repeating its process. The page is rewritten at the close.

At the end of the step, hold the checkpoint. Once the developer approves, apply their decisions, move this step out of Current Focus's unfinished list, and commit the pages.

## 6. Step 2: Skills

1. Copy `Templates/skills/guardrails-review/SKILL.md` to `.claude/skills/guardrails-review/SKILL.md`, and the ux-design skill if it was chosen.
2. Fill every placeholder its opening comment lists, from the pages just written and the survey. A known regression trap comes only from the developer or the repository; if there is none, write "None recorded yet." If the developer declined a page the skill loads, remove that line.
3. Delete the opening comment, and write the filled skill.

Hold the checkpoint. Once the developer approves, apply their decisions, move this step out of Current Focus's unfinished list, and commit the step's tracked files. Files under `.claude/` that the developer keeps untracked are not committed.

## 7. Step 3: Agents

1. Copy `Templates/agents/red-team.md` to `.claude/agents/red-team.md`, and the historian if it was chosen.
2. Fill the placeholders, delete the opening comment, and write each file. If the developer declined guardrails-review, remove the `skills:` field from the red-team, and replace its paragraph about the preloaded skill, under "Review process", with the documents to load before reviewing.
3. If the stale-docs list was chosen, copy `Templates/stale-docs.md` to a path the developer picks, kept out of version control as its opening comment says. Its placeholders stay until each pull request fills them.

Claude Code picks up a new agent file within seconds, as long as `.claude/agents/` existed when the session started. If it did not, or if `red-team` is still not available at the review, ask the developer to restart the session and resume it.

Hold the checkpoint. Once the developer approves, apply their decisions, move this step out of Current Focus's unfinished list, and commit the step's tracked files. Files under `.claude/` that the developer keeps untracked are not committed.

## 8. Step 4: Review

Brief the red-team, if it was written:

- **Goal:** the onboarding pages for this project, as the developer approved them
- **Target:** every file written during the onboarding, listed by path, including any under `.claude/` that git does not track, reviewed as a design document, except the follow-up document
- **Known gaps:** the follow-up document, by path. What it lists is known and left open on purpose; don't report it again.
- **Constraints:** owner-only content is the developer's call. Report claims the repository contradicts, contradictions between pages, placeholders left (except in the stale-docs list, whose placeholders are filled per pull request), and rules the pages break.

If the developer declined the red-team, brief a new surveyor instead: kind Check, with the same brief as before each checkpoint for every page written, and the follow-up document as known gaps.

Triage each finding with the developer: recommend a fix or decline it, with your reasoning. Apply the fixes they approve, and commit once they confirm.

## 9. Close

1. Ask the developer what the project is working on now that the onboarding is done, and rewrite Current Focus with their answer. Commit once approved.
2. Tell them what was written (each path), what was declined, and what comes next: the next issue follows the Development Workflow they approved.
3. Give them the follow-up document's path and the number of entries in it, and suggest they take it into a new session.
4. Offer to push the branch and open a pull request. Confirm each action before taking it.

## Rules

- One approval per step, at its checkpoint, unless the developer asks for one per page. Nothing is committed without the developer's approval.
- Never fill a gap with a guess. What the developer has not confirmed goes into the follow-up document, not into a page.
- A page holds only what its skeleton or model asks for.
- Touch only the pages in the plan and the files under `.claude/`. Never edit the project's code, or the clone.
- Write nothing to the agent's memory.
- Confirm every outward-facing action first: a push, a pull request.

## Never

- Never put in a page what its harness page lists under "Stays out", or anything its skeleton or model does not ask for.
- Never report defects, bugs or improvement ideas in a page or a step report. You are not reviewing the code: write what you saw in the follow-up document and go on.
- Never mark a page "needs the owner" or the like, and never give an ADR a status the ADR format does not define.
- Never read the whole codebase to verify the survey.
- Never fix, tidy or refactor anything outside the pages, even when asked in passing; note it in the follow-up document instead.
- Never pad a report: no lists of everything you noticed, no repeated summaries, no step ahead without its approval.
- Never use the harness's terms unexplained: name a page by what it does the first time you mention it.
