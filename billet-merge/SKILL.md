---
name: billet-merge
description: Merge a finished task's branch, verify the result, close the task, and remove its worktree when the user explicitly invokes billet-merge (`$billet-merge` in Codex, `/billet-merge` in Claude Code).
---

# Merge task

Use only when explicitly invoked as `$billet-merge` or `/billet-merge`.
Follow [../billet-add/format.md](../billet-add/format.md).

Work in the main checkout, on the branch that should receive the work. If
invoked from the task's own worktree, say so and stop. Find the branch from the
task's `branch` field, the user's words, or `git worktree list`; ask if it is
unclear. One branch may close several tasks.

Before merging, read the branch's commits and confirm what `billet-finish`
requires. Stop if it falls short, if the branch has uncommitted changes, or if
the main checkout's uncommitted changes overlap it. Ask first if the task's
`running` is set. Leave other uncommitted changes out of every commit.

Follow the project's documented merge rules: merge style, commit message,
catching up with the base branch, and checks. If the project lands work through
reviewed pull requests, say so and stop. With no rules, ask which checks to run,
then make a plain merge. Never push unless the project's rules or the user say
to. On conflicts, abort the merge and report.

Run the checks on the merged result. If they fail, stop and report how to undo
the merge; keep the task open and remove nothing. Otherwise follow
`billet-finish`, using the branch's commits for its Result and findings, and
commit the closing changes if the project's rules say to. Then remove the
worktree and branch, only once the branch is merged and the worktree and any
submodules are clean, and report what was removed.
