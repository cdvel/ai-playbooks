<div align="center">

# ai-playbooks

**Playbooks for six kinds of coding-agent work: one loop, the prompts to paste, and checks that show it worked.**

Plain markdown · prompts are tool-neutral · all six playbooks are draft-untested and will be revised after their first real runs · MIT license

[Uses](#uses) · [Using a playbook](#using-a-playbook) · [Playbooks](#playbooks) · [Principles](principles.md) · [Background](#background)

</div>

![Flow from setup to research, plan, implement and check. Sub-agents can search for research. A person reviews the plan, and only plan.md crosses into a fresh implementing session. A failed check returns to implement, and legacy work returns to plan for the next slice. Under each step hang the changes made by individual playbooks.](docs/playbook_loop.svg)

[P1](principles.md#p1-context-is-finite) context is finite · [P2](principles.md#p2-fresh-context-per-phase) fresh context per phase · [P3](principles.md#p3-review-where-it-is-cheapest) review where it is cheapest · [P4](principles.md#p4-give-the-agent-a-way-to-check-itself) let the agent check itself · [P5](principles.md#p5-write-down-what-it-cant-know) write down what it can't know · [P6](principles.md#p6-small-reversible-steps) small, reversible steps · [P7](principles.md#p7-isolate-noisy-work) isolate noisy work

You ask an agent to refactor and behavior changes. You ask for an upgrade and an unrelated package gets pinned. Fifty turns in, the session is full of search output and starts to drift. Each playbook here is one page for one kind of task: what to prepare, the steps, the prompts to paste, what usually goes wrong, and how to tell it worked. They share one loop (research, plan, implement, check), and seven [principles](principles.md) about what goes into the model's context window explain each step.

> [!IMPORTANT]
> The plan is the one step you review. Implementation starts in a fresh session from `plan.md` alone, so a wrong line is caught in a plan that takes minutes to read, before it becomes hundreds of lines of code.

## Uses

- Change the structure of code without changing what it does.
- Modernize or rebuild an old codebase piece by piece.
- Rebuild something from a written spec without the implementing session seeing the original code.
- Add tests to code that has none, before changing it.
- Upgrade a framework, language version or major dependency.
- Start agent work in a repo that has no `AGENTS.md`.

## Using a playbook

1. Open the page that matches the task, and check its Setup list.
2. Run the steps in order. Where the page says so, start a new session. Fill in the `<placeholders>` in each prompt.
3. Run the Done check before you merge.

> [!TIP]
> After the Research step, `git status` should show only the new notes file. Changes to code mean the step broke its "no changes" rule: discard them and rerun it.

## Playbooks

### Refactoring

Pins current behavior with characterization tests, then restructures in small steps with the tests as the check. Test files are off limits while implementing.

<details>
<summary><b>Steps</b></summary>

Pin current behavior, research, plan, implement, check. [playbooks/refactoring.md](playbooks/refactoring.md)

</details>

### Legacy redevelopment

Maps the system, picks a seam where new code can take over one slice while the old code keeps running, and repeats per slice.

<details>
<summary><b>Steps</b></summary>

Map the system once, then for each slice: pick a seam and a slice, implement, compare old and new. [playbooks/legacy_redevelopment.md](playbooks/legacy_redevelopment.md)

</details>

### Clean-room implementation

Keeps two sessions apart: one writes `spec.md` from observable behavior, the other builds from the spec alone. `provenance.md` records what each was given. It makes no legal claim.

<details>
<summary><b>Steps</b></summary>

Spec session, human review of the spec, implementation session, check with tests written from the spec. [playbooks/clean_room_implementation.md](playbooks/clean_room_implementation.md)

</details>

### Test backfill

Ranks the behaviors worth protecting by risk, then writes tests only. Bugs the tests reveal go to `notes.md`, not into the code.

<details>
<summary><b>Steps</b></summary>

Research, plan, implement, check by reading what each test asserts. [playbooks/test_backfill.md](playbooks/test_backfill.md)

</details>

### Dependency migration

Reads the changelog, lists the breaking changes that affect this codebase with file references, and upgrades in small steps without silencing warnings.

<details>
<summary><b>Steps</b></summary>

Research, plan (one jump or stepwise), implement, check including the lockfile diff. [playbooks/dependency_migration.md](playbooks/dependency_migration.md)

</details>

### Codebase onboarding

Produces an `AGENTS.md` that a fresh session can build and test from. A person adds the unwritten rules.

<details>
<summary><b>Steps</b></summary>

Research with sub-agents, draft `AGENTS.md`, add the unwritten rules, check in a fresh session. [playbooks/codebase_onboarding.md](playbooks/codebase_onboarding.md)

</details>

## Adding a playbook

1. Do the task once for real, on a sandbox repo or a public OSS clone. Keep the prompts and notes.
2. Copy [templates/playbook_template.md](templates/playbook_template.md).
3. Write up what worked: the steps, the prompts worth reusing, the pitfalls, and the principle behind each step.
4. Use it on a second task and revise. Then change its status from `draft-untested` to `tested`.
5. Add it to the Uses and Playbooks sections above, and put run notes in [examples/](examples/README.md).

## Background

- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices)
- [Advanced Context Engineering for Coding Agents](https://www.humanlayer.dev/blog/advanced-context-engineering)

## License

MIT
