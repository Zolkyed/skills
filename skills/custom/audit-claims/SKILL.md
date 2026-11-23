---
name: audit-claims
description: Check claims about a codebase against the code itself before acting on them, with each claim confirmed or refuted by file:line evidence. Use before building on findings from exploration or a subagent report, or when the user asks "is that actually true?".
---

Explorers hallucinate, and orchestrators trust them. An **audit** breaks that chain: every claim about the code has to point at the lines that prove it, and a fresh reader checks that the lines really say so.

## Steps

1. **List the claims.** Pull every factual claim about the code out of the findings: what calls what, where a value comes from, what a function does, what is unused, what a change would break. One claim per line, numbered. Opinions and plans are not claims; leave them out.
2. **Dispatch an auditor.** Start a subagent with a fresh context window. Give it the numbered claims and the repo path, and nothing of the reasoning that produced them. Its brief:

   > For each claim, find the code that decides it and give a verdict:
   > - **Confirmed**: quote the `file:line` range that proves it.
   > - **Refuted**: quote the `file:line` range that contradicts it, and state what is actually true.
   > - **Unverifiable**: say what you searched and why it did not settle the claim.
   >
   > Judge only from the code you read. A claim with no quoted lines is unverifiable.

3. **Act on the verdicts.** Build only on confirmed claims. Correct anything that was refuted, and tell the user when a refuted claim changes the plan. For each unverifiable claim, either find the evidence yourself or carry it forward explicitly marked as inferred.

Done when every claim the next step depends on is confirmed by quoted lines, or openly marked as inferred.
