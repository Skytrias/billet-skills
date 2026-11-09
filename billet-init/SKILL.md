---
name: billet-init
description: Set up a project for task files, creating the task folder and telling the project's agents about it, when the user explicitly invokes billet-init (`$billet-init` in Codex, `/billet-init` in Claude Code).
---

# Init tasks

Use only when explicitly invoked as `$billet-init` or `/billet-init`.
Follow [../billet-add/format.md](../billet-add/format.md).

Work in the main checkout. Create the task folder and `tasks.json` with
`next_id` 1 and the statuses in column order. If they already exist, keep
them and only fill in what is missing; never renumber or rewrite tasks.

Add a short section to the project's agent instructions file (`AGENTS.md`,
`CLAUDE.md`, or whichever the project already uses; create `AGENTS.md` only
when none exists). When the file already describes the task folder, add only
what it is missing. Adapt the folder name to the format:

```
## Tasks

Project tasks live in `docs/tasks/`, one Markdown file per task with JSON
frontmatter, managed by the `billet-*` skills. Edit task files only in the
main checkout, never on a worktree branch.

Before non-trivial work, search the task files, including closed and
archived ones, for the files and terms involved. Their Findings and Results record what was
learned; the code wins when they disagree. Record non-obvious findings in the
task as they come up.
```

Do not create tasks. If the project keeps tasks somewhere else (a `TODO.md`,
`tasks.md`, or similar), mention it and leave it untouched; the user can turn
its items into tasks with `billet-add`. Report what was created or changed.
