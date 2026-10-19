# Historian

## What this file is for

It documents the `historian` subagent: the documentation updater that runs right before a merge.

Documentation goes stale in the gap between the code changing and someone updating the docs. While it works on an issue, the main session keeps a running [stale-docs list](../../Templates/stale-docs.md) of every statement its change made untrue. The historian turns that list into edits, so the owner reviews documentation changes instead of writing them.

Its value is **a cross-check between three parties**:

- The main session writes the list from the implementation.
- The historian checks each entry against the code before applying it, and sweeps for anything the list missed.
- The owner reviews the historian's diff against the list and the change.

If one of them makes a mistake, another is positioned to catch it. What the historian reports beyond the list is something the main session missed. What it refuses to apply is an entry the main session got wrong. What the owner finds in the diff is something both missed.

## What goes in it, and what stays out

Goes in the definition:

- Its role as an editor, not an author
- The inputs it expects, and the rule that it stops when there is no list
- The process: load context, verify each entry, apply, sweep, draft rule candidates
- The hard rules: where it may edit, what it may do in the decisions file, read-only Bash
- The format of its report

Stays out:

- **The list itself.** The main session builds it during the work. The historian does not build one from scratch.
- **Authoring.** A new document is written by the main session with the owner. The historian has no tool to create a file.
- **The agent's own tooling.** The agent guidance file and the definitions in `.claude/agents` and `.claude/skills` stay with the main session and the owner.
- **Decisions and commits.** The owner confirms every finding beyond the list and makes every call on a standing rule. The main session commits after the owner's review.

## When to use it, and when not to

Use it at stage 10 of the [Development Workflow](../Context/Development_Workflow.md): after CI, the red-team scan and the fixes, once the change is final, and with a stale-docs list in hand.

Do not use it:

- While the code is still changing. The docs would go stale again.
- Without a list
- To write a new document

## Configuration

| Field | Value | Why, and the trade-off |
|---|---|---|
| `tools` | Read, Grep, Glob, Edit, Bash | Edit applies small changes in place. There is no Write, so it cannot create a file or overwrite a whole one. Bash is for read-only `git` and `gh` inspection. The trade-off: "edit only the documentation" and "read-only Bash" are enforced by the prompt, not by permissions. |
| `model` | sonnet | The work is bounded and driven by the list: verify a fact, apply a small edit. Depth matters less here than for the red-team, and each pass costs less. The trade-off is a slightly higher chance of a miss in the sweep, which the owner's review covers. |
| `effort` | medium | The same reason, and the same trade-off |
| `skills` | none | The rules it needs are in the documents it reads |
| `color` | blue | Display only |
| No `Agent` tool | | It cannot spawn other agents. It returns one report. |

## The rules it follows

| Rule | Where it comes from |
|---|---|
| It applies only the listed entries. Anything else is reported and waits for the owner. | The cross-check: every edit starts from an entry the main session wrote and the owner can review |
| The code wins. An entry that does not match the code is left unapplied and reported with evidence. | The same |
| It checks every fact in a section it edits, not only the listed ones | BabyBuddyHelper's first run left a stale fact untouched inside a section it had just edited |
| It reports every adaptation of the suggested text, including a change of format | The same run adapted a format without saying so, and the report no longer matched the diff |
| It starts from a `git ls-files` snapshot and compares every listed set against it in both directions | The second run missed an item that was absent from a list, not wrong in it |
| It checks the decisions file against the change and reports rule text made untrue | On InvoiceMe, a rule contradicted by the historian's own edit was caught only by an automated reviewer |
| It keeps the owner's voice: small edits in the surrounding style, nothing reflowed outside the listed location | The documents are the owner's |
| It never commits | The main session commits after the owner's review |

In the decisions file it may correct a listed factual detail inside an existing rule, such as a path or a name. It never changes a status, and never adds, removes or renumbers a rule. A candidate for a new rule comes back as a draft in its report.

## What to brief it with

- **Target:** the branch or pull request, with the change final
- **The stale-docs list:** each entry with its ID, file and location, what is stale, what it should say, and the evidence
- **Rule candidates,** if any
- **The owner's notes** on entries already rejected or changed

## What it returns

A summary count, then:

- the entries it applied, with any adaptation of the suggested text
- the entries it did not apply, each with the reason and the evidence
- what it found beyond the list, not edited
- rule drafts, not written
- the files it touched

The report must match the diff exactly, because the owner reviews one against the other. The counts go into the stale-docs list's cross-check line when the entries are closed.

## How the two projects differ

InvoiceMe's historian was adapted from BabyBuddyHelper's.

| | BabyBuddyHelper | InvoiceMe |
|---|---|---|
| Beyond the list | Reports it and waits for the owner | Fixes what it can verify. Reports what it cannot verify, what is outside its scope, and anything where the wording is a judgment call. |
| Decisions file | May correct a listed factual detail. Never changes status, adds, removes or renumbers. | Never writes it, not even a factual correction. Reports rule text the change made untrue. |
| Report | Applied, not applied, found beyond the list, rule drafts, files touched | Opens with a map from each change in the diff to the doc update it caused, or to "no doc impact". Lists what it fixed beyond the list in place of what it found, and adds the stale code comments it hands back to the main session. |
| Deleting a section | Only when the list says so | Also when what the section documents no longer exists; every deletion is reported |

The template follows BabyBuddyHelper on all four rows. From InvoiceMe it takes one thing: the sweep also checks the decisions file against the change, and reports what it finds.

## Skeleton

The copy-ready definition is [Templates/agents/historian.md](../../Templates/agents/historian.md). Copy it to `.claude/agents/historian.md`, fill the placeholders listed in its opening comment, and delete that comment.

| Placeholders | What they hold |
|---|---|
| `<project>` | The project's name |
| `<context-index>`, `<decisions-doc>` | The paths of the page an agent loads first and of the file that holds the standing rules |
| `<base-branch>` | The branch pull requests merge into |
| `<docs-paths>` | The documentation it may edit |
| `<never-edit>` | What it must not touch besides code |
| `<set-examples>` | The kinds of sets the documents list |

## Examples

Examples: [BabyBuddyHelper](../../Examples/BabyBuddyHelper-examples.md#historian), [InvoiceMe](../../Examples/InvoiceMe-examples.md#historian).
