---
name: extract-embedded-web-state
description: Extract structured records and configuration embedded in public HTML or script payloads, including hydration data, JSON-LD, serialized page props, and inline application state. Use when the initial response contains the needed data outside the rendered DOM.
---

# Extract Embedded Web State

Recover structured data already shipped in a page response before introducing browser automation or reverse-engineering additional endpoints.

## Locate candidate state

Fetch the permitted page with an ordinary HTTP client and retain the final URL, status, content type, and a minimal redacted fixture. Inspect script elements, metadata, and relevant attributes for:

- `application/ld+json` and other JSON script blocks;
- framework hydration or page-prop payloads;
- inline assignments and serialized application state;
- configuration objects, initial caches, and preload metadata.

Prefer explicit identifiers and content types over framework-name assumptions. Confirm that a candidate contains the target fields before building extraction around it.

## Decode without executing

Parse HTML first, isolate the smallest candidate payload, and decode it according to its actual serialization. Handle HTML entities, escaped JSON strings, nested serialization, and non-strict JavaScript deliberately. Do not evaluate page scripts to obtain data that can be decoded as data.

For JavaScript assignments, locate the assignment boundary with a parser or balanced-token scan rather than a greedy regular expression over the full document. Reject ambiguous or truncated payloads and preserve the original fragment as a redacted test fixture.

## Identify stable records

Trace the path from the payload root to the desired records. Separate content fields from build IDs, cache keys, framework internals, and presentation state. Normalize types only after extraction, and retain source URL plus a precise payload location for provenance.

Compare at least two representative pages when designing a reusable extractor. Treat object ordering, optional fields, and framework-generated paths as unstable unless evidence shows otherwise.

## Verify the result

Validate required fields, record counts, unique identifiers, and a small sample against the user-visible page. Detect error pages and consent or login interstitials before treating missing state as an empty result.

Use a browser only when the required state is created after the initial response. If the embedded payload merely supplies parameters for a later request, report that boundary and hand the endpoint discovery to the appropriate API-mapping workflow.

Deliver the extraction path, decoding assumptions, normalized output schema, provenance, and fixtures covering ordinary, missing, escaped, and malformed payloads.
