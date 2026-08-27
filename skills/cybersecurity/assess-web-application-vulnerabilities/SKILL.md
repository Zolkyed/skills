---
name: assess-web-application-vulnerabilities
description: Perform a scoped, non-destructive security assessment of a web application or API the user is authorized to test. Use for defensive runtime vulnerability discovery and validation; do not use without explicit target authorization or for denial-of-service, persistence, or credential attacks.
---

# Assess Web Application Vulnerabilities

Assess only targets the user owns or is explicitly authorized to test. Follow the engagement scope over generic testing ambition.

## Confirm the engagement boundary

Before active testing, establish target hosts and environments, allowed accounts and roles, excluded paths and data, request-rate limits, time window, permitted techniques, evidence handling, and stop contacts. If authorization or target scope is unclear, restrict work to passive review and ask for clarification.

Never perform denial-of-service or stress testing, destructive writes, malware delivery, persistence, social engineering, credential stuffing, password spraying, broad account enumeration, data exfiltration, or testing against third-party infrastructure. Stop on service instability, unexpected access to another user's data, production side effects, or requests from the target owner.

## Build a coverage model

Map exposed hosts, routes, APIs, roles, authentication states, state-changing flows, uploads, integrations, and trust boundaries. Use the versioned OWASP Web Security Testing Guide as a coverage reference and OWASP ASVS as a control reference; choose tests relevant to the application rather than mechanically running every case.

Prioritize authorization and tenant isolation, session lifecycle, input handling, browser output contexts, request forgery protections, server-side URL fetching, file and parser boundaries, business-logic invariants, error leakage, security configuration, and API object or function authorization.

## Test safely and validate findings

Begin with passive observation and the least invasive request capable of answering the question. Use dedicated test accounts and synthetic records. Change one variable at a time, bound automation and retries, and preserve redacted request/response evidence.

A scanner alert is a lead. Confirm the affected endpoint, prerequisites, control failure, repeatability, and realistic impact without accessing unnecessary data. For authorization issues, use only test objects and roles assigned for the engagement. Do not escalate exploitation after the minimum proof is established.

## Report and stop

For each confirmed finding, provide severity and confidence, affected surface, prerequisites, minimal reproduction, redacted evidence, impact, remediation, and a regression-test idea. Separate confirmed vulnerabilities, unverified leads, and hardening advice. Include tested scope, identities and roles, exclusions, tool versions, rate limits, and coverage gaps.

Use versioned OWASP identifiers when cited. Do not claim comprehensive coverage or safety from a clean scan.
