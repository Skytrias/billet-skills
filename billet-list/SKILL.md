---
name: billet-list
description: Report open project tasks with IDs, status, and hardness when the user explicitly invokes billet-list (`$billet-list` in Codex, `/billet-list` in Claude Code).
---

# List tasks

Use only when explicitly invoked as `$billet-list` or `/billet-list`.
Follow [../billet-add/format.md](../billet-add/format.md).

Read only the live tasks' headers, never their bodies or the archive (see
Reading the task folder in format.md), without modifying anything. Report tasks
that are not `done` or `canceled`, grouped by status in column order and
sorted by `order`, with ID, title, hardness, and area. Past about 100 open
tasks, give the counts by status and area first, then the list for the statuses
or areas the user asks about. Mark tasks with `running`
set, with their branch and elapsed time, and mention invalid frontmatter directly.
