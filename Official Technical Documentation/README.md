# Official Technical Documentation

Detailed technical documentation for the School Comparison & Shortlisting App (SC2006). Built from the Lab 1 and Lab 2 material, maintained by the `solution-architect` skill together with the team. Each document is self-contained so it can be handed to the `software-engineer` skill on its own.

## Areas

| Area | ID prefix | Covers | Documents |
| --- | --- | --- | --- |
| [01-App-Architecture](01-App-Architecture/) | `ARC-` | Requirements baseline, system context, architecture style, layers, modules, component diagram, tech stack. | 1 |
| [02-Data-Schema](02-Data-Schema/) | `DATA-` | ER model, tables, enums, indexes, delete rules, DDL, migrations. Starts from the draft in `lab 2/Data Schema/`. | 1 |
| [03-Backend](03-Backend/) | `BE-` | One document per backend module: control classes, services, business rules, state machines, background jobs. | 0 |
| [04-API](04-API/) | `API-` | One document per resource group of endpoints: paths, auth, request/response JSON, status codes, errors. | 0 |
| [05-UI-Screens](05-UI-Screens/) | `UI-` | One document per screen or closely linked screen group: route, layout, UI states, actions, validation, API calls. | 0 |
| [06-Integrations](06-Integrations/) | `INT-` | One document per external system (school data, maps/routing, email): endpoint, auth, limits, schedule, mapping, failures. | 0 |
| [07-Security](07-Security/) | `SEC-` | Authentication, sessions, lockout, password hashing, PDPA, and how each NFR is met and tested. | 0 |
| [08-Deployment](08-Deployment/) | `OPS-` | Environments, containers, cloud layout, CI/CD, backups, monitoring, config and secrets. | 0 |

Work follows the step-by-step workflow in [`CHECKLIST.md`](CHECKLIST.md): requirements baseline → foundations (architecture, data schema, dev environment) → a thin end-to-end slice → features one at a time (design, build, review) → security and deployment → final review. Each step is ticked only when the user confirms it.

## All documents

| ID | Document | Area | Version | Status | Last updated |
| --- | --- | --- | --- | --- | --- |
| ARC-02 | [System Architecture](01-App-Architecture/ARC-02-System-Architecture.md) | 01-App-Architecture | 0.1 | Draft | 2026-10-25 |
| DATA-01 | [Data Schema](02-Data-Schema/DATA-01-Data-Schema.md) | 02-Data-Schema | 1.0 | Approved | 2026-10-23 |
| API-01 | [API Endpoints](04-API/API-01-API-Endpoints.pdf) | 04-API | 0.1 | Draft | 2026-10-26 |

## Decisions

Architecture Decision Records live in [`ADR/`](ADR/).

| ADR | Title | Status | Date |
| --- | --- | --- | --- |
| [ADR-001](ADR/ADR-001-school-identity-key.md) | School identity key for the data.gov.sg sync | Accepted | 2026-10-23 |
| [ADR-002](ADR/ADR-002-school-type-mapping.md) | Mapping the dataset's main level to school type | Accepted | 2026-10-23 |
| [ADR-003](ADR/ADR-003-school-geocoding.md) | Filling school coordinates by geocoding | Accepted | 2026-10-23 |
| [ADR-004](ADR/ADR-004-school-dataset-fields.md) | Which dataset fields to store, and how | Accepted | 2026-10-23 |
| [ADR-005](ADR/ADR-005-migrations-and-seeding.md) | Schema migrations and seed data | Accepted | 2026-10-23 |
| [ADR-006](ADR/ADR-006-cca-category-others.md) | CCA category "Others" | Accepted | 2026-10-23 |

## Implementation handoffs

Each area folder has a `Handoffs/` folder. When the `software-engineer` skill builds a document, it keeps that document's `HANDOFF.md` there, e.g. `04-API/Handoffs/API-02-Schools/HANDOFF.md`: phase, features and progress, next steps, blocked items and questions for the architect.

## Status meanings

- **Draft**: being written with the user.
- **In review**: complete and self-checked; waiting for the team.
- **Approved**: signed off by the user; ready for implementation. Changes need a version bump and a change-log line.

Approved documents are exported to [`PDF/`](PDF/), in the same area sub-folders.
