---
title: Refactoring
status: draft-untested
last_updated: 2026-11-16
---

# Refactoring

## When to use it

You want to change the structure of code without changing what it does: split a large module, rename for clarity, remove duplication, move responsibilities.

Not for: code with no tests (run [test backfill](test_backfill.md) first), or version upgrades ([dependency migration](dependency_migration.md)).

## Setup

- [ ] Tests exist for the target code and pass.
- [ ] The working tree is clean.
- [ ] You are on a branch made for this work.
- [ ] `AGENTS.md` lists the test command (see [codebase onboarding](codebase_onboarding.md) if there is none).

## Steps

1. Pin current behavior ([P4](../principles.md#p4-give-the-agent-a-way-to-check-itself)). If coverage of the target code is thin, write characterization tests: tests that record what the code does today, right or wrong. Commit them on their own, before any restructuring.

   ```
   Write characterization tests for <target code>. Record what it does today, including odd behavior. Do not change production code. Run the tests and confirm they pass.
   ```

2. Research ([P1](../principles.md#p1-context-is-finite), [P7](../principles.md#p7-isolate-noisy-work)). The agent reads the target code and its callers and writes a summary. No changes.

   ```
   Read the code involved in <refactoring goal>. Write research.md: files that matter, how they connect, who calls the public interfaces, risks. Do not change any code.
   ```

3. Plan ([P3](../principles.md#p3-review-where-it-is-cheapest)). The agent turns the research into a plan, and you review it before any code changes. Check that every step preserves behavior and that the out-of-scope list is explicit.

   ```
   From research.md, write plan.md: ordered steps that each preserve behavior, files touched per step, what stays out of scope, how each step is checked. Include an out-of-scope list.
   ```

4. Implement ([P2](../principles.md#p2-fresh-context-per-phase), [P6](../principles.md#p6-small-reversible-steps)). A fresh session works through the plan in small steps, with the tests as the check.

   ```
   Follow plan.md one step at a time. Run the tests after each step and commit. Do not edit any test file. Stop and ask if the plan doesn't fit what you find.
   ```

5. Check ([P4](../principles.md#p4-give-the-agent-a-way-to-check-itself)). Run the done check and read the diff for anything unplanned.

   ```
   Summarize what changed against plan.md. List anything you did that the plan didn't include, and any tests you modified.
   ```

## Pitfalls

- The agent changes behavior while restructuring. Ask for behavior-preserving steps only, and read each diff.
- The agent edits tests to make them pass. Forbid it in the prompt, then run `git diff` on the test paths.
- The agent "simplifies" error handling or removes edge cases. List these as out of scope in the plan.
- Scope creep into unrelated cleanup. Keep an out-of-scope list in `plan.md` and point the agent back to it.

## Done check

- [ ] The same tests pass before and after.
- [ ] `git diff <commit after step 1> -- <test paths>` is empty.
- [ ] Public interfaces are unchanged, unless the plan said otherwise.

## Example

No run recorded yet. Add a link to `examples/` after the first real use.
