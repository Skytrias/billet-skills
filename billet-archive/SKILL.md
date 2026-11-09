---
name: billet-archive
description: Move long-closed done and canceled project tasks into the task folder's archive, keeping them searchable, when the user explicitly invokes billet-archive (`$billet-archive` in Codex, `/billet-archive` in Claude Code).
---

# Archive tasks

Use only when explicitly invoked as `$billet-archive` or `/billet-archive`.
Follow [../billet-add/format.md](../billet-add/format.md), its Archive section
above all.

Work in the main checkout. Read only headers (see Reading the task folder).
Find the tasks that qualify: `done` or `canceled`, with `finished` more than the
Archive after days ago, or as many days as the user names. Hold back any that an
open task names in `blocked_by` or links to. Present the count, the IDs and
titles, and each held-back task with the open task that needs it, and ask before
moving anything.

Once the user agrees, create `archive/` in the task folder if needed and move
each file, with a folder of the same name beside it, using `git mv` when the
project uses Git. Never overwrite a file already in the archive; stop and report
it instead. Do not edit any task, `tasks.json`, or `CHANGELOG.md`. Report what
moved, and leave committing to the user unless asked.
