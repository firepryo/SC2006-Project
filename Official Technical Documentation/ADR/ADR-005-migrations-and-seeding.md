# ADR-005: Schema migrations and seed data
Status: Accepted
Date: 2026-10-23
Context: The Lab 2 tech stack report chose Flask-Migrate (Alembic) for versioned migrations. Subjects, CCAs and affiliations are not in the school dataset.
Options:
- Alembic, with the source for subjects, CCAs and affiliations decided later in INT-01.
- Alembic, with hand-maintained CSV seed files decided now.
Decision: Alembic for every schema change; DATA-01 v0.2's DDL is the first migration. Fixed lookup rows (comparison criteria, the dataset-derived programme and language subjects) are seeded inside migrations. The source of the remaining subjects, CCAs and affiliations is decided in INT-01. Chosen by the user.
Consequences: OPS-01 documents the migration commands. INT-01 must cover subject, CCA and affiliation data. Until then those tables hold only the seeded rows.
