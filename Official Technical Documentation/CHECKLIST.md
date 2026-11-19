# Design and Build Checklist

Workflow maintained by the `solution-architect` skill. Work top to bottom; a step is ticked only when the user confirms it is done. Build steps are done with the `software-engineer` skill.

**Current step:** 1.1

## Phase 1: Requirements baseline

| Done | Step | Output | Confirmed |
| --- | --- | --- | --- |
| [ ] | 1.1 Resolve conflicts in the Lab 1 / Lab 2 material (scope, shortlist cardinality, application statuses, open schema questions) | ADRs | |
| [ ] | 1.2 Prioritise use cases and confirm the feature build order | ARC-01 §Priorities | |
| [ ] | 1.3 Write and approve the Requirements Baseline (scope, use cases, FR/NFR targets) | ARC-01 Requirements Baseline | |

## Phase 2: Foundations

| Done | Step | Output | Confirmed |
| --- | --- | --- | --- |
| [ ] | 2.1 System architecture: layers, modules, tech stack, request flow | ARC-02 System Architecture | |
| [x] | 2.2 Data schema, finalised from `lab 2/Data Schema/` | DATA-01 Data Schema | 2026-10-23 |
| [ ] | 2.3 Local development environment (Docker, run and test commands) | OPS-01 Local Development Environment | |

## Phase 3: Thin end-to-end slice (accounts and student profiles, UC01–UC03)

| Done | Step | Output | Confirmed |
| --- | --- | --- | --- |
| [ ] | 3.1 Backend: accounts, login lockout, sessions, student profiles | BE-01 Accounts and Profiles | |
| [ ] | 3.2 API: auth and profile endpoints | API-01 Auth and Profiles | |
| [ ] | 3.3 UI: login/register and student profile screens | UI-01 Login and Register, UI-02 Student Profiles | |
| [ ] | 3.4 Engineer builds the slice (`software-engineer`, one document at a time) | Code + HANDOFF.md per document | |
| [ ] | 3.5 Review the slice HANDOFFs and update documents | New document versions | |

## Phase 4: Features in dependency order

For each feature: design the documents → engineer builds → review HANDOFFs.

| Done | Step | Output | Confirmed |
| --- | --- | --- | --- |
| [ ] | 4.1 School data sync (UC12): design | INT-01 School Data Source, BE-02 School Data Sync | |
| [ ] | 4.2 School data sync: build and review | Code, HANDOFFs | |
| [ ] | 4.3 Search and filter (UC04–UC05): design | BE-03 School Search, API-02 Schools, UI-03 School Search | |
| [ ] | 4.4 Search and filter: build and review | Code, HANDOFFs | |
| [ ] | 4.5 School details (UC06): design | API-02 update, UI-04 School Details | |
| [ ] | 4.6 School details: build and review | Code, HANDOFFs | |
| [ ] | 4.7 Compare schools (UC07, 07a–07d): design | BE-04 Comparison, API-03 Compare, UI-05 Comparison, INT-02 Maps/Routing (if used) | |
| [ ] | 4.8 Compare schools: build and review | Code, HANDOFFs | |
| [ ] | 4.9 Shortlist (UC08): design | BE-05 Shortlist, API-04 Shortlist, UI-06 Shortlist | |
| [ ] | 4.10 Shortlist: build and review | Code, HANDOFFs | |
| [ ] | 4.11 Applications and status (UC09, UC10, UC13): design | BE-06 Applications, API-05 Applications, UI-07 Applications | |
| [ ] | 4.12 Applications and status: build and review | Code, HANDOFFs | |
| [ ] | 4.13 Deadline reminders (UC11): design | BE-07 Reminders, INT-03 Email | |
| [ ] | 4.14 Deadline reminders: build and review | Code, HANDOFFs | |

## Phase 5: Cross-cutting

| Done | Step | Output | Confirmed |
| --- | --- | --- | --- |
| [ ] | 5.1 Security and NFR compliance: how each NFR is met and tested | SEC-01 Security and NFR Compliance | |
| [ ] | 5.2 Cloud deployment, CI/CD, backups, monitoring | OPS-02 Cloud Deployment | |
| [ ] | 5.3 Build and verify (NFR tests, deployment) | Code, HANDOFFs | |

## Phase 6: Final review

| Done | Step | Output | Confirmed |
| --- | --- | --- | --- |
| [ ] | 6.1 Traceability check: every FR/NFR/UC → document → code | Traceability table in master README | |
| [ ] | 6.2 All documents Approved and consistent | Updated README indexes | |
| [ ] | 6.3 Approved documents exported to PDF | `PDF/<area>/` | |

## Change log

- 2026-10-23: Checklist created.
- 2026-10-23: Step 2.2 started out of order at the user's request: DATA-01 v0.1 (Draft) carries over the Lab 2 schema unchanged; Phase 1 still open.
- 2026-10-23: DATA-01 v0.2 (Draft) aligned with the data.gov.sg school dataset; ADR-001 to ADR-005 recorded. Step 2.2 not yet confirmed.
- 2026-10-23: DATA-01 v1.0 Approved by the user (ADR-006 added); step 2.2 ticked out of order. Engineer started DATA-01 models (Flask-SQLAlchemy) in `App/` at the user's request, ahead of ARC-02 and OPS-01.
- 2026-10-25: Step 2.1 started out of order at the user's request (Lab 3 deliverable): ARC-02 v0.1 (Draft) written and exported to `Lab 3/System Architecture/System_Architecture.pdf`. Engineer built the ARC-02 skeleton from the Draft at the user's request. Step 2.1 not yet confirmed.
