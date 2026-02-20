---
title: Legacy redevelopment
status: draft-untested
last_updated: 2026-11-16
---

# Legacy redevelopment

## When to use it

You are modernizing or rebuilding an old codebase piece by piece, while the old system keeps running. The work is a series of slices, each with its own plan and review.

Not for: a small structural change ([refactoring](refactoring.md)), or rebuilding without reference to the original code ([clean-room implementation](clean_room_implementation.md)).

## Setup

- [ ] The system builds and runs locally.
- [ ] `AGENTS.md` exists. If not, run [codebase onboarding](codebase_onboarding.md) first.
- [ ] You have some way to compare old and new behavior on the same inputs: recorded requests, sample data, or tests.
- [ ] Tests exist for the area you will touch, or [test backfill](test_backfill.md) has been run on it.

## Steps

Repeat steps 2 to 4 for each slice. Step 1 is done once and updated as you learn.

1. Map the system ([P1](../principles.md#p1-context-is-finite), [P7](../principles.md#p7-isolate-noisy-work)). The agent writes a domain map: what the system does, its entry points and its data flows. No changes. Add odd behavior to the map as you find it.

   ```
   Read the code involved in <system or area>. Write domain_map.md: what the system does, entry points, data flows, external dependencies, and any behavior that looks odd or undocumented. Do not change any code.
   ```

2. Pick a seam and a slice ([P3](../principles.md#p3-review-where-it-is-cheapest)). A seam is a boundary where new code can take over one route or function while the old code keeps running. This is the strangler fig pattern: the new system grows around the old one and replaces it one piece at a time. You review the plan before code exists.

   ```
   From domain_map.md, propose three candidate seams for the next slice. For the one I choose, write plan.md: the slice, how old and new paths coexist, how to compare their results, what stays out of scope, and the steps in order.
   ```

3. Implement the slice ([P2](../principles.md#p2-fresh-context-per-phase), [P6](../principles.md#p6-small-reversible-steps)). A fresh session builds the new path from the plan. The old path stays in place.

   ```
   Follow plan.md one step at a time. Keep the old path working and untouched. Run the tests after each step and commit. Stop and ask if the plan doesn't fit what you find.
   ```

4. Check the slice ([P4](../principles.md#p4-give-the-agent-a-way-to-check-itself)). Compare old and new on the same inputs, then update the map.

   ```
   Run old and new paths on <inputs> and compare the results. Summarize differences against plan.md, list anything you did that the plan didn't include, and update domain_map.md with what you learned.
   ```

## Pitfalls

- Drifting into a full rewrite. Keep one slice per plan, and keep the old path until the new one is proven.
- Losing behavior nobody documented. Record odd behavior in the domain map as you find it, and decide per item whether to keep it.
- The domain map growing too large to be useful. Keep it to what the next slice needs ([P1](../principles.md#p1-context-is-finite)).
- Removing old code too early. Removal is its own slice, after the new path has run for a while.

## Done check

For each slice:

- [ ] Old and new paths give the same results on the same inputs, or each difference is recorded and accepted.
- [ ] The old path is still available.
- [ ] `domain_map.md` is updated.

## Example

No run recorded yet. Add a link to `examples/` after the first real use.
