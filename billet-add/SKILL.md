---
name: billet-add
description: Analyze a proposed project task and add it as one task file with JSON frontmatter when the user explicitly invokes billet-add (`$billet-add` in Codex, `/billet-add` in Claude Code).
---

# Add task

Use only when explicitly invoked as `$billet-add` or `/billet-add`.
Follow [format.md](format.md) for the folder, file layout, and all values.

Read the open tasks' titles and areas from their headers (see Reading the task
folder in format.md), the few closest open tasks in full, and relevant
source/docs; avoid duplicates and reuse existing areas. Search earlier tasks
and link related ones in the body. Take the ID from `next_id` in `tasks.json`,
check that no file with that ID exists anywhere in the task folder, archive
included, increment `next_id`, and create `NNNN-short-slug.md` with complete
frontmatter and the default body sections. Record the observed current state, scope boundaries, likely
approach, acceptance criteria, verification, and material open questions.

Use `ready` only when no unresolved decision materially changes execution;
otherwise `proposed`. Do not implement the task or infer a release version.

When the user adds several related tasks at once toward one aim, ask whether to
group them under a goal (see Goals in format.md): a new goal task with its
folder, or an existing goal. Suggest a goal for a single task that is clearly
many tasks' worth of work. A task in a goal is created in the goal's folder.
