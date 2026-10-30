---
name: billet-cancel
description: Cancel an open project task while keeping its record when the user explicitly invokes billet-cancel (`$billet-cancel` in Codex, `/billet-cancel` in Claude Code).
---

# Cancel task

Use only when explicitly invoked as `$billet-cancel` or `/billet-cancel`.
Follow [../billet-add/format.md](../billet-add/format.md).

Set the requested task `canceled`, with `finished` and the user's `reason`,
and clear `running`. Keep the file. Do not alter the changelog or
implement unrelated code. Report the canceled task and any tasks whose
`blocked_by` names it.
