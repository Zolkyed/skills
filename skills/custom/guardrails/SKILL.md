---
name: guardrails
description: "Wire a repo's own checks into Claude Code so work can't end red: a Stop hook that runs typecheck, lint and tests, plus deny rules for destructive commands."
disable-model-invocation: true
---

A rule in a prompt can be forgotten; a **guardrail** cannot. This skill turns "verify before claiming done" into a Stop hook that sends Claude back to work while the repo's checks are red, and turns "ask before destroying things" into permission deny rules.

`retro` finds missing checks after a session. This skill installs the Claude Code side of them up front.

## Steps

1. **Find the repo's checks.** Read `package.json` scripts, `Makefile`, `pyproject.toml`, `Cargo.toml`, `justfile`, and the CI workflow. List the typecheck, lint and test commands the project already uses. Prefer the fast variants: changed files only, or the unit suite over e2e. Done when each command has been run once and its pass/fail output seen. A check that is already red is a finding: report it rather than wiring it in.
2. **Agree the set with the user.** Show the commands, how long each one takes, and where they will run. Keep the Stop hook under about 60 seconds in total. Slower suites belong in CI.
3. **Install the hook script.** Copy [check.sh](check.sh) from this skill's directory to `.agents/hooks/check.sh` in the repo, then run `chmod +x`. It detects typecheck, lint and test commands from `package.json`, `Cargo.toml`, `go.mod` or `pyproject.toml`. When the agreed set differs from what it detects, edit its `checks` list to match. Run it once by hand (`echo '{}' | bash .agents/hooks/check.sh`) to confirm it picks up the agreed commands.

   It sends the agent back only once per turn, and its message lets an intentional red (a TDD red step, a bug repro being shown to the user) stop after saying so, so it works alongside `tdd` and `diagnosing-bugs`.
4. **Register the hook and the deny rules** in `.claude/settings.json`, merging into whatever is already there:

   ```json
   {
     "hooks": {
       "Stop": [{ "hooks": [{ "type": "command", "command": "bash \"$CLAUDE_PROJECT_DIR/.agents/hooks/check.sh\"", "timeout": 180 }] }]
     },
     "permissions": {
       "deny": [
         "Bash(git push --force:*)",
         "Bash(git push -f:*)",
         "Bash(git reset --hard:*)",
         "Bash(git clean -f:*)",
         "Bash(rm -rf:*)"
       ]
     }
   }
   ```

   Add the repo's own irreversible commands to the deny list, such as migrations or deploy scripts, after confirming them with the user.
5. **Prove it works.** Break a check on purpose (a failing assertion or a type error), run the hook script by hand, and confirm it exits 2 with the failure shown. Revert the break and confirm it exits 0.

Done when the hook has been seen to go red on a broken check and green on a clean tree, and the deny rules are in `.claude/settings.json`.
