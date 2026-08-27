---
name: scrape-browser-sites
description: Extract structured data from web pages that require JavaScript rendering or permitted browser interaction. Use for dynamic content, infinite scrolling, and browser-only state; use HTTP parsing when the initial response already contains the needed data.
---

# Scrape Browser Sites

Use browser automation only for the part of collection that genuinely requires a browser.

## Approach

1. Define the target records, fields, and stopping condition. Inspect the initial response and public network activity first; prefer a documented API or direct HTTP collection when it provides the same permitted data reliably.
2. Wait for observable application state—a specific element, response, or URL change—not fixed sleeps.
3. Prefer accessible roles, labels, stable attributes, and user-visible text for interaction. Avoid generated class names and deep DOM paths.
4. Make pagination, load-more behavior, or infinite-scroll termination explicit. Track record identifiers to deduplicate results and detect stalled loops.
5. Keep navigation and interaction separate from extraction and normalization. Save minimal fixtures or snapshots needed to test parsing without repeatedly driving the live site.
6. Validate representative records, empty states, and the terminal page or scroll state before running at scale.

## Collection discipline

- Follow the site's terms and applicable access constraints. Do not evade authentication, CAPTCHAs, paywalls, rate limits, or anti-bot controls.
- Reuse sessions only when the user is authorized to access the data. Keep credentials outside source code and redact cookies, tokens, and personal data from logs and artifacts.
- Limit concurrency, bound retries, and stop when the site signals blocking or the expected page state no longer appears.
- Capture source URLs and useful provenance. Surface partial runs and selector drift instead of silently returning incomplete data.

## Deliverable

Document prerequisites, configuration, output schema, and known limits. When adding code to a repository, include focused tests for extraction logic and a small smoke path for the browser flow when the project supports it.
