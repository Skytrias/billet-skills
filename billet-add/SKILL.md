---
name: billet-add
description: Analyze a proposed project task and add it as one task file with JSON frontmatter when the user explicitly invokes billet-add (`$billet-add` in Codex, `/billet-add` in Claude Code).
---

# Add task

Use only when explicitly invoked as `$billet-add` or `/billet-add`.
Follow [format.md](format.md) for the folder, file layout, and all values.

Read the existing task files and relevant source/docs; avoid duplicates and
reuse existing areas. Take the ID from `next_id` in `tasks.json`, increment
it, and create `NNNN-short-slug.md` with complete frontmatter and the default
body sections. Record the observed current state, scope boundaries, likely
approach, acceptance criteria, verification, and material open questions.

Use `ready` only when no unresolved decision materially changes execution;
otherwise `proposed`. Do not implement the task or infer a release version.
