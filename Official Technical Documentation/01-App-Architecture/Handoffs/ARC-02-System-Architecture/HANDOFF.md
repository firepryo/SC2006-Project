# HANDOFF: ARC-02 System Architecture

| Field | Value |
| --- | --- |
| Document | `Official Technical Documentation/01-App-Architecture/ARC-02-System-Architecture.md` |
| Document version used | 0.1 (Draft, 2026-10-25), built from the Draft at the user's request for Lab 3 |
| Phase | Awaiting skeleton approval |
| Code location | `app/run.py`, `app/app.py` (`create_app()`, settings included), `app/requirements.txt`, `app/__init__.py`, `app/extensions.py`, `app/errors.py`, `app/control/`, `app/boundary/`, `app/gateway/`, `app/jobs/`, `app/frontend/`, `app/SKELETON.md` (ARC-02 section) |
| Progress | 0 / 9 features (F3–F11), 1 function blocked |
| Current feature | none |
| Last updated | 2026-10-25 |

## Status summary
Every layer in ARC-02 §3.12 exists as a skeleton: 13 controllers, 4 comparison strategies, 2 gateways, 7 blueprints with all 30 §4.1 routes, request schemas, jobs and CLI, and a React SPA with one page per boundary UI class plus a typed client for every endpoint. All bodies are stubs, so the app does not start yet (`create_app()` raises).

## Features
| ID | Feature | Source in document | Status |
| --- | --- | --- | --- |
| F3 | Wiring and cross-cutting | §3.3, §3.9, §5 | Not started |
| F4 | M1 Accounts | §3.4, §3.7.2, UC01, UC02, UC07a, UC14 | Not started |
| F5 | M2 Student profiles | §3.4, UC03 | Not started |
| F6 | M8 School data sync | §3.7.5, UC12 | Not started |
| F7 | M3 School discovery | §3.4, UC04–UC06 | Not started |
| F8 | M4 Comparison | §3.7.3, §3.10, UC07 | Not started |
| F9 | M5 Shortlist | §3.4, UC08 | Not started |
| F10 | M6 Applications | §3.10, UC09, UC10, UC13 | Not started |
| F11 | M7 Notifications | §3.7.4, UC11 | Not started (mark_as_read blocked) |

## Done
- 2026-10-25: Skeleton for all of ARC-02 §3.12 (back end and front end); SKELETON.md ARC-02 section.
- 2026-10-26: Layout change requested by the user: `App/` and `App/app/` merged into one package `app/` at the repository root; `create_app()` in `app/app.py` (replaces `app()`), with the settings inside it (no `Config` class or `config.py`; JWT settings + `python-dotenv`); Flask-Login replaced by Flask-JWT-Extended (ARC-02 §3.9.2). Run from the repository root: `python -m app.run`, `flask --app "app.app:create_app()" ...`.

## Next steps
1. User confirms the skeleton.
2. DATA-01 F1 + ARC-02 F3: implement `create_app()` and the wiring functions, then DATA-01 F2 (first migration).

## Blocked and open questions
| Item | Document section | Question / reason | Raised | Answer |
| --- | --- | --- | --- | --- |
| `ReminderController.mark_as_read` | §7 Q1 | `deadline_reminder` has no read flag | 2026-10-25 | |
| Email reminders | §7 Q2 | In-app only, or SES too? | 2026-10-25 | |
| Distance | §7 Q3, Q4 | Straight-line PostGIS (stubbed) or OneMap travel distance? | 2026-10-25 | |
| Subject / affiliation datasets | §3.7.5 | Dataset ids not chosen (INT-01 not written) | 2026-10-25 | |

## Deviations from the document
- `HomeUI` page added for dialog-map state DM-10; it is not a class-diagram boundary class.
- Request field rules (lengths, formats) are not in ARC-02; `boundary/schemas.py` has field names and required flags only, pending API- documents.

## How to check it
- `py -m compileall App`: OK (2026-10-25).
- Import test in a venv with `requirements.txt` (minus psycopg): all modules import; 7 blueprints, 30 routes; `ALLOWED_TRANSITIONS` covers all 6 statuses (2026-10-25).
- Front end: `cd App/frontend && npm install && npx tsc -b`. Not run: Node.js is not installed here.

## Notes for the architect
- Q1 needs DATA-01 v1.1 before F11 can finish.
- API- documents should fix request validation rules and response bodies for each route group.
