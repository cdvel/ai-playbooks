---
title: Test backfill
status: draft-untested
last_updated: 2026-11-16
---

# Test backfill

## When to use it

Code has no tests, or too few to change it safely. This is often the first step before [refactoring](refactoring.md) or [legacy redevelopment](legacy_redevelopment.md).

Not for: writing tests for new features, which belong in the feature's own work.

## Setup

- [ ] The code builds and runs.
- [ ] A test runner is configured, or setting one up is the first step of the plan.
- [ ] The working tree is clean, on a branch made for this work.

## Steps

1. Research ([P1](../principles.md#p1-context-is-finite)). The agent reads the code and lists behaviors worth protecting, ranked by risk. The output is a list of behaviors, not a list of functions. No changes.

   ```
   Read the code involved in <target area>. Write research.md: the behaviors worth protecting, ranked by risk of breaking and cost of breakage, with the files each one lives in. Do not change any code.
   ```

2. Plan ([P3](../principles.md#p3-review-where-it-is-cheapest)). The agent picks which behaviors get tests in this pass. You review the list: is the risky behavior in, and is the scope small enough to finish?

   ```
   From research.md, write plan.md: which behaviors get tests in this pass, the test file for each, what stays out of scope, and how each test is checked.
   ```

3. Implement ([P2](../principles.md#p2-fresh-context-per-phase), [P6](../principles.md#p6-small-reversible-steps)). A fresh session writes the tests, one plan step at a time. It writes tests only.

   ```
   Follow plan.md one step at a time. Write tests only. Do not change production code. If a test reveals a bug, record it in notes.md and leave the code alone. Run the tests after each step and commit.
   ```

4. Check ([P4](../principles.md#p4-give-the-agent-a-way-to-check-itself)). Run the done check, then read what each test asserts.

   ```
   Summarize the tests added against plan.md. For each test, state in one line what behavior it asserts. List anything not in the plan, and any bugs recorded in notes.md.
   ```

## Pitfalls

- Tests that assert nothing useful, such as checking only that a function runs. Ask for the behavior each test asserts, and reject tests that assert none.
- Tests that lock in an existing bug. Review what each test asserts, not just that it passes, and check `notes.md` for bugs the agent found.
- Mocking the thing under test. Look at what the mocks replace.
- Chasing a coverage number instead of the risky behaviors. Rank by risk in the plan and stop when the list is done.

## Done check

- [ ] The new tests pass.
- [ ] For a sample of the tests, breaking the code on purpose makes the test fail.
- [ ] `git diff <base> -- <production paths>` is empty.

## Example

No run recorded yet. Add a link to `examples/` after the first real use.
