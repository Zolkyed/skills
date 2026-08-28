---
name: authenticated-http-request
description: Establish an authorized website session once in Zendriver or Patchright, inspect its login traffic with mitmproxy when needed, and transfer the resulting cookies and tokens into curl_cffi for continued browser-free HTTP requests.
---

# Authenticated HTTP Requests

Use a browser only to complete an authorized login boundary, then continue the permitted workflow with a persistent `curl_cffi` session.

## Define the handoff

Confirm the target origins, account or role, login path, and a harmless authenticated endpoint that can verify the handoff. Use only credentials and session state the user is authorized to operate. Keep credentials, cookies, tokens, captured bodies, and personal data out of source control, command history, logs, and reports.

Use Zendriver as the default browser driver. Use Patchright when Playwright-compatible controls or its surrounding project integration are more useful. Start mitmproxy only when browser events and exported storage do not explain the session lifecycle; filter captures to the approved origins.

## Establish the browser session

Launch a dedicated temporary browser profile, perform the login once, and wait for an observable authenticated state. Collect only the state needed for the handoff:

- cookies with domain, path, expiry, `Secure`, and `SameSite` metadata;
- CSRF values and their source;
- authorization and refresh tokens when the application exposes them to the client;
- redirect order and state-setting responses;
- required origin, referrer, content-type, or request-signing context.

Treat secret values as opaque. Preserve scope and expiry metadata instead of flattening all cookies into a single header.

## Transfer to curl_cffi

Create a persistent `curl_cffi.requests.Session`. Import cookies into its cookie jar with their original domain and path, and supply other secret state through an existing secret provider, protected environment variables, or an explicitly approved local store.

Reproduce the smallest request sequence needed after login. Set ordinary headers only when captured evidence shows they are required. Select client impersonation behavior only when a controlled comparison demonstrates that it matters.

Verify the handoff using a stable, non-sensitive response property that distinguishes authenticated from unauthenticated behavior. Do not rely on the status code alone. Exercise refresh or reauthentication once when the application has a legitimate session-lifecycle path.

## Handle transfer boundaries

If replay fails, compare the earliest divergent browser and HTTP exchanges. Check cookie scope, redirect handling, CSRF coupling, token freshness, request order, encoding, HTTP version, and client impersonation before adding arbitrary headers.

When the session depends on browser-held keys, user presence, or non-transferable application state, retain the browser for that boundary and hand off only after it. Report the boundary explicitly.

Remove the temporary browser profile and sensitive mitmproxy capture after extracting the required flow. Deliver the browser bootstrap, the minimal `curl_cffi` handoff, lifecycle notes, redacted evidence, and offline tests for cookie scoping, CSRF propagation, redirects, and secret redaction.
