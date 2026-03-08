# ai-playbooks

Practical playbooks for working with coding agents. One page per kind of task. Open the page that matches the job.

## What a playbook is

A playbook says what to prepare, which steps to follow, the prompts to use, what usually goes wrong, and how to tell it worked. Each is written from a real run and revised after use.

## Pick a playbook

| Task | Playbook | Use it when |
|---|---|---|
| Refactoring | [refactoring](playbooks/refactoring.md) | You want to change the structure of code without changing what it does. |
| Legacy redevelopment | [legacy_redevelopment](playbooks/legacy_redevelopment.md) | You are modernizing or rebuilding an old codebase piece by piece. |
| Clean-room implementation | [clean_room_implementation](playbooks/clean_room_implementation.md) | You want to rebuild something from a written spec without looking at the original code. |
| Test backfill | [test_backfill](playbooks/test_backfill.md) | Code has no tests, or too few to change it safely. |
| Dependency migration | [dependency_migration](playbooks/dependency_migration.md) | You are upgrading a framework, language version or major dependency. |
| Codebase onboarding | [codebase_onboarding](playbooks/codebase_onboarding.md) | You are about to do agent work in a repo that has no `AGENTS.md`, or one you don't know. |

## How they work

Most playbooks follow four steps: research, plan, implement, check. The agent researches and writes a short summary, then a plan. You review the plan before any code exists. A fresh session implements the plan in small steps, and a final check compares the result with the plan.

Each step applies one or more of seven principles about what goes into the model's context window. [principles.md](principles.md) gives the reasons and the sources.

## Status

All playbooks are `draft-untested`. They will be revised after their first real runs.

## Adding a playbook

1. Do the task once for real, on a sandbox repo or a public OSS clone. Keep the prompts and notes.
2. Copy [templates/playbook_template.md](templates/playbook_template.md).
3. Write up what worked: the steps, the prompts worth reusing, the pitfalls, and the principle behind each step.
4. Use it on a second task and revise. Then change its status from `draft-untested` to `tested`.
5. Add one line to the table above.

Run notes go in [examples/](examples/README.md).
