# ADR-004: Which dataset fields to store, and how
Status: Accepted
Date: 2026-10-23
Context: The dataset has 31 fields; the Lab 2 `school` table holds only a few. FR 5.1 filters by location, subjects/programmes, CCAs and affiliations; UC06 shows school details. The dataset also contains principal and vice-principal names (personal data, PDPA).
Options: store per group (location/classification, programme flags, contact and transport, mother tongue languages, staff names), as columns or as subject rows.
Decision (chosen by the user):
- Store zone, planning area, funding type, gender type and session as `school` columns.
- Store the SAP, autonomous, gifted (GEP) and IP flags as `subject` rows with `is_special_programme = true`, linked through `school_subject`, so they filter like other programmes.
- Store the mother tongue languages offered as `subject` rows (Chinese, Malay, Tamil Language).
- Store the main telephone, email, MRT and bus descriptions as `school` columns; drop the second phone and both fax numbers.
- Do not store principal or vice-principal names.
Consequences: DATA-01 v0.2 adds the columns and the seeded subject rows; the sync owns only the links to those seeded subjects. No personal staff data is held, which keeps SEC-01's PDPA scope to user accounts.
