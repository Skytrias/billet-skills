---
name: billet-finish
description: Verify and close a completed project task, add a user-facing Unreleased changelog entry, and make the tasks it unblocks ready when the user explicitly invokes billet-finish (`$billet-finish` in Codex, `/billet-finish` in Claude Code).
---

# Finish task

Use only when explicitly invoked as `$billet-finish` or `/billet-finish`.
Follow [../billet-add/format.md](../billet-add/format.md).

Confirm the task's acceptance criteria and recorded verification actually
passed. Add a `## Result` section with the completed outcome and
verification, add any findings not yet recorded, link the tasks it built on,
set `done` and `finished`, and clear `running`. Add a concise meaningful
user-facing item under `Unreleased` in `CHANGELOG.md`. Do not close a partial
or unverified task; state the blocker instead.

Then release what the closed tasks unblock. For every live task, goal folders
included, whose `blocked_by` names a task just closed, reread its Open
questions:

- If none remain open, set a `proposed` task to `ready`. That covers "None"
  and questions that only waited on the closed task, such as "None beyond
  [0044]". Note in its Open questions what settled them, with a link.
- If a real decision is still open, leave it `proposed`.
- Never change `in-progress`, `done` or `canceled` tasks.

Other unfinished blockers don't keep a task `proposed`: `blocked_by` already
tracks them, and `proposed` means an open decision. Keep closed IDs in
`blocked_by` as history. Edit only the fields you change, in place, keeping
the frontmatter's layout (arrays on one line).

Report which tasks moved to `ready`, which of those are now fully unblocked
(every blocker `done` or archived), and which stay `proposed` and why.

A goal closes only once every task in its folder is done or canceled. When the
task closed was the last open one in its goal, say so and suggest finishing the
goal.
