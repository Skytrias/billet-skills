---
name: billet-split
description: Split one large project task into independently workable tasks only when the pieces can genuinely proceed in parallel, when the user explicitly invokes billet-split (`$billet-split` in Codex, `/billet-split` in Claude Code).
---

# Split task

Use only when explicitly invoked as `$billet-split` or `/billet-split`.
Follow [../billet-add/format.md](../billet-add/format.md).

Read the task and the code it touches. Split only along seams where each piece
can be built, verified, and merged on its own, ideally in its own worktree
without touching the same files as a sibling. A large task whose parts are
tightly interdependent stays one task: say so and change nothing. Never split
just to make tasks smaller.

When a split is justified, create the new tasks with their own outcome,
scope, acceptance criteria, and verification, using `blocked_by` only for real
ordering constraints. Cancel the original with a `reason` naming the new IDs,
or keep it as a small integration task blocked by them. Report which pieces
can run in parallel.
