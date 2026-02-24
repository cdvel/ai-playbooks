---
title: Dependency migration
status: draft-untested
last_updated: 2026-11-16
---

# Dependency migration

## When to use it

You are upgrading a framework, a language version or a major dependency, and the new version has breaking changes.

Not for: structural changes unrelated to the upgrade ([refactoring](refactoring.md)).

## Setup

- [ ] Tests pass on the current version.
- [ ] The lockfile is committed.
- [ ] You are on a branch made for this work.
- [ ] You know the target version.

## Steps

1. Research ([P1](../principles.md#p1-context-is-finite)). The agent reads the changelog and migration guide for the target version and lists the breaking changes that affect this codebase, with file references. No changes.

   ```
   Read the changelog and migration guide for <dependency> <current version> to <target version>. Write research.md: each breaking change that affects this codebase, the files it touches, and anything that needs a decision. Skip changes that don't apply. Do not change any code.
   ```

2. Plan ([P3](../principles.md#p3-review-where-it-is-cheapest)). The agent orders the changes and says whether to upgrade in one jump or through intermediate versions. You review before any code changes.

   ```
   From research.md, write plan.md: one jump or intermediate versions and why, the ordered code changes, files touched per step, what stays out of scope, and how each step is checked. Do not add or remove other dependencies.
   ```

3. Implement ([P2](../principles.md#p2-fresh-context-per-phase), [P6](../principles.md#p6-small-reversible-steps)). A fresh session works through the plan in small steps.

   ```
   Follow plan.md one step at a time. Run the build and tests after each step and commit. Fix the cause of each deprecation warning instead of silencing it. Stop and ask if the plan doesn't fit what you find.
   ```

4. Check ([P4](../principles.md#p4-give-the-agent-a-way-to-check-itself)). Run the done check, and read the lockfile diff.

   ```
   Summarize what changed against plan.md. List every dependency added, removed or re-pinned, every warning suppressed, and anything you did that the plan didn't include.
   ```

## Pitfalls

- Silencing deprecation warnings instead of fixing their cause. Search the diff for new ignore rules and suppression flags.
- Pinning or downgrading other packages to get around a problem without saying so. Ask the agent to list every re-pinned package.
- Adding dependencies the plan didn't mention. Review the lockfile diff line by line.
- Mixing the upgrade with unrelated cleanup. Keep unrelated changes out of the branch.

## Done check

- [ ] The build and tests pass on the new version.
- [ ] No warnings were suppressed to get there.
- [ ] The lockfile diff contains only expected changes.

## Example

No run recorded yet. Add a link to `examples/` after the first real use.
