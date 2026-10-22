# Project Vision

## Summary

HarnessConfigAndWorkflow is study material for harness configuration and development workflow. It documents how I work with an AI coding agent on a real project:
the context it reads, the rules it follows, the subagents and skills it uses, and the steps every issue goes through.

---

The approach grew on two projects: BabyBuddyHelper (.NET MAUI) and InvoiceMe (MERN).
It works on both, but it is only written down inside them, mixed with each project's own details.

This repository pulls it out into one place, so that:

- Someone studying harness engineering can read how it works, see it applied on two projects, and start their own.
- Each step stays small and self-contained, and its context is written down, so it can be understood on its own.

## What the approach is

- The owner decides. Agent recommendations come with trade-offs, and the agent says so explicitly when the path looks sub-optimal.
- Context is written down. The agent loads the project's own documents before it plans or edits anything.
- Decisions are authoritative standing rules. A reviewer can check a change against them.
- Every issue goes through the same stages, in order. The owner approves at fixed gates: the decisions, the plans, the pull request, the fixes and the documentation.
- Review is independent. A subagent with no stake in the change and no biased context tries to break it and give an adversarial review before the change is merged.
- Documentation is part of the change. What a change makes stale is tracked while it happens on a running list and fixed before the merge.
- Simple first. Add structure when the project needs it, not before.

## What this repository is

- Study material for harness configuration and development workflow: each piece explains what it is for and gives a skeleton to fill in.
- A set of real examples: the same piece as it was filled in on two projects.
- Built with the workflow it documents.

## What it is NOT

- A framework, a library or a tool to install.
- A claim that this is the only way, or the best way, to work with an agent.
- Tied to one stack. The examples are .NET MAUI and MERN; this repository is neither.
- A replacement for the owner's judgment. Agents and skills recommend; the developer makes every call.
- A production workflow. It favors written context and approval gates over speed and token use.

## Target feeling

Think:

- A senior colleague's project notes, tidy enough to hand to a new teammate

rather than:

- A methodology with a certification
