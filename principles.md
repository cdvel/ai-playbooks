# Principles

Every step in the playbooks traces back to one of seven principles. This page gives the reason behind each.

Context engineering is deciding what goes into the model's context window at each step (instructions, files, tool output, notes) and what stays out. Prompt wording is one part of it.

## P1: Context is finite

Why it holds: a model works from what is in its window, and its accuracy falls as the window fills with material it doesn't need. More tokens is not better. The goal is the smallest set of tokens that carries the signal.

In the playbooks: research compresses the repo into a short document, and the agent works from that document instead of the whole codebase.

Source: Anthropic, Effective context engineering for AI agents (recall drops as the window grows). HumanLayer, Advanced Context Engineering (noise in the window lowers output quality).

## P2: Fresh context per phase

Why it holds: exploration leaves noise behind. Files such as `research.md` and `plan.md` carry the useful state into a clean session, so the next phase starts with only what it needs.

In the playbooks: implement starts in a new session from the plan only.

Source: Anthropic, Effective context engineering for AI agents (notes persisted outside the window, summaries that start a new window). Anthropic, Best practices for Claude Code (build from a written spec in a fresh session). HumanLayer, Advanced Context Engineering (research, plan and implement, with state compacted into files).

## P3: Review where it is cheapest

Why it holds: a wrong line in a plan becomes hundreds of wrong lines of code, and a plan takes minutes to read. Review effort buys the most at the plan.

In the playbooks: the plan is the one step the human reviews before code exists.

Source: HumanLayer, Advanced Context Engineering (human review of research and plans has more leverage than review of code).

## P4: Give the agent a way to check itself

Why it holds: an agent that can run tests or a build gets a pass or fail answer, and can catch and correct its own mistakes in a loop.

In the playbooks: setup and the done check on every page.

Source: Anthropic, Best practices for Claude Code (give the agent a check it can run, such as tests, a build or a linter).

## P5: Write down what it can't know

Why it holds: an agent has none of a team's unwritten knowledge: conventions, commands, files nobody touches. If it is not in a file the agent reads, it does not exist for the agent.

In the playbooks: `AGENTS.md` and the codebase onboarding playbook.

Source: Anthropic, Best practices for Claude Code (keep the project instructions file to commands and conventions the agent can't find in the repo).

## P6: Small, reversible steps

Why it holds: errors compound over a long run. Small commits keep each one cheap to find and undo.

In the playbooks: one plan step at a time, commit after each.

Source: Anthropic, Best practices for Claude Code (try a few files first, and commit per unit in batch migrations). The page does not state "commit often" as a rule, so this principle goes slightly beyond it.

## P7: Isolate noisy work

Why it holds: a sub-agent does a broad search in its own context and returns only the conclusion, so the main session never carries the search noise.

In the playbooks: research on large repos.

Source: Anthropic, Effective context engineering for AI agents (sub-agents explore widely and return a short summary). Anthropic, Best practices for Claude Code (keep long output out of the main conversation). HumanLayer, Advanced Context Engineering (sub-agents as context control).

## Sources

- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices)
- [Advanced Context Engineering for Coding Agents](https://www.humanlayer.dev/blog/advanced-context-engineering)
