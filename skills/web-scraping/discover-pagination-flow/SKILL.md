---
name: discover-pagination-flow
description: Determine and implement the pagination contract used by an authorized website or API, including page, offset, cursor, load-more, and infinite-scroll flows. Use when one page can be collected but traversal and reliable termination are not yet understood.
---

# Discover Pagination Flows

Turn a verified single-page extraction into a bounded traversal that neither skips records nor loops indefinitely.

## Establish the first transition

Define the target record identity and capture a redacted baseline for the first page. Trigger exactly one next-page action and compare the two requests and responses. Identify:

- page number, offset, limit, cursor, continuation token, or next URL;
- where the next value comes from and whether it is opaque;
- sort, filter, locale, account, and session state coupled to pagination;
- record ordering and overlap between adjacent pages;
- explicit and implicit end-of-data signals.

Prefer a documented next link or response cursor. Treat cursors and continuation tokens as opaque values; do not synthesize them from apparent internal structure.

## Prove the contract

Advance through several controlled transitions and record the input state, returned record identities, next state, and terminal indicators. Distinguish an empty terminal page from an error, expired session, throttling response, repeated cursor, or unchanged infinite-scroll result.

Test only variations needed to resolve uncertainty, such as whether limit changes affect cursors or whether filters must remain byte-for-byte stable. Keep request volume and retries bounded.

## Implement traversal

Maintain an explicit pagination state and a set of seen cursors, URLs, page states, and record identifiers. Stop when any configured bound is reached or when:

- the response declares completion;
- no next state is present;
- a cursor or page state repeats;
- no new record identifiers appear under a documented terminal rule;
- the response no longer matches the verified page shape.

Checkpoint the next state and emitted record IDs when the run must be resumable. Update the checkpoint only after durable output succeeds so a restart cannot silently skip a page.

Do not infer completeness only from a short page unless the observed contract supports it. Surface duplicates, ordering changes, gaps, and partial termination instead of silently normalizing them away.

## Validate and deliver

Test the first transition, a middle transition, the terminal condition, a repeated cursor, and recovery from an interrupted run when resumability is required. Deliver the pagination contract, stopping rules, safety bounds, deduplication key, checkpoint format, and a minimal implementation using the least expensive permitted client.
