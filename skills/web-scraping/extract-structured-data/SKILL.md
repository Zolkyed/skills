---
name: extract-structured-data
description: Convert web content into records that conform to an explicit schema with normalized types, validation, deduplication, and source provenance. Use when scraping output must be machine-consumable or auditable; use crawling skills to discover or fetch large URL sets.
---

# Extract Structured Data

Treat extraction as a typed transformation from source evidence to validated records.

## Start with the schema

Define each field's name, type, meaning, required status, nullability, units, format, and source. Include a stable record identity and provenance fields when the consumer needs auditability. Distinguish:

- missing from the page;
- present but empty;
- not applicable;
- extraction failure.

Do not invent values to satisfy required fields. Use an explicit null or error representation agreed by the output contract.

## Extract from stable evidence

Prefer embedded structured data, semantic markup, labeled values, and stable attributes over layout position or generated classes. Keep raw capture or a minimal fixture when permitted so parsing can be reproduced without another request.

Separate extraction from normalization. Preserve the source text before converting dates, prices, measurements, identifiers, enums, and locale-specific numbers. Never infer currency, timezone, or units without page evidence or an explicit task-level default.

## Validate every record

Validate types and required fields before emission. Reject or quarantine invalid records with the source URL, field errors, and raw values needed to investigate. Deduplicate using the declared identity rather than whole-record equality, and define how conflicting observations are resolved.

Test representative fixtures for complete records, missing optional fields, malformed values, duplicates, layout variants, and empty result pages. Selectors should fail visibly when the page shape changes; a plausible partial record is more dangerous than an explicit extraction error.

## Deliverable

Provide the schema, example output, normalization rules, validation summary, rejected-record count, and source provenance. Report coverage and null rates per important field so consumers can judge data quality.
