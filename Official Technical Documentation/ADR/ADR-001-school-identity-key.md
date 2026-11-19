# ADR-001: School identity key for the data.gov.sg sync
Status: Accepted
Date: 2026-10-23
Context: The Lab 2 schema has `school.moe_code` (UNIQUE) and uses `school.name` as the sync upsert key. The data.gov.sg school dataset (`d_688b934f82c1059ed0a6993d2a829089`, 337 records) has no MOE school code. All 337 school names are unique; two pairs of schools share a postal code. Related: UC12, FR 12.x.
Options:
- Upsert on `name`, drop `moe_code`: matches the data; no unused column. A renamed school appears as a new row and the old row is retired.
- Upsert on `name`, keep `moe_code` nullable: room for a future source with codes, but a column nothing fills.
- Upsert on `postal_code`: not unique in the dataset, so it would need a composite key.
Decision: Upsert on `school.name`; remove `moe_code`. Chosen by the user.
Consequences: DATA-01 v0.2 drops `moe_code`. The sync (BE-02, INT-01) matches on the exact dataset name and retires schools missing from a full sync (`is_active = false`). A rename needs no special handling but loses shortlist/application links to the old row's successor.
