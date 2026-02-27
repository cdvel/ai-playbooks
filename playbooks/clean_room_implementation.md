---
title: Clean-room implementation
status: draft-untested
last_updated: 2026-11-16
---

# Clean-room implementation

This describes a working method. It makes no claim about legal independence from the original work. Get legal advice before relying on it for that purpose.

## When to use it

You want to rebuild something from a written spec, without the implementing session ever seeing the original code. The method keeps two sessions apart: one writes the spec, the other builds from it.

Not for: modernizing code you are free to read ([legacy redevelopment](legacy_redevelopment.md)).

## Setup

- [ ] Two separate sessions, each in its own working directory.
- [ ] The implementing directory does not contain the original code, in any form.
- [ ] You know what the spec session may read: observable behavior, public docs and public interfaces.
- [ ] An empty `provenance.md` ready to record what each session was given.

## Steps

This playbook replaces the shared workflow.

1. Spec session ([P1](../principles.md#p1-context-is-finite), [P2](../principles.md#p2-fresh-context-per-phase)). In the first working directory, the agent writes `spec.md` from observable behavior, public docs and public interfaces only. Record what it was given in `provenance.md`.

   ```
   Write spec.md for <system> from its public documentation, its public interfaces and the behavior I show you. Describe what it does, not how it is built. Do not copy names of internal functions or structure. List the inputs, outputs, errors and edge cases.
   ```

2. Review the spec ([P3](../principles.md#p3-review-where-it-is-cheapest)). You read `spec.md` and remove anything copied from the original's internals: function names, file structure, comments. Then copy only `spec.md` into the implementing directory.

   ```
   Read spec.md as a reviewer. List every place where it describes internals instead of behavior: function names, class names, file layout, algorithms that are not part of the public contract.
   ```

3. Implementation session ([P2](../principles.md#p2-fresh-context-per-phase), [P6](../principles.md#p6-small-reversible-steps)). In a fresh session in the second directory, the agent receives only `spec.md`. It plans, you review the plan, then it implements in small steps.

   ```
   Read spec.md. Write plan.md: ordered steps, files per step, how each step is checked. After I approve it, follow plan.md one step at a time, run the tests after each step and commit. Stop and ask if the spec is unclear. Do not look for or ask for the original code.
   ```

4. Check ([P4](../principles.md#p4-give-the-agent-a-way-to-check-itself)). Write tests from `spec.md`, not from the original code, and run them against the new implementation.

   ```
   From spec.md only, write tests for every behavior, error and edge case it lists. Run them against the implementation and summarize failures against the spec.
   ```

## Pitfalls

- Original code leaking into the implementing session through pasted snippets, shared directories or attached files. Check the working directory and the conversation before you start.
- The spec describing internals instead of behavior. Review it for function names and structure lifted from the original.
- The model reproducing code it may have seen in training. This playbook cannot rule that out.

## Done check

- [ ] Tests derived from the spec pass.
- [ ] `provenance.md` shows the implementing session received only `spec.md`.

## Example

No run recorded yet. Add a link to `examples/` after the first real use.
