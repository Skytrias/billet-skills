---
name: billet-critique
description: Critique one project task's plan before work starts, finding weak spots, wrong assumptions, and missing decisions, when the user explicitly invokes billet-critique (`$billet-critique` in Codex, `/billet-critique` in Claude Code).
---

# Critique task

Use only when explicitly invoked as `$billet-critique` or
`/billet-critique`. Follow
[../billet-add/format.md](../billet-add/format.md).

Read the task and the code it touches, then challenge the plan:

- Does the outcome solve the real problem, or a symptom?
- Do the stated current state and assumptions match the code?
- Is the scope bounded, and is anything important missing from it?
- Is there a simpler approach, or existing code to reuse?
- Are the acceptance criteria observable, and does the verification prove them?
- What breaks at the edges: errors, empty or large data, platforms, performance?
- Is the hardness honest, and are dependencies captured in `blocked_by`?

Report findings ranked by impact, each with a concrete suggested change. Edit
the task only for changes the user accepts; move it to `proposed` if a
material open decision surfaced.
