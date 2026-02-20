---
title: Codebase onboarding
status: draft-untested
last_updated: 2026-11-16
---

# Codebase onboarding

## When to use it

You are about to do agent work in a repo that has no `AGENTS.md`, or one you don't know. The result is an `AGENTS.md` that a fresh session can work from.

Not for: repos that already have a current `AGENTS.md`.

## Setup

- [ ] The repo is cloned and its dependencies can be installed.
- [ ] You know who to ask about the parts of the repo you don't understand.

## Steps

1. Research ([P1](../principles.md#p1-context-is-finite), [P7](../principles.md#p7-isolate-noisy-work)). The agent explores the repo and reports structure, build and test commands, and conventions. On a large repo, have sub-agents search each area and return only a summary. No changes.

   ```
   Explore this repo. Write research.md: directory layout, how to install, build and test, code conventions you can see, anything that looks fragile or generated. Use sub-agents for broad searches and keep only their summaries. Do not change any code.
   ```

2. Draft AGENTS.md ([P5](../principles.md#p5-write-down-what-it-cant-know)). This step replaces the plan. The agent writes a short `AGENTS.md` from the research: commands, layout, conventions, gotchas.

   ```
   From research.md, draft AGENTS.md. Include only what an agent needs on every task: commands, layout, conventions, gotchas. Run every command you list and note whether it worked. Keep it short.
   ```

3. Add the unwritten rules ([P5](../principles.md#p5-write-down-what-it-cant-know)). You add what only people know: files nobody touches, deploy rules, naming habits, past incidents. Edit `AGENTS.md` by hand, or have the agent interview you.

   ```
   Read AGENTS.md and ask me one question at a time about anything a newcomer would get wrong in this repo. Add my answers to AGENTS.md.
   ```

4. Check ([P2](../principles.md#p2-fresh-context-per-phase), [P4](../principles.md#p4-give-the-agent-a-way-to-check-itself)). Start a fresh session that sees only `AGENTS.md` and the repo, and ask it to build and test.

   ```
   Using only AGENTS.md, install the dependencies, build the project and run the tests. Report each command you ran and what you needed that AGENTS.md did not say.
   ```

## Pitfalls

- The file describes the code but misses the unwritten rules. Step 3 is not optional.
- The file is too long. Keep it to what an agent needs on every task ([P1](../principles.md#p1-context-is-finite)), and move the rest to separate docs.
- Commands listed but never run. Run each one and fix the ones that fail.
- The agent describes what it assumes, not what it found. Ask for the file or command behind each claim.

## Done check

- [ ] A fresh session can build the project and run the tests using only `AGENTS.md`.
- [ ] Every command in the file has been run at least once.
- [ ] A person has read the file and added at least the unwritten rules they know.

## Example

No run recorded yet. Add a link to `examples/` after the first real use.
