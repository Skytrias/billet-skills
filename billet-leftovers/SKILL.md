---
name: billet-leftovers
description: Check whether recent work actually finished what it set out to do and turn real leftovers into new project tasks when the user explicitly invokes billet-leftovers (`$billet-leftovers` in Codex, `/billet-leftovers` in Claude Code).
---

# Task leftovers

Use only when explicitly invoked as `$billet-leftovers` or
`/billet-leftovers`. Follow
[../billet-add/format.md](../billet-add/format.md).

Compare the task or session in question (current conversation, named task,
branch, or commit range) with what actually landed: diff, task acceptance
criteria, verification results, and new `TODO`/`FIXME` markers. Look for
skipped or partial criteria, failing or unrun checks, deferred follow-ups
mentioned along the way, temporary workarounds, and newly exposed bugs.

For each real leftover, update an existing open task when one already covers
it; otherwise add a new task, `proposed` unless it is clearly `ready`, with
the observed evidence in its current state. Ignore polish nobody asked for.
If the work was a task still open, note the leftovers in its body. Report
what was created or updated, and say plainly when nothing is left.
