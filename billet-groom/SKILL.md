---
name: billet-groom
description: Clean up a project's task board, both its data and its accuracy against the current code, when the user explicitly invokes billet-groom (`$billet-groom` in Codex, `/billet-groom` in Claude Code).
---

# Groom tasks

Use only when explicitly invoked as `$billet-groom` or `/billet-groom`.
Follow [../billet-add/format.md](../billet-add/format.md).

Data: check every task file's header, never its body, for valid, complete,
pretty-printed frontmatter, filenames matching IDs, duplicate IDs, `next_id`
above every ID (archive included), consistent areas, sensible `order`,
`blocked_by` pointing at existing tasks, `running` set on tasks nobody is
working on, and goal folders (see Goals): each with its goal file, none nested,
and an open goal whose tasks are all closed. Mention how many closed tasks qualify for `billet-archive`.

Code: for each open task, compare its current state, scope, and approach with
the code as it is now. With more than about 30 open tasks, go area by area and
ask the user which areas to review first. Find tasks already done or made obsolete by other
work, tasks whose assumptions no longer hold, duplicates, and `proposed`
tasks whose questions are now answered.

Fix mechanical data problems directly. For anything that changes meaning
(status, scope, cancel, merge, reorder), present the proposed changes and
apply them once the user agrees. Report what changed and what still needs a
decision.
