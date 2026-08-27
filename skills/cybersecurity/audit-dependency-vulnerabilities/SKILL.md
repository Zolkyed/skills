---
name: audit-dependency-vulnerabilities
description: Find and triage known vulnerabilities in authorized project dependencies, lockfiles, vendored packages, and container manifests. Use for software-composition analysis and upgrade planning; do not use for source-code defects or license-only reviews.
---

# Audit Dependency Vulnerabilities

Turn scanner matches into an evidence-based remediation plan. A vulnerable version match does not by itself prove exploitability, and absence of matches does not prove safety.

## Build the inventory

Find every relevant manifest, lockfile, workspace, vendored dependency, generated SBOM, container base image, and build stage. Prefer resolved lockfile or image data over loose version ranges. Record ecosystem, resolved version, dependency path, runtime or development scope, and artifact actually shipped.

Use the project's native audit command and an OSV-compatible scanner when available. Preserve tool versions and database timestamps. Do not install new scanners or upload private manifests to third-party services without authorization.

## Triage matches

For each advisory, confirm:

- package identity, ecosystem, affected range, and resolved version;
- whether the vulnerable component reaches a shipped or deployed artifact;
- direct versus transitive path and feature or platform conditions;
- vulnerable function or behavior reachability where evidence permits;
- fixed versions, backports, workarounds, and upstream status.

Use authoritative advisory sources and vendor or maintainer notices. Treat severity scores as inputs; prioritize actual exposure, exploit preconditions, asset impact, and known exploitation. Do not dismiss a development dependency automatically when it executes during builds or handles untrusted input.

## Remediate safely

Prefer the smallest supported upgrade that removes the affected range, then run focused and full verification appropriate to the change. Avoid unexplained resolution overrides. If no fix exists, document compensating controls, affected environments, an owner, and a review date.

Never claim a vulnerability is fixed solely because a scanner is green: confirm the resolved dependency graph or produced artifact no longer contains the affected version.

## Report

Provide the scanned artifacts, commands and database date, confirmed findings, dismissed matches with reasons, remediation choices, verification evidence, and residual risks. Link advisories directly and keep uncertain reachability labeled as uncertain.
