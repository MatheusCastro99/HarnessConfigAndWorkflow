# Red Team

## What this file is for

It documents the `red-team` subagent: an independent, adversarial reviewer that tries to break a finished change before the owner sees it.

Its value is **independence**. The main session wrote the change, which makes it the worst-placed reviewer of it. The red-team starts in a fresh context with no stake in the work, assumes the change can be broken, and reports only what is worth fixing, each finding scored and backed by evidence.

That independence is also why it is a subagent and not a skill. A subagent rebuilds its context from nothing, which costs time and tokens on every run. For a review, the clean context is the point. For the other lenses (the project checklist, the interface review), rebuilding context costs more than it returns, so they run inline as skills.

## What goes in it, and what stays out

Goes in the definition:

- Its role, and the rule that it is read-only
- The inputs it expects, and what to do when the goal is missing
- The review process: goal, architecture, the attempt to break the change, and a check of its own findings
- The scoring formula, the priority bands and the output format
- The limit on re-reviews

Stays out:

- **The project's rules and known traps.** They come from the preloaded [guardrails-review](../Skills/Guardrails_Review.md) skill and the documents that skill names.
- **Documentation review.** The red-team reads the documents to learn the rules; it does not review them or list stale docs. That belongs to the main session's stale-docs list and the [historian](Historian.md).
- **Decisions.** It recommends. What happens with each finding is triaged by the main session and decided by the owner, as described in [Working Agreements](../Context/Working_Agreements.md).

## When to use it, and when not to

Use it:

- At stage 8 of the [Development Workflow](../Context/Development_Workflow.md), on the finished change
- When a design needs an independent challenge before it is built

Do not use it:

- On a small, mechanical change, where rebuilding the context costs more than the review returns. Skipping the scan is the owner's call unless they delegated it ([Working Agreements](../Context/Working_Agreements.md), "Who decides", rule 9).
- On work the main session still has open. It reviews finished work, not work in progress.

## Configuration

| Field | Value | Why, and the trade-off |
|---|---|---|
| `tools` | Read, Grep, Glob, Bash | No Edit and no Write, so it cannot change a file through a tool. Bash is there for `git` and `gh` inspection and for running the build and the tests. The trade-off: "read-only" for Bash is enforced by the prompt, not by permissions. |
| `model` | opus | Adversarial review is where depth matters most. The trade-off is the cost of each run. |
| `effort` | high | The same reason, and the same trade-off |
| `skills` | guardrails-review | It reviews against the project's rules and known traps, not generic taste. The trade-off: the agent depends on that skill existing under that name. |
| `color` | red | Display only |
| No `Agent` tool | | It cannot spawn other agents. It returns one report. |

## What to brief it with

- **Goal:** the issue number and its decided scope
- **Target:** a branch, a commit range, a pull request or a design document
- **Constraints:** the standing rules in play, and what is out of scope
- **Prior findings,** on a re-review

It knows nothing about the session. If the goal is missing it reads the issue and its comments, and if it still cannot tell what "done" means, that is its first finding.

## What it returns

A verdict on three dimensions (goal, architecture, implementation) and one recommendation: approve, approve with changes, or rework recommended. Then the findings, the build and test results, edge cases for the owner's manual check, and problems next to the change that already existed.

### Scoring

Before a finding is scored it has to survive five questions: is there `file:line` evidence, what actually happens to the people affected, is it a real problem or a preference, is it inside this change, and would a senior engineer on a project of this size prioritize it.

Each surviving finding is rated from 1 to 5 on Severity, Confidence, Impact and Fix cost.

**Priority = Severity + Confidence + Impact − Fix cost**

| Score | Priority | Meaning |
|---|---|---|
| 12-14 | Critical | Should block the merge |
| 10-11 | High | Fix before merge unless there is a justification |
| 7-9 | Medium | Strong recommendation |
| 4-6 | Low | Note it; do not block |
| 3 or less | Discard | Not reported |

Fix cost is subtracted, so a real but expensive fix ranks below a cheap one of the same weight. Some findings are escalated whatever their score: data loss or corruption, exposed secrets, and what the project adds to that list.

"No findings above 3" is a valid result.

### Re-reviews

The same change is reviewed at most twice. A re-review checks the previous findings, the newly changed code and the side effects of the fixes; it does not repeat the full review unless the architecture changed. After the second cycle the red-team reports what remains and stops.

## How the two projects differ

Both projects run the same agent with the same settings, process, scoring and limit. InvoiceMe's was adapted from BabyBuddyHelper's, with the probes rewritten for its stack.

| | BabyBuddyHelper | InvoiceMe |
|---|---|---|
| When it runs | Before a large or risky pull request is handed to the owner | At step 9 of the issue workflow, as the last pass before the pull request goes to the owner |
| Stale docs | Documentation is read-only reference. The report has no section for it. | The report ends with "Docs made stale", which feeds the stale-docs list |
| Probe scripts | Not mentioned | It may write throwaway probe scripts, only in the operating system's temporary directory |
| Results section | Build | Verification: the commands run and their results |

On the first row this workflow follows InvoiceMe: the scan has a fixed place at stage 8, and skipping it for a small change is a judgment the owner makes or delegates. On stale docs and probe scripts the template follows BabyBuddyHelper. It names its results section "Build and tests".

## Skeleton

The copy-ready definition is [Templates/agents/red-team.md](../../Templates/agents/red-team.md). Copy it to `.claude/agents/red-team.md`, fill the placeholders listed in its opening comment, and delete that comment. The guardrails skill must be in place first.

| Placeholders | What they hold |
|---|---|
| `<project>`, `<project-kind>` | The project's name, and its size and kind as the measure for justified complexity |
| `<build-command>`, `<test-command>` | The commands it may run |
| `<decisions-doc>` | The path of the file that holds the standing rules |
| `<probe-area>`, `<probes>` | One line per group of ways to break a change in this stack |
| `<who-is-affected>` | Whose data or experience a defect reaches |
| `<always-escalate>` | What is reported whatever its score |

## Examples

Examples: [BabyBuddyHelper](../../Examples/BabyBuddyHelper-examples.md#red-team), [InvoiceMe](../../Examples/InvoiceMe-examples.md#red-team).
