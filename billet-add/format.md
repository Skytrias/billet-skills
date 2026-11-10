# Task format

Shared by every `billet-*` skill. Edit the defaults below to change
wording, language, or values; the skills follow whatever this file says.

## Defaults

- Folder: `docs/tasks/`
- Archive after: 30 days (see Archive)
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
  0050-new-parser.md    a goal (see Goals)
  0050-new-parser/      its tasks
    0051-tokenizer.md
  archive/
    0002-older-closed-task.md
```

- `tasks.json` holds the next unused ID and the status column order. Create
  it when missing.
- One Markdown file per task, named `NNNN-short-slug.md`: four-digit ID, then
  a lowercase, hyphenated slug of the title in at most five words. The name
  never changes after creation.
- IDs are never reused, archived ones included. Tasks are never deleted.
  Finishing or canceling only changes the status; the only move is into the
  archive, once, long after a task closed (see Archive).

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

## Goals

A goal groups many tasks toward one large aim, such as a new parser. It is an
ordinary task file whose Outcome is the aim, with a folder of the same name
beside it holding its tasks.

- One level only: a goal's folder holds task files, never folders or goals.
- IDs come from the project's one `tasks.json`, so they stay unique across
  goals, and `blocked_by` and links work across folders
  (`[0012](../0012-fix-cli-flags.md)` from inside a goal).
- A task's goal is chosen when the task is created, like its file name.
  Moving tasks into or out of a goal is a regrouping the user asks for, never
  part of a status change.
- A goal has its own status and is closed with `billet-finish` once its tasks
  are closed. It is never started as one task: its tasks are.
- Its progress, its tasks done out of those not canceled, is read from its
  folder, never written into the goal.
- `order` counts across the whole project, goals' folders included.

## Knowledge

Tasks are the project's record of what was learned; keep no separate notes
folder.

- Findings: a `## Findings` section holds what someone would otherwise have
  to rediscover: a gotcha, a rejected approach, or a decision and its reason.
  Write it when found, not at the end. Most tasks have none. Leave out what
  the code or docs already show. A fact that applies to all future work in an
  area goes in the project's agent instructions file instead.
- Later: a closed task can still gain findings, each starting with the date.
  When a finding turns out wrong, add a dated correction beside it.
- Links: refer to another task as `[0011](0011-short-slug.md)`, not by bare ID.
- Searching earlier tasks: search task files of every status, including `done`,
  `canceled`, and the archive, for the files, symbols, and terms involved; in a
  monorepo, also search sibling projects' task folders. A file most tasks touch says
  little, so rank by the most specific matches. Read only what the closest 3-5
  tasks learned: Findings, Result, the cancel `reason`, and older notes or
  decisions sections. Treat these as dated claims: check them against the code,
  and the code wins.

## Reading the task folder

A project can hold thousands of tasks, and an agent's command output is cut
short past a limit (30,000 characters in Claude Code), silently dropping tasks.
Read in two steps: a broad pass over headers, then the bodies of only the few
tasks that matter.

- A header is everything between the first two `---` lines. Its length varies,
  since arrays may take a line per item, so never read a fixed number of lines.
- The live tasks are the task files in the task folder and its goal folders,
  one level down, without `archive/`. List, pick, and count from them. Include the archive only
  to find a task by ID and to search what earlier tasks learned.
- Never print every task body, or every header, in one command. Filter by
  status first, then print one short line per task.
- Scalar fields sit on their own line as `"key": value`, so a line search finds
  them. Parse the JSON for `blocked_by` and `tags`, which may span lines.
- Past about 100 open tasks, report counts by status and area before any detail.

For example, from the project root, with the project's task folder in place of
`docs/tasks`:

```sh
# How many live tasks are open: decides between counts and a list.
grep -rlE '"status": "(proposed|ready|in-progress)"' docs/tasks \
  --include='[0-9][0-9][0-9][0-9]-*.md' --exclude-dir=archive | wc -l
# One line per open live task, read from headers only.
python3 - <<'PY'
import glob, json
for path in sorted(glob.glob("docs/tasks/**/[0-9][0-9][0-9][0-9]-*.md", recursive=True)):
    if "/archive/" in path: continue
    with open(path) as f:
        lines = iter(f)
        head = [] if next(lines, "").strip() == "---" else None
        for line in lines if head is not None else ():
            if line.strip() == "---": break
            head.append(line)
    try: t = json.loads("".join(head or []))
    except ValueError: print("unreadable header:", path); continue
    if t.get("status") in ("done", "canceled"): continue
    print(t["id"], t["status"], t.get("order"), t.get("hardness"), t.get("area"),
          t["title"], "waits on", t.get("blocked_by"))
PY
# The next order: the highest live order plus one.
grep -rhoE '"order": [0-9]+' docs/tasks --include='[0-9][0-9][0-9][0-9]-*.md' \
  --exclude-dir=archive | awk '{print $2}' | sort -n | tail -1
# A task by ID, archive included.
find docs/tasks -name '0042-*.md'
# Rank earlier tasks for a term by match count; read only the top 5.
grep -rciE 'conflict' docs/tasks --include='[0-9][0-9][0-9][0-9]-*.md' \
  | grep -v ':0$' | sort -t: -k2 -rn | head -5
```

Then read only those few files, and only the sections needed: Findings and
Result for what was learned, or the whole body when working on the task.

## Archive

Done and canceled tasks that closed long ago move into `archive/` inside the
task folder (by default `docs/tasks/archive/`), so the folder stays short over
years of work. `billet-archive` does it, and Billet can too.

- A task qualifies when its status is `done` or `canceled` and its `finished`
  date is more than the Archive after days ago. A task without `finished` never
  qualifies.
- Never archive a task that an open task names in `blocked_by` or links to.
- A folder beside a task with the same name as its file moves with it.
- A goal moves with its folder, and only once the goal and every task in its
  folder qualify. A task inside a goal never moves on its own.
- An archived file keeps its name and content; `tasks.json` stays in the task
  folder. Nothing else is edited.
- An archived task counts as closed wherever it is named: an archived blocker
  does not block.

## Main checkout

Task files are only ever edited in the repository's main checkout (the first
entry of `git worktree list`), even when the code work happens in another
worktree. Never edit or commit task files on a worktree branch; this keeps
`running` visible and avoids merge conflicts. Task file changes may stay
uncommitted in the main checkout until the user commits them.
