CLAUDE.md — Repository guidance for claude-code and subagents

Purpose
-------
This file tells claude-code and local subagents how to work in this repository. It collects the essential project facts, the documents that must be loaded before making changes, the content rules, and the behavioral rules for the main session and all subagents.

Repository facts
---------------
- Repo root: the directory containing `LICENSE`
- GitHub: MatheusCastro99/HarnessConfigAndWorkflow (public)
- Content: Markdown, with Mermaid for diagrams. There is no code to build or compile.
- `Docs/` holds this repository's own documents. `Harness_Config/`, `Templates/` and `Examples/` are the harness configuration and workflow.
- Source projects this repository draws from (both public): MatheusCastro99/BabyBuddyHelper (.NET MAUI) and MatheusCastro99/InvoiceMe (MERN).

Authoritative docs (always load before making edits)
---------------------------------------------------
When planning or making changes, the agent MUST read these files first and follow them:
- Docs/README.md
- Docs/Project_Vision.md
- Docs/Project_Roadmap.md
- Harness_Config/AI_CONTEXT.md
- Harness_Config/Context/*
- The GitHub issue being worked and its comments (`gh issue view <n> --comments`); the owner records decided scope there.

Workflow
--------
Every issue goes through these stages, in order. Say which stage we are in when reporting.
1. Gather all relevant information.
2. Settle open questions and decisions. (owner's approval)
3. Plan the issue's sub-phases. (owner's approval)
4. Plan the implementation of each sub-phase. (owner's approval: the go-ahead to implement)
5. Implement one sub-phase.
6. Test and refine. Commit the sub-phase once its checks pass, and report it.
7. Open a PR, and monitor CI and comments with Auto-fix on. (owner's approval: the push and the PR)
8. Last pass and red-team scan. Starts as soon as the PR is verified open.
9. Fix comments and findings: triage each one. (owner's approval)
10. Historian doc pass. (owner's approval)
11. Ready to merge: a note that the PR is ready.
12. Memory flush, only at an epic's close-out or after an isolated issue. (owner's approval)

Loops: stage 4 repeats for every sub-phase; stages 5 and 6 repeat for every sub-phase; the fixes approved at stage 9 loop back to stage 4, at most twice. Details in `Harness_Config/Context/Development_Workflow.md`.

At a stage marked (owner's approval), report and wait; at the others, report and go on. Do not jump a stage. A scope change during implementation goes into the issue before the content.

AI tooling (Claude Code)
------------------------
Runnable definitions live in `.claude/agents/` and `.claude/skills/` (gitignored, maintainer's personal tooling). Copy-ready versions for readers live in `Templates/`, and their documentation in `Harness_Config/`.

Subagents:
- red-team — independent adversarial reviewer, read-only. Checks a finished change for claims the source projects do not support, private details, leftover placeholders, broken links and contradictions between pages.
- historian — pre-merge doc updater for `Docs/`. Applies the main session's stale-docs list, checks each item against the repository, reports anything beyond the list without editing it. Never commits.

Subagent invocation
-------------------
- Brief the subagent with: goal (issue number and decided scope), target (branch, commit range or PR), constraints (out-of-scope items), and expected deliverable.
- Agents and skills recommend; the maintainer makes every decision.
- Always return a concise summary and list of modified files before committing.

Content rules
-------------
- Every `Harness_Config/` page has the same shape: what the file is for; what goes in it and what stays out; a skeleton to fill in; links to the matching examples in `Examples/`.
- Describe what the source projects actually do. Check a claim against the source repository before writing it; do not describe a practice neither project follows.
- Where the two projects differ, show both; do not justify the differences.
- An example links to its source file at a named commit.
- A template definition must run in Claude Code once its placeholders are filled. List every placeholder at the top of the template.
- Link only to files that exist. A path that arrives in a later phase is written as plain text until then.
- Keep the owner's wording. Do not rewrite sentences the owner edited; report a typo instead of fixing it unasked.
- Prefer small, plain pages. Do not add sections, files or structure the issue did not ask for.

Documentation rules
-------------------
- The main session keeps a running stale-docs list per PR (ID, file and location, what's stale, what it should say, evidence).
- Right before merge, the historian subagent applies the list; the maintainer reviews its diff against the list and the change.
- Keep `Docs/` consistent with reality: update the README status table, the PRD structure and the roadmap when a phase ships.

Branching and commits
---------------------
- One issue, one branch, one PR. Planning work uses `planning/<issue>-<name>`; other work uses `docs/<issue>-<name>`.
- One commit per sub-phase, with a message that names the issue: `docs: add README (#2)`.
- Never commit to `main` directly after the root commit.

Safety and privacy
------------------
- The repository is public. Do not publish secrets, personal notes about the owner, or unfixed security findings from either source project.
- Session notes and memory files are sources for rules, not text to copy. Restate a rule in general terms.

Contacting the user
-------------------
- For decisions that affect direction or scope, present options (2–3) with trade-offs, mark one as recommended, and wait.
- Confirm each outward-facing action (issues, comments, pushes, PRs) before taking it.
- For small implementation choices (naming, formatting) prefer reasonable defaults and proceed.

Change log
----------
- 2026-10-13 (#2): Initial CLAUDE.md added.
- 2026-10-16 (#14): Repository renamed to HarnessConfigAndWorkflow and `AI_Env/` to `Harness_Config/`; content rules aligned with the PRD.
- 2026-10-19 (#19): Workflow tuned to 12 stages, with approval gates and loops.
