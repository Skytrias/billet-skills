---
name: billet-finish
description: Verify and close a completed project task and add a user-facing Unreleased changelog entry when the user explicitly invokes billet-finish (`$billet-finish` in Codex, `/billet-finish` in Claude Code).
---

# Finish task

Use only when explicitly invoked as `$billet-finish` or `/billet-finish`.
Follow [../billet-add/format.md](../billet-add/format.md).

Confirm the task's acceptance criteria and recorded verification actually
passed. Add a `## Result` section with the completed outcome and
verification, set `done` and `finished`, and clear `running`. Add a
concise meaningful user-facing item under `Unreleased` in `CHANGELOG.md`. Do
not close a partial or unverified task; state the blocker instead.
