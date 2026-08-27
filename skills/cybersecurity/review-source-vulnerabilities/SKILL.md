---
name: review-source-vulnerabilities
description: Review an authorized codebase for exploitable security defects by tracing untrusted input to sensitive operations and verifying reachable attack paths. Use for defensive source-code security reviews; use dependency or secret-specific skills for those narrower scans.
---

# Review Source Vulnerabilities

Find concrete, reachable vulnerabilities in code the user is authorized to assess. A suspicious pattern is a lead, not a finding.

## Establish scope

Identify the applications, languages, entry points, trust boundaries, data classifications, and threat actors in scope. Read repository security guidance and architecture decisions. Do not expand into external systems, production testing, or credentials merely because the code references them.

## Map attack paths

Start from attacker-controlled inputs: HTTP parameters and headers, uploads, webhooks, messages, serialized data, environment or tenant configuration, database content that can become second-order input, and model or tool output. Trace validation, normalization, authorization, transformation, storage, and later use.

Prioritize sensitive sinks and trust decisions:

- database, shell, template, expression, and interpreter execution;
- filesystem paths, archives, parsers, URL fetches, redirects, and deserialization;
- authentication, session, authorization, tenant isolation, and object ownership;
- cryptographic verification, secret handling, logging, and error disclosure;
- browser output contexts, state-changing requests, and security headers;
- resource allocation, concurrency, recursion, and attacker-controlled amplification.

Use existing static-analysis tools when available, but inspect configuration and validate their results manually. Search for disabled checks and suppression comments as review leads, not automatic vulnerabilities.

## Prove before reporting

For each candidate, establish the source, path, missing or ineffective control, sink, preconditions, attacker capability, and impact. Prefer a focused test or minimal local reproducer that cannot affect real users or data. Do not create weaponized payloads, persistence, destructive side effects, or broad exploitation infrastructure.

Reject false positives explicitly when a control breaks the path. Distinguish reachable vulnerabilities from defense-in-depth improvements and unverified concerns.

## Report

Report findings by severity and confidence with affected locations, attack path, impact, safe reproduction evidence, remediation at the correct trust boundary, and a regression-test idea. Map to a versioned OWASP ASVS requirement when it genuinely fits; do not use checklist labels as proof. Include reviewed scope, tools, blind spots, and areas with no finding.
