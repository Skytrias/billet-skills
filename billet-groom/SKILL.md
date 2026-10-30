---
name: billet-groom
description: Clean up a project's task board, both its data and its accuracy against the current code, when the user explicitly invokes billet-groom (`$billet-groom` in Codex, `/billet-groom` in Claude Code).
---

# Groom tasks

Use only when explicitly invoked as `$billet-groom` or `/billet-groom`.
Follow [../billet-add/format.md](../billet-add/format.md).

Data: check every task file for valid, complete, pretty-printed frontmatter,
filenames matching IDs, `next_id` above every ID, consistent areas, sensible
`order`, `blocked_by` pointing at existing open tasks, and `running` set on
tasks nobody is working on.

Code: for each open task, compare its current state, scope, and approach with
the code as it is now. Find tasks already done or made obsolete by other
work, tasks whose assumptions no longer hold, duplicates, and `proposed`
tasks whose questions are now answered.

Fix mechanical data problems directly. For anything that changes meaning
(status, scope, cancel, merge, reorder), present the proposed changes and
apply them once the user agrees. Report what changed and what still needs a
decision.
