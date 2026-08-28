---
name: minimize-http-request
description: Reduce a working authorized HTTP replay to the smallest reliable request by determining which captured headers, cookies, parameters, and preceding requests are actually required. Use when a browser-derived request works but contains unexplained or unnecessary state.
---

# Minimize HTTP Requests

Turn a known-working authorized request into a small, explainable, repeatable HTTP request without guessing which captured browser fields matter.

## Establish a baseline

Choose one harmless endpoint and one stable response property that proves the replay still works. Save a redacted representation of the known-working request and response. Keep cookies, tokens, credentials, and personal data out of logs, fixtures, and source control.

Hold the account, session, URL, method, body, client impersonation, network path, and timing constant while minimizing. If the baseline is unstable, fix that before interpreting removal experiments.

## Classify captured state

Group inputs before testing them:

- protocol-managed fields such as `Host`, `Content-Length`, and connection headers;
- representation fields such as `Content-Type` and `Accept`;
- authentication, cookies, CSRF state, and request signatures;
- origin-context fields such as `Origin`, `Referer`, and fetch metadata;
- client hints, user-agent fields, tracing IDs, analytics, and browser noise;
- query parameters, form fields, JSON properties, and preceding state-setting requests.

Let the HTTP client calculate protocol-managed fields. Preserve opaque signatures and coupled values until their acquisition and validation rules are understood.

## Minimize systematically

Start from the working request and remove groups of related inputs. If removing a group breaks the verification property, restore it and split the group until the required member or dependency is isolated. Repeat individual trials when session freshness or server variance could create a false result.

Test in a deliberate order:

1. tracing, analytics, priority, and navigation-only fields;
2. client hints and browser-generated metadata;
3. optional negotiation headers;
4. origin-context headers;
5. cookies individually while preserving their scope;
6. query, body, and preceding-flow state.

Change one logical variable per comparison. Record pass, fail, redirect, challenge, and response differences. A field is required only when repeated controlled trials support that conclusion; a single successful omission is not enough when the endpoint is stateful.

Check interactions after finding individually removable fields. Two optional-looking values may become required when both are absent. Finish by replaying the final minimal request in a fresh authorized session.

## Implement the replay

Use a persistent `curl_cffi.requests.Session` when cookies or redirects are involved. Configure only the headers supported by the experiments, allow the client to manage its cookie jar, and select client impersonation only when the baseline proves it matters.

Produce the minimal request, a redacted removal matrix, required state-acquisition steps, and any conditional dependencies. Keep retry counts and request volume bounded, and stop when the endpoint no longer behaves like the approved baseline.
