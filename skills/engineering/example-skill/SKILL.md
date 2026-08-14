---
name: example-skill
description: Example skill demonstrating the SKILL.md format for this collection. Ships a branch end-to-end - commit, push, PR, wait for checks, merge - using gh CLI, matching a Conventional-Commits + squash-merge workflow. Use when the user asks to "ship" a change, or wants the full commit-to-merge sequence run consistently.
---

Ships the current branch's staged/committed changes through to a merged PR, in a fixed order, so the sequence never varies between runs.

## Process

### 1. Verify before committing

Run the repo's canonical `verify` (or `check`) command. Do not proceed if it fails — fix first.

### 2. Commit with a message file, not a heredoc

Some shells alias `cat` (e.g. to `bat`) in ways that silently break `$(cat <<EOF ... EOF)` command substitution, producing an empty commit message with no error. Always write the message to a temp file and commit with `-F <file>`:

```bash
git commit -F /path/to/scratch/commit-msg.txt
```

Same rule for PR bodies — use `gh pr create --body-file <file>`, never `--body "$(cat <<EOF...)"`.

### 3. Push and open the PR

```bash
git push -u origin <branch>
gh pr create --title "<type>: <description>" --body-file <file> --base main --head <branch>
```

### 4. Wait for checks, don't guess

Poll `gh pr checks <n>` until nothing is `pending`. Never merge on an assumption that checks "probably passed."

### 5. Merge

```bash
gh pr merge <n> --squash --delete-branch
```

Confirm the merge actually landed (`gh pr view <n> --json state`) before reporting done.
