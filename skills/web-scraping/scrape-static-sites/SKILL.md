---
name: scrape-static-sites
description: Extract structured data from public web pages whose useful content is present in the initial HTTP response. Use for HTML parsing, pagination, and repeatable HTTP-based collection; use a browser-oriented skill when content requires JavaScript or interaction.
---

# Scrape Static Sites

Build the smallest reliable HTTP-based collector for the requested data.

## Approach

1. Inspect the page and identify the exact fields, records, and stopping condition before writing the scraper.
2. Confirm that the required content is present in the raw response. If it depends on JavaScript, browser interaction, or an authenticated session, switch to a browser-based approach.
3. Prefer stable semantic selectors and embedded structured data over brittle position-based selectors. Treat CSS classes that look generated as unstable.
4. Separate fetching, parsing, normalization, and output so parsing can be tested against saved fixtures without repeated network requests.
5. Handle pagination explicitly. Deduplicate records and stop on a known terminal condition rather than guessing an arbitrary page count.
6. Validate a small sample against the source, including missing fields and the final page, before scaling up.

## Collection discipline

- Check the site's terms, robots guidance, and applicable access constraints. Do not bypass authentication, CAPTCHAs, paywalls, or technical access controls.
- Identify the client honestly, keep concurrency conservative, respect retry hints, and use bounded exponential backoff for transient failures.
- Cache responses while developing when practical. Never log cookies, authorization headers, personal data, or other secrets.
- Preserve source URLs and enough provenance to audit extracted records.
- Fail visibly when the page shape changes; do not silently emit plausible but incomplete data.

## Deliverable

Document how to run the collector, its output schema, required configuration, and known coverage limits. Include parser fixtures or focused tests for representative, missing-field, and pagination cases when code is being added to a repository.
