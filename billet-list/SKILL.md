---
name: billet-list
description: Report open project tasks with IDs, status, and hardness when the user explicitly invokes billet-list (`$billet-list` in Codex, `/billet-list` in Claude Code).
---

# List tasks

Use only when explicitly invoked as `$billet-list` or `/billet-list`.
Follow [../billet-add/format.md](../billet-add/format.md).

Read the task files' frontmatter without modifying anything. Report tasks
that are not `done` or `canceled`, grouped by status in column order and
sorted by `order`, with ID, title, hardness, and area. Mark tasks with `running`
set, with their branch and elapsed time, and mention invalid frontmatter directly.
