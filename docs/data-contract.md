# Synthetic data contract

The public example uses only invented businesses and `.test` URLs. The private output
has the same field roles but is not included.

| Field | Purpose |
|---|---|
| `business_name` | normalized display name |
| `source` | adapter that discovered the record |
| `source_url` | source identity used for audit and deduplication |
| `city_area` | public location evidence, or an unresolved state |
| `email`, `phone`, `website`, `facebook` | public contact paths with provenance |
| `services_found` | supported service evidence from the source |
| `booking_method` | visible appointment path |
| `lead_score` | review-order score after evidence reconciliation |
| `priority` | human-readable review bucket |
| `reason_for_score` | short evidence tokens explaining the score |
| `recommended_offer_angle` | grounded automation use case |
| `review_state` | ready, unresolved, or manual-review boundary |

`Not found` means the checked source did not provide a value. `Needs manual review`
means the system could not determine a trustworthy result. Those states must never be
collapsed into an invented contact or a definite negative claim.
