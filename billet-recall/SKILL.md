---
name: billet-recall
description: Answer what a project's earlier tasks and docs already know about a topic, with links, when the user explicitly invokes billet-recall (`$billet-recall` in Codex, `/billet-recall` in Claude Code).
---

# Recall

Use only when explicitly invoked as `$billet-recall` or `/billet-recall`.
Follow [../billet-add/format.md](../billet-add/format.md).

Search earlier tasks for the topic, archive included, trying related terms as
well as the user's own, and check the project's docs. Rank the matches and
read only the closest few (see Reading the task folder in format.md). Answer from what they record, linking each
claim to its task or doc. Check the claims against the code and say when one no
longer holds. Say plainly when nothing is recorded, and mark anything you
learned only from the code. Do not edit anything; name wrong findings so the
user can have them corrected.
