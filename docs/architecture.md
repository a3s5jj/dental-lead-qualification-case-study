# Pipeline architecture

## 1. Source adapters

Directory, map, and advertising sources expose different identifiers and failure
modes. Each adapter owns navigation, extraction, checkpointing, and raw-source audit
fields. It emits one normalized record contract to the shared pipeline.

## 2. Qualification

Qualification asks whether the business is appointment-based, whether a booked visit
can plausibly create revenue, whether a public contact path exists, and whether the
visible booking process shows an automation opportunity. Missing evidence stays
missing; category alone does not create a high-priority record.

## 3. Identity and deduplication

Stable source profile URLs are preferred. Normalized business names, locations,
phones, websites, and social handles provide progressively weaker supporting signals.
Within-source duplicates are removed early. Cross-source duplicates are reconciled
after enrichment so the richer record can be retained.

## 4. Link checks

Identity matching and link liveness are separate stages. A liveness checker answers
only whether the supplied page appears live, dead, or uncertain. It must not silently
replace a URL or decide that a similarly named page belongs to the business.

## 5. Enrichment

Public pages can fill unresolved email, phone, website, owner, activity, or advertising
signals. Enrichment is backfill-only. It cannot overwrite a stronger existing value,
and unresolved access becomes a review state.

## 6. Scoring and quality gate

Evidence transitions reconcile the old and new score contribution, which makes reruns
idempotent. Final delivery requires agreement between machine-readable rows, workbook
rows, audit rows, source summaries, and cross-source reconciliation status.

## Operating boundary

The private implementation also has resume state, browser controls, source limits,
and paid-run approvals. Those operational details and tools are intentionally outside
this public case study.
