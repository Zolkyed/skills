---
name: diagnose-scraper-failure
description: Diagnose why an authorized scraper that previously worked now fails, returns incomplete data, or diverges from browser behavior. Use for evidence-based triage of transport, session, request, response, extraction, pagination, and output regressions.
---

# Diagnose Scraper Failures

Find the earliest layer where current behavior diverges from a known-good run, then identify the smallest supported correction. Diagnose first; implement a fix only when the user requests it.

## Define the failure

Capture the expected result, actual result, first known failing run, last known working run, affected targets, and whether failure is complete, intermittent, or partial. Preserve redacted evidence such as status, final URL, redirect chain, content type, stable response fingerprint, record count, and terminal state.

Reproduce once with conservative request volume. Do not obscure the first failure with broad retries, fresh selectors, extra headers, or a different client.

## Locate the first divergence

Compare current and known-good behavior in order:

1. DNS, connection, TLS, proxy, and HTTP negotiation;
2. redirects, authentication state, cookies, CSRF, and token freshness;
3. URL, method, headers, query, body, and request ordering;
4. status, content type, response shape, and blocking or interstitial pages;
5. embedded state, API schema, DOM structure, and selectors;
6. pagination state, termination, deduplication, and checkpoints;
7. normalization, validation, persistence, and downstream output.

Stop descending once an upstream divergence explains downstream symptoms. A selector failure on a login page is an authentication problem, not evidence that the selector changed.

## Test hypotheses narrowly

Form each hypothesis from observed differences and change one logical variable at a time. Use saved fixtures for extraction and normalization tests so live-site variance does not contaminate them. When browser behavior still works, compare it with the HTTP client at the earliest differing exchange.

Distinguish deterministic breakage from session expiry, cache effects, locale or account variation, rollout differences, throttling, and transient server failures. Repeat only enough trials to establish which class applies, with explicit bounds.

## Report the diagnosis

State the root cause when evidence supports it; otherwise rank remaining hypotheses and name the smallest experiment that would distinguish them. Provide:

- the earliest divergence and supporting evidence;
- affected layer and blast radius;
- confidence and unresolved uncertainty;
- the minimal recommended correction;
- a regression test or monitoring signal that would catch recurrence.

Keep captured secrets and personal data redacted. Do not publish raw response bodies when a stable fingerprint or minimal sanitized fixture is sufficient.
