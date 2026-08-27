---
name: crawl-large-sites
description: Build or operate resumable crawlers over many public pages. Use when collection needs a URL frontier, checkpoints, deduplication, bounded retries, incremental output, or safe restart behavior; use a single-page scraping skill for small extractions.
---

# Crawl Large Sites

Design the crawl as a recoverable data pipeline, not a long loop that starts over after failure.

## Define the crawl contract

Before implementation, establish:

- allowed hosts and path patterns;
- seed URLs and discovery sources such as sitemaps, feeds, pagination, and page links;
- record identity and output schema;
- URL and record deduplication rules;
- stopping conditions and expected scale;
- refresh policy when previously visited pages can change.

Keep the frontier restricted to the approved scope. Normalize URLs deliberately: remove fragments, resolve relative links, normalize host casing and default ports, and change query parameters only when their semantics are known. Treat declared canonical URLs as evidence, not unconditional commands that can escape scope.

## Make progress durable

Persist enough state to resume safely:

- frontier items with pending, active, complete, retryable, or terminal status;
- attempt count, last error, and next eligible retry time;
- final URL after redirects, response status, fetch time, and content fingerprint;
- emitted record identifiers and source URLs.

Write records incrementally using an append-safe or transactional strategy. Make processing idempotent so replaying an active item after a crash cannot duplicate output. Use atomic checkpoint replacement or a transactional store; never leave the only checkpoint half-written.

## Schedule responsibly

Apply per-host concurrency and delay limits. Honor retry guidance and use bounded exponential backoff with jitter for transient failures. Do not retry permanent client errors blindly. Put exhausted items in a reviewable failure set instead of blocking the entire crawl.

Do not bypass authentication, CAPTCHAs, paywalls, robots restrictions, rate limits, or other technical access controls. Stop when the site signals blocking or when continued collection would exceed the approved scope.

## Verify completion

Report counts for discovered, completed, skipped, retrying, and failed URLs; unique records; duplicates; and out-of-scope links. Sample early, middle, and terminal pages against the source. A crawl is complete only when the in-scope frontier is exhausted or a documented stopping condition is reached. Preserve failure details and coverage limits rather than claiming silent completeness.

Document the resume command, state location, output schema, scope rules, and how operators can inspect or retry failures.
