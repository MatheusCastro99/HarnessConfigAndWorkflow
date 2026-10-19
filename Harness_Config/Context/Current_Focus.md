# Current Focus

## What this file is for

It says what the project is working on now: its status, the current phase or epic, what comes next, and what is unfinished on purpose.

The main session reads it to know where an issue sits in the larger plan. The [guardrails review](../Skills/Guardrails_Review.md) skill reads it so that it does not report a gap the project has left open on purpose.

## What goes in it, and what stays out

Goes in:

- The status of the project, in a few words, such as a prototype in active development
- The current phase or epic, with its sub-issues in order, each marked shipped, in progress, next or planned
- The next issue
- What is unfinished on purpose, and the issue that will finish it
- Work outside the epic that changes what comes next
- The open issues, grouped by the phase they belong to
- A link to the roadmap

Stays out:

- The full plan, and later phases in detail. They are in the roadmap.
- The plan and the decisions of the issue in progress. They live in the issue.
- The structure of the project. That is in the [architecture document](Architecture_Design.md).
- Standing rules. They are in [Decisions and Consistency](Decisions_Consistency.md).

## How often it changes, and who updates it

- **In every issue that changes it.** When the issue's work makes the page untrue, the main session adds an entry to the stale-docs list for this page. The historian applies it in the doc pass, and the owner approves the diff ([Development Workflow](Development_Workflow.md), stage 10).
- **When a phase or epic is planned.** The planning pull request updates this page before the first issue starts ([Development Workflow](Development_Workflow.md), "Rules for every stage").

Nothing else changes it. If the page falls out of date between those two moments, that is an entry on the stale-docs list.

## Skeleton

Copy the page outline and replace the text in angle brackets. Repeat a sub-issue line for each sub-issue of the epic, delete a section the project has nothing for, and delete the comment under the sub-issues.

Placeholders: `<date>`, `<status>`, `<phase or epic>`, `<epic issue>`, `<n.n>`, `<name>`, `<issue>`, `<state>`, `<path>`, and the text in angle brackets in the outline.

```markdown
# Current Focus

Last updated: <date>

Status: <status>

## <phase or epic> (<epic issue>)

Sub-issues, in order:
- <n.n> <name> (<issue>): <state>. <What it delivers, in one line.>
<!-- <state> is one of: shipped | in progress | next | planned -->

Next: <issue>

Unfinished on purpose:
- <What is not built yet, and the issue that builds it.>

## Outside the epic
- <issue>: <what it changes about what comes next>

## Open issues
- <phase or group>: <issue> <title>, <issue> <title>

The full plan is in the [Roadmap](<path>).
```

## Examples

Examples: [BabyBuddyHelper](../../Examples/BabyBuddyHelper-examples.md#current-focus).
