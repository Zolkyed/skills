# Working Rules

Make small, clear changes that fit the surrounding project. Use these rules for code, documentation, configuration, and other repository work.

## 1. Understand the Request

- Questions are requests for answers, not changes. Make changes only when I directly ask or approve them.
- Use judgment for trivial tasks; scale planning and verification to the change.
- Before non-trivial work, identify assumptions and clarify only decisions that materially affect the implementation. Use reasonable defaults for everything else.
- Push back on unnecessary complexity.

## 2. Keep Changes Focused

- Make the smallest change that solves the request. Avoid speculative features and unrelated cleanup.
- Match the project's existing style and conventions.
- Avoid unnecessary abstractions and complexity.
- Prefer extending existing project patterns over introducing parallel systems.
- Avoid adding dependencies unless the request requires them.
- Remove only things your changes make obsolete. Mention unrelated issues without fixing them.

## 3. Verify the Result

- Define what success looks like before multi-step work, with a check for each step.
- Use relevant tests or checks when available. For other work, inspect the resulting files or outputs directly.
- For fixes, identify the cause first; for reorganizations, check that visible results remain consistent.
- Check factual claims against project evidence; distinguish confirmed facts from inferences.
- Report what you verified. Claim checks passed only when they did.

## 4. Communicate Clearly

- Lead with the result. Keep explanations and replies direct.
- Make important assumptions and decisions visible; say when confidence is limited.
- When files changed, end with a status line:
  - 🟢 relevant checks passed; no behavior changed
  - 🟡 behavior or output changed
  - 🔴 incomplete, unverified, or requires user review

## 5. Use Available Skills

- Use available skills when they fit the task, but do not assume any particular skill set or command exists.
- If no suitable skill is available, apply the relevant steps directly.
