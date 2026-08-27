---
name: map-website-apis
description: Document the permitted network API used by a website by observing browser traffic, tracing client-side request construction, and replaying requests safely. Use for authorized API discovery or client interoperability; do not use for ordinary page extraction or bypassing access controls.
---

# Map Website APIs

Produce an evidence-backed description of a website's reachable API behavior that an authorized developer can reproduce without guessing.

## Establish authority and scope

Confirm the target hosts, user-visible flows, account or role being tested, and intended use. Limit observation and replay to traffic the user is authorized to generate. Do not bypass authentication, authorization, CAPTCHAs, paywalls, signing controls, rate limits, or anti-bot systems. Never test other users' identifiers or attempt privilege escalation.

Keep credentials, cookies, authorization headers, personal data, and captured payloads out of source control and reports. Use placeholders in examples and retain sensitive captures only as long as necessary.

## Observe before interpreting

For each approved flow, capture the browser's requests and responses while recording the action that triggered them. Group noise such as analytics and static assets separately. Identify:

- method, origin, path, query, and content type;
- required headers, cookies, tokens, and their legitimate acquisition flow;
- request and response shapes, pagination, errors, and rate-limit signals;
- ordering, state, and identifiers shared across multi-request flows.

Treat a single capture as an observation, not a complete contract. Compare controlled variations to distinguish constants, user input, session state, timestamps, and computed values.

## Trace request construction when needed

Use readable client source, source maps, or downloaded public bundles to locate endpoint strings, serializers, parameter builders, and response consumers. Follow only the code needed to explain observed behavior. Mark minified-code interpretations as lower-confidence until confirmed by a controlled replay.

Prefer a documented public API when it covers the use case. Do not publish proprietary implementation code or secrets discovered in bundles.

## Replay minimally

Reproduce the smallest authorized request with secrets supplied through environment variables or an existing permitted session. Start with read-only behavior. Bound retries and request volume, preserve server error responses, and stop on blocking or unexpected authorization behavior.

For multi-step flows, document the state transition and provide a small replay script only when prose and a single request are insufficient. The script must validate required configuration, redact logs, avoid embedded credentials, and expose a conservative request limit.

## Document evidence and confidence

Write one entry per endpoint or coherent flow with purpose, evidence source, confidence, request schema, response schema, authentication prerequisites, pagination, errors, and a redacted example. Separate observed facts from inference. Record unknowns and the exact authorized experiment that could resolve each one.
