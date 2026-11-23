---
name: cross-check
description: "Get a blind second opinion on a diff from a different model (Codex CLI), then verify each finding before acting on it."
disable-model-invocation: true
---

A model reviewing its own work shares its own blind spots. A **cross-check** sends the diff to a different model, with none of the reasoning behind it, to hunt for bugs. It complements `code-review`, which checks standards and spec. This skill looks only for things that are broken.

## Steps

1. **Pin the diff.** Use what the user names: uncommitted changes, a base branch, or a commit. With nothing named, take uncommitted changes, or the current branch against `main` when the tree is clean. Confirm the diff is non-empty before going further.
2. **Run the reviewer.** Check `codex --version`. If Codex is installed, run the matching command from the repo root:

   ```bash
   codex review --uncommitted "<brief>"
   codex review --base main "<brief>"
   codex review --commit <sha> "<brief>"
   ```

   Brief: *"Find bugs only: wrong behaviour, unhandled edge cases, race conditions, broken error paths, security holes, and changes that break existing callers. Skip style. For each finding give file:line, the failing scenario, and severity."*

   If Codex is not installed, tell the user, then run the same brief in a subagent with a fresh context window and a different model from the one that wrote the code.
3. **Verify each finding.** A second opinion is a lead, not a verdict. For each finding, read the cited code and reproduce the failing scenario with a test or a command where you can. Mark each one **confirmed**, **false alarm** (say why), or **unclear**.
4. **Report.** List confirmed findings first, worst first, each with its evidence. Then false alarms in one line each, then unclear ones. Ask before fixing anything.

Done when every finding has a verdict backed by the code or a run.
