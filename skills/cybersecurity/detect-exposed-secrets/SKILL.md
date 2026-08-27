---
name: detect-exposed-secrets
description: Detect and triage exposed credentials, tokens, private keys, and sensitive configuration in an authorized repository or provided artifacts. Use for secret scanning and leak response; do not retrieve secrets from unrelated systems or print recovered values.
---

# Detect Exposed Secrets

Locate potential secret exposure without spreading the secret further.

## Define the scan surface

Confirm whether scope includes the working tree, untracked files, generated artifacts, build output, configuration, fixtures, logs, documentation, and Git history. History scanning is broader and may be expensive; do it only when requested or clearly required by a reported leak.

Use repository-configured scanners first. Combine high-confidence format detectors with entropy or keyword heuristics, then inspect context. Exclude dependency caches, binaries, and generated data only with a documented reason.

## Handle matches safely

Never print a complete candidate secret. Report a stable fingerprint, type, location, and redacted prefix or suffix only when needed for identification. Do not place candidates in commands, chat, patches, tickets, test output, or new files.

Classify each match as:

- confirmed credential or private key;
- likely secret requiring owner verification;
- public identifier or intentionally publishable key;
- example, placeholder, fixture, checksum, or false positive.

Do not test a credential against a live service unless the user explicitly authorizes that validation and owns the target. A syntactically valid token can still be inactive; treat status as unknown without safe evidence.

## Respond to confirmed exposure

Contain first: identify the credential owner and affected system, revoke or rotate through the approved operational process, and preserve only minimal incident evidence. Removing the string from the latest commit does not revoke it or remove it from history.

After rotation, remove the value from tracked content, add an appropriate secret source or placeholder, and add a narrow prevention control. Rewriting published history is disruptive and does not erase forks, caches, logs, or clones; propose it separately and obtain explicit approval.

## Report

Report counts and classifications, redacted locations, whether history was scanned, scanner configuration, confirmed response actions, remaining exposure channels, and false-positive suppressions. Never include recoverable secret material.
