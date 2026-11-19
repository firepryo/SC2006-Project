# HANDOFF: DATA-01 Data Schema

| Field | Value |
| --- | --- |
| Document | `Official Technical Documentation/02-Data-Schema/DATA-01-Data-Schema.md` |
| Document version used | 1.0 (2026-10-23) |
| Phase | Implementing |
| Code location | `app/app.py` (`create_app()`, settings included), `app/extensions.py`, `app/requirements.txt`, `app/.env.example` (local `app/.env` is git-ignored), `app/models/` (`__init__.py`, `enums.py`, `account.py`, `school.py`, `application.py`), `app/SKELETON.md` |
| Progress | 1 / 2 features (1 / 7 items), 1 blocked |
| Current feature | F2 (blocked: no PostgreSQL + PostGIS) |
| Last updated | 2026-10-23 |

## Start here

**Where it stands (end of 2026-10-23):** models done and checked against §3.2–3.6; F1 (app wiring) done; F2 (first migration) blocked on a local database. Auth/session settings exist ahead of their documents (see "Work outside DATA-01"). **Nothing is committed** (branch `Srujan_test`).

**Next steps, in order:**

| # | Step | Who | Unblocks |
| --- | --- | --- | --- |
| 1 | Commit today's work on `Srujan_test` | user | safe restart point |
| 2 | Choose the local database: PostgreSQL + PostGIS on Windows, or Docker `postgis/postgis` (OPS-01, checklist 2.3) | user | F2 |
| 3 | Put the real `DATABASE_URL` in `App/app/.env` | user | F2 |
| 4 | F2: from `App/`, `flask --app "app.app:app()" db init`; set up `migrations/env.py` for GeoAlchemy2; first revision with `CREATE EXTENSION citext/postgis`, 5 enums, 16 tables, indexes, seed rows (4 criteria, 21 subjects); `downgrade()` drops it all | engineer | database |
| 5 | Apply with `db upgrade`; compare `pg_dump --schema-only` with §3.6; test delete rules with sample rows (account → students cascade; school in an application is blocked) | engineer | DATA-01 Complete |
| 6 | Answer the open questions below (GeoAlchemy2, index names, app layout) | user / architect | DATA-01 Complete |
| 7 | Login, once BE-01 / SEC-01 exist: user loader + `UserAccount.get_id()`, JSON 401 `unauthorized_handler`, password hashing, login/logout endpoints with `session.permanent = True`, lockout (NFR 3.5.1), CSRF | architect, then engineer | checklist 3.1 |

**Setup for a fresh machine:** from `App/`, `pip install -r app/requirements.txt`; copy `app/.env.example` to `app/.env` and fill in `DATABASE_URL` and `SECRET_KEY` (`python -c "import secrets; print(secrets.token_hex(32))"`). On this Windows machine SQLAlchemy needs `DISABLE_SQLALCHEMY_CEXT=1 pip install --no-binary sqlalchemy sqlalchemy` (SKELETON.md, open question 4).

## Status summary
All 16 tables and 5 enums are declared as Flask-SQLAlchemy models. An offline check found no differences from §3.2–3.6 apart from index names. `app()` in `App/app/app.py` builds the Flask app: it loads `app.config.Config`, requires `DATABASE_URL` and `SECRET_KEY`, sets the session-cookie security flags, attaches `db`, `migrate` and `login_manager`, and registers the models. There are no blueprints, no `create_app()` and no `App/app/__init__.py` (`app` is a namespace package). Nothing has been applied to a database.

## Features
| ID | Feature | Source in document | Status |
| --- | --- | --- | --- |
| F1 | App wiring (`app()` in `app/app.py`) | §3.7 | Done |
| F2 | First migration and seed rows | §3.6, §3.7, ADR-005 | Blocked (needs PostgreSQL + PostGIS, OPS-01) |

## Done
- 2026-10-23: Skeleton: enums, all 16 models, extensions, config, requirements, SKELETON.md.
- 2026-10-23: F1: `app()` in `App/app/app.py` (user asked for the settings there, no blueprints, no `create_app()`). Raises `RuntimeError` if `DATABASE_URL` or `SECRET_KEY` is unset.
- 2026-10-23: Layout changes requested by the user: `App/app/__init__.py` removed; `config.py` and `requirements.txt` moved into `App/app/`; config path is `app.config.Config`.
- 2026-10-23: Secrets moved to `App/app/.env`, loaded by `python-dotenv` in `config.py` (variables already set in the environment win). `.env.example` is the committed template.
- 2026-10-23: Schema check against §3.2–3.6 (16 tables, 87 columns, 17 FKs with delete rules, 9 uniques, 6 checks, 10 indexes, 5 enums): no differences.
- 2026-10-23: Comment on `student_profile.user_id` (`account.py`) reworded to describe the cascade correctly.
- 2026-10-23: Session-cookie settings and `login_manager` added (see "Work outside DATA-01").
- 2026-10-26: Layout change requested by the user: `App/` and `App/app/` merged into one package `app/` at the repository root; `create_app()` in `app/app.py` (replaces `app()`), with the settings inside it (no `Config` class or `config.py`; JWT settings + `python-dotenv`); Flask-Login replaced by Flask-JWT-Extended (ARC-02 §3.9.2). Run from the repository root: `python -m app.run`, `flask --app "app.app:create_app()" ...`.

## Blocked and open questions
| Item | Document section | Question / reason | Raised | Answer |
| --- | --- | --- | --- | --- |
| Local PostGIS | §1, §3.7 | F2 needs PostgreSQL + PostGIS; none on this machine and OPS-01 not written. Installed locally or Docker? | 2026-10-23 | |
| GeoAlchemy2 | §3.3 | Library for `geography` not named in DATA-01; GeoAlchemy2 used. | 2026-10-23 | |
| App layout | n/a | ARC-02 not written; minimal layout used: `app()` in `App/app/app.py`, no blueprints (user's instruction). | 2026-10-23 | |
| Index names | §3.6 | SQLAlchemy names the indexes (e.g. `ix_school_zone`); §3.6 leaves them unnamed. OK? | 2026-10-23 | |

## Deviations from the document
- Index names are set by SQLAlchemy (e.g. `ix_school_zone`, `idx_school_location`); §3.6 leaves them unnamed. Not yet approved by the user.
- `app/app.py` and `app/extensions.py` are not in DATA-01; they are the minimum needed to host the models in Flask, as the user asked.

## Work outside DATA-01 (no document yet)
Done at the user's request, ahead of the documents that should define it. It belongs to BE-01 (checklist 3.1) and SEC-01 (5.1); move it to their HANDOFFs when they exist.
- Auth strategy chosen by the user (2026-10-23): HttpOnly session cookie ("Option A").
- Settings in `app()`:

  | Setting | Value |
  | --- | --- |
  | `SESSION_COOKIE_HTTPONLY` | `True` |
  | `SESSION_COOKIE_SECURE` | env `SESSION_COOKIE_SECURE`, default `true` |
  | `SESSION_COOKIE_SAMESITE` | `"Lax"` |
  | `PERMANENT_SESSION_LIFETIME` | 30 minutes (`SESSION_IDLE_TIMEOUT`, placeholder for SEC-01) |
  | `SESSION_REFRESH_EACH_REQUEST` | `True` |
  | `REMEMBER_COOKIE_HTTPONLY` / `_SECURE` / `_SAMESITE` | same as the session cookie |

- `SECRET_KEY` read from `.env`; `app()` refuses to start without it.
- `login_manager` (Flask-Login, `session_protection="strong"`) created in `extensions.py` and attached in `app()` after `migrate.init_app`. Flask-Login and python-dotenv added to requirements.
- Not built: see next step 7.

## How to check it
- `python -m compileall App`: OK (2026-10-23).
- F1: with `.env` present, `from app.app import app; app()` (from `App/`) returns a Flask app with `sqlalchemy` and `migrate` extensions, `login_manager` attached, and 16 tables on `db.metadata`; without `DATABASE_URL` or `SECRET_KEY` it raises `RuntimeError`. `flask --app "app.app:app()" db --help` runs. (2026-10-23, no live database.)
- Schema: compare `db.metadata` with §3.2–3.6 table by table (columns, types, NOT NULL, defaults, PKs, FKs and delete rules, uniques, checks, indexes, enums). Last result (2026-10-23): no differences apart from index names.
- Session cookie: a test request that sets a permanent session returns `Set-Cookie: session=...; Expires=<+30 min>; Secure; HttpOnly; Path=/; SameSite=Lax` (2026-10-23).

## Notes for the architect
- §3.6 should name its indexes, so Alembic and the DDL agree.
- OPS-01 is needed before F2 can be applied.
- Auth and session code exists ahead of BE-01 and SEC-01 (see "Work outside DATA-01"); those documents should confirm or change it, including the 30-minute idle timeout.
- ARC-02 should decide routes vs blueprints and whether frontend and API share an origin (affects CORS and CSRF).
- CHECKLIST.md change log does not yet mention F1, the `.env` setup or the session/login settings.
