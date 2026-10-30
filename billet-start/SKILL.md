---
name: billet-start
description: Start or continue implementing one project task, surfacing material questions before work begins, when the user explicitly invokes billet-start (`$billet-start` in Codex, `/billet-start` in Claude Code).
---

# Start task

Use only when explicitly invoked as `$billet-start` or `/billet-start`.
Follow [../billet-add/format.md](../billet-add/format.md).

Read the task file, relevant code, and current worktree. Set `running` to now
and `branch` to where the work happens, in the main checkout, before anything
else. Validate that the task is ready and its `blocked_by` tasks are done; ask
concise questions for decisions that materially affect the implementation,
and set the task `ready` once they are answered. When work begins, set
`in-progress` and `started` if unset. Perform the scoped work, keep the body
current when findings change it, and run the stated verification.

When work stops without finishing, set `running` back to `null`. Do not close
the task or update CHANGELOG.md; that is `billet-finish`.
