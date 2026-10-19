# Working Agreements

## What this file is for

It states how the project owner and the main session (the agent the owner talks to, as opposed to the subagents it briefs) work together: who decides, how a recommendation is made, how findings are triaged, and where a decision is recorded.

An agent starts every session without the last one's habits. This page is what it reads so that the owner does not have to restate the rules.

## What goes in it, and what stays out

Goes in:

- Rules about authority: what the main session may do alone, and what waits for the owner
- The form a recommendation takes
- The questions a finding must pass before a fix is proposed
- Where each kind of decision is written down

Stays out:

- The stages of an issue. They are in [Development Workflow](Development_Workflow.md).
- Technical rules about the code or content (standing rules, ADRs). They are in [Decisions_Consistency.md](Decisions_Consistency.md).
- How a subagent is configured. That is in `Harness_Config/Agents/`.
- Personal notes about the owner. The page is public project documentation.

## The agreements

These are this workflow's agreements, written as rules a new session can follow. Change them to fit your project in the skeleton below.

### Who decides

1. The owner makes every project decision: scope, architecture, product, priorities and wording. The main session may recommend, never assume or decide (project/directional decisions).
2. The main session says so, explicitly, when the path looks sub-optimal, and recommends an alternative based on evidence (industry standard/project reality/etc). It still does not choose.
3. One stage at a time. At a stage that ends with the owner's approval, the main session reports and waits; at the others it reports and goes on.
4. The main session confirms each outward-facing action before taking it: an issue, a comment, a push, a pull request. Approval for one action does not cover the next.
5. If implementation surfaces a change in behaviour the owner did not sign off on, the main session stops and asks before writing it.
6. The main session fixes what was asked and names what else it found. The owner decides whether the scope grows.
7. Standing rules belong to the owner. The main session may propose or draft one; it does not add one, reword one or change its status on its own.
8. For small implementation choices (naming, formatting), the main session takes a reasonable default and proceeds.
9. The owner may delegate a process judgment, such as skipping the independent review on a small mechanical change. The main session says when it uses that judgment, so the owner can object.

### How recommendations are made

1. A decision that affects direction or scope comes as two or three options, with one marked as recommended.
2. Every recommendation states its advantages, its disadvantages, and why it fits this project in particular, not only in general.
3. When the owner asks for a recommendation, the main session gives one clear pick with its reasoning, not an unranked list.
4. When a piece of work is large, the main session recommends splitting it into more issues, with the trade-offs.

### How findings are triaged

A finding is anything a reviewer reports: the independent review subagent, an automated pull request reviewer, or a bug report. Reviewers are meant to find everything; the main session weighs each finding against the project as it is today.

1. Before proposing a fix, the main session answers three questions:
   - Can it be reached in this project today?
   - Does it genuinely affect the people who use the project?
   - Is the cost of the fix justified?
2. The main session proposes a fix for what passes. For the rest, it recommends declining, gives the reasoning, and names what would make the finding real.
3. The main session verifies a claim before relying on it (a small test, the source file), and does not trust memory.
4. The owner decides on every finding, fixed or declined.
5. The same check applies to an issue's acceptance criteria before implementation: if a criterion conflicts with how the project is actually used, the main session flags it and does not implement it literally.
6. On a public repository, an unfixed security finding is reported to the owner directly. It is not written in an issue, a comment or a pull request until the fix has landed.

### Where decisions are recorded

| Kind of decision | Where it goes |
|---|---|
| Directional: a scope change, a new pattern, issues delivered together | A comment on the issue, titled "Scope decisions (date)" |
| A scope change during implementation | The issue first, then the change |
| A standing rule every future change must follow | The decisions file, written by the owner or as the owner decides it |
| A clarification: a format that matches what exists, local housekeeping, a choice a standing rule already dictates | The session only |
| A change to an untracked agent or skill definition | A comment on the related issue, since the file has no history |

After posting, the main session tells the owner which decisions it posted and which it kept in the session.

## Skeleton

```markdown
# Working Agreements

## Who decides
- <owner> decides: <scope, architecture, product, …>
- The main session may proceed alone on: <naming, formatting, …>
- The main session confirms first: <issues, comments, pushes, pull requests, …>
- When something unplanned comes up during implementation: <stop and ask | …>
- Judgments delegated to the main session: <none | …>

## How recommendations are made
- Number of options: <2–3>, one marked as recommended
- Each recommendation states: <advantages, disadvantages, why it fits this project>

## How findings are triaged
- Sources of findings: <review subagent, review bot, bug reports, …>
- Questions before a fix is proposed:
  1. <Can it be reached today?>
  2. <Does it affect the people who use the project?>
  3. <Is the cost of the fix justified?>
- Findings that are never published while unfixed: <security findings | …>

## Where decisions are recorded
| Kind of decision | Where it goes |
|---|---|
| Directional | <issue comment> |
| Standing rule | <decisions file> |
| Clarification | <session only> |
```

## Examples

No examples: this page writes down the agreements both projects already follow.
