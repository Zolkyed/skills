# Working Rules

Rules for writing clean code: small, simple, verified, and in the style of the code around it.

**Tradeoff:** These rules favour caution over speed. For trivial tasks, use judgment.

## 1. Answer Before Acting

**A question is a request for an answer, not a change.**

- When I ask a question or think out loud, answer it. Change files only after I approve the approach. An approved ticket or spec counts as approval.
- Ask before pushing, deleting files or branches, running migrations, or adding dependencies.

The test: Every file change follows an explicit go-ahead.

## 2. Think Before Coding

**Surface assumptions. Name ambiguity. Push back.**

For non-trivial work, before writing code:
- Restate the task and list your assumptions, including what I haven't told you.
- If the request could mean two things, give both readings and let me pick.
- If a wrong guess would be costly, ask. For larger plans, suggest `/grill-with-docs`.
- If my plan is overcomplicated, say so. Disagreement is welcome.

When designing:
- Offer 2–3 options with a recommendation.
- Note what would hurt first if this had to grow 100×.

## 3. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- Build only what was asked.
- Add abstractions, options and error paths only when the request needs them.
- If 200 lines could be 50, rewrite.

The test: Would a senior engineer call this overcomplicated? If yes, simplify.

## 4. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

- Match the surrounding style, even where you'd write it differently.
- Remove imports, variables and functions that your change made unused.
- Mention unrelated problems you notice; leave the fix to a separate change.

The test: Every changed line traces directly to the request.

## 5. Verify, Then Claim

**Define done up front. Prove it before saying it.**

- Write a failing test and a one-screen plan before editing (`tdd`).
- For multi-step work, give each step a check:
  ```
  1. [Step] → verify: [check]
  2. [Step] → verify: [check]
  ```
- Before claiming done, follow `verification-before-completion`.
- Before committing, run `deslop` on the diff.
- Mark each claim about the code as confirmed (read, ran, grepped) or inferred.

## 6. Report Plainly

**Result first. Decisions visible. Weak spots honest.**

- Lead with a one-line result.
- End every reply that changed files with one line: a light, then what changed in at most 10 plain words.
  - 🟢 nothing works differently · 🟡 behaviour changed · 🔴 needs my review
  - Give 🟢 only when the checks ran and passed. When unsure, pick the next colour up.
- After non-trivial work, list the major decisions you made and why, then what you're least confident about.
- Run commit messages, PR text and review replies through `unslop`.
- When review feedback arrives, follow `receiving-code-review`.
