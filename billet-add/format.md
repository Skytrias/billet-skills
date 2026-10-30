# Task format

Shared by every `billet-*` skill. Edit the defaults below to change
wording, language, or values; the skills follow whatever this file says.

## Defaults

- Folder: `docs/tasks/`
- Language for titles and bodies: English
- Dates: `YYYY-MM-DD`; `running`: ISO 8601 timestamp with offset
- Statuses, in board column order:
  - `proposed`: an open decision still changes how it would be done
  - `ready`: can be started without further questions
  - `in-progress`: work has started
  - `done`: finished and verified
  - `canceled`: dropped, kept for history
- Hardness: `easy`, `medium`, `hard`
- Body sections for new tasks: Outcome, Current state, Scope, Approach,
  Acceptance criteria, Verification, Open questions

## Files

```
docs/tasks/
  tasks.json        {"next_id": 1, "statuses": [...]}
  0007-short-slug.md
```

- `tasks.json` holds the next unused ID and the status column order. Create
  it when missing.
- One Markdown file per task, named `NNNN-short-slug.md`: four-digit ID, then
  a lowercase, hyphenated slug of the title in at most five words. The name
  never changes after creation.
- IDs are never reused. Tasks are never deleted or moved; finishing or
  canceling only changes the status.

## Task file

A `---` line, one pretty-printed JSON object (2-space indent, keys in this
order), a `---` line, then the Markdown body without a title heading.

```
---
{
  "id": 7,
  "title": "Short imperative title",
  "status": "ready",
  "hardness": "medium",
  "area": "docs",
  "tags": ["ui"],
  "order": 3,
  "blocked_by": [],
  "created": "2026-10-19",
  "started": null,
  "finished": null,
  "reason": null,
  "running": null,
  "branch": null
}
---
## Outcome
...
```

- `area`: one short lowercase group (feature, component, or subsystem); reuse
  existing areas before inventing new ones. `tags`: optional extras.
- `order`: position inside its status column, lowest first. New tasks take
  the highest `order` in the project plus one.
- `blocked_by`: IDs of tasks that must be `done` first.
- `started`, `finished`: dates set when work starts and when the task is done
  or canceled. `reason`: why it was canceled.
- `running`: timestamp of when an agent started actively working on the
  task, or `null`. A toggle beside the status, not a status. `branch`: the
  branch or worktree that work happens on, or `null`.
- Keep the JSON valid and pretty-printed whenever writing the file; people
  read these raw.

## Main checkout

Task files are only ever edited in the repository's main checkout (the first
entry of `git worktree list`), even when the code work happens in another
worktree. Never edit or commit task files on a worktree branch; this keeps
`running` visible and avoids merge conflicts. Task file changes may stay
uncommitted in the main checkout until the user commits them.
