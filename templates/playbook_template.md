---
title: <Playbook name>
status: draft-untested
last_updated: 2026-11-16
---

# <Playbook name>

## Scope

*Two or three lines on the task this fits. End with a "Not for" line naming the nearest other playbook.*

Not for: <task>, use <other playbook> instead.

## Setup

*A short checklist of what must be in place before starting: repo state, tests, context files such as `AGENTS.md`.*

- [ ] <thing that must be true>

## Steps

*Numbered steps. Each has a name, one or two sentences on what happens, the prompt in a code block, and the principle IDs it applies. Change or add steps where the task needs it.*

1. Research ([P1](../principles.md#p1-context-is-finite), [P7](../principles.md#p7-isolate-noisy-work)). The agent reads the relevant code and writes a summary. No changes.

   ```
   Read the code involved in <task>. Write research.md: files that matter, how they connect, risks. Do not change any code.
   ```

2. Plan ([P3](../principles.md#p3-review-where-it-is-cheapest)). The agent turns the research into a plan. The human reviews it before any code exists.

   ```
   From research.md, write plan.md: ordered steps, files touched per step, what stays out of scope, how each step is checked.
   ```

3. Implement ([P2](../principles.md#p2-fresh-context-per-phase), [P6](../principles.md#p6-small-reversible-steps)). A fresh session works through the plan in small steps.

   ```
   Follow plan.md one step at a time. Run the tests after each step and commit. Stop and ask if the plan doesn't fit what you find.
   ```

4. Check ([P4](../principles.md#p4-give-the-agent-a-way-to-check-itself)). Run the done check and read the diff for anything unplanned.

   ```
   Summarize what changed against plan.md. List anything you did that the plan didn't include, and any tests you modified.
   ```

## Pitfalls

*Three to five items. Each names what goes wrong and how to steer the agent back.*

- <what goes wrong>. <how to steer it back>.

## Done check

*A short checklist that is observable: a command passes, a diff is empty, a file exists.*

- [ ] <observable condition>

## Example

No run recorded yet. Add a link to `examples/` after the first real use.
