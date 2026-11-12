# Billet skills

Skills that let your coding agent manage a project's tasks. Each task is a
Markdown file in `docs/tasks/` with a small JSON header for status, order and
blockers. You tell the agent to add, start or finish a task and it edits the
files.

They work with any agent that supports skills. Call them by name, like
`billet-add`.

A billet is a written order that assigns someone a job.

## Getting started

Copy or symlink the `billet-*` folders into your agent's skill folder, for
example `~/.claude/skills/`. Keep them next to each other. Restart the agent
and run `billet-init` in your project.

## Skills

| Skill | What it does |
|---|---|
| `billet-init` | Set up a project |
| `billet-add` | Write a new task |
| `billet-critique` | Poke holes in a task's plan before work starts |
| `billet-split` | Split a big task into pieces that can be worked on in parallel |
| `billet-start` | Work on a task, asking open questions first |
| `billet-finish` | Check the work, close the task, add a changelog entry and ready the tasks it unblocks |
| `billet-merge` | Merge a task's branch, check the result, close the task and remove its worktree |
| `billet-cancel` | Cancel a task but keep its file |
| `billet-list` | List open tasks |
| `billet-leftovers` | Find unfinished work and add it as tasks |
| `billet-groom` | Fix broken task data and tasks that no longer match the code |
| `billet-recall` | Answer what earlier tasks and docs know about a topic |
| `billet-archive` | Move long-closed tasks into the archive, still searchable |

Tasks also remember what was learned. Agents note gotchas and decisions in a
`## Findings` section as they work, and check earlier tasks before planning new
ones.

## A task file

```
---
{
  "id": 7,
  "title": "Add dark mode",
  "status": "ready",
  "hardness": "medium",
  "area": "ui",
  "blocked_by": [],
  ...
}
---
## Outcome
The app follows the system's light or dark setting.
```

The full list of fields is in [`billet-add/format.md`](billet-add/format.md).

A large aim can be a goal: an ordinary task with a folder of the same name
beside it that holds its tasks. `billet-add` offers one when you add many
related tasks at once, and `billet-split` turns a big task into one.

## Changing them

The skills are a starting point. Change them however you like.

The file format and defaults like statuses and language live in
`billet-add/format.md`. Every skill reads it, so one edit changes them all.
Keep its fields if you want the Billet app to read your tasks.

Some of the workflow is just how I work. `billet-finish` writes a
`CHANGELOG.md` entry, for example. Drop or rewrite anything you don't need.

## Billet

[Billet](https://mktwsk.xyz/billet) is a desktop app that shows the tasks of
all your projects as a board and lets you manage them. It supports the basic
format. More may come later.

## License

zlib, see [LICENSE](LICENSE).
