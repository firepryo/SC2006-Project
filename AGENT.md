# AGENT.md

Guide for AI agents working in this repository (SC2006 School Comparison & Shortlisting App). It says which skill to use for which kind of work. Read it at the start of every session.

## The two skills

| Skill | Role | Use it when | Writes to |
| --- | --- | --- | --- |
| `solution-architect` | Designs the system and writes the technical documentation, together with the user, following `Official Technical Documentation/CHECKLIST.md` step by step | Designing, or writing, reviewing or revising technical documentation | `Official Technical Documentation/` (area sub-folders, `ADR/`) |
| `software-engineer` | Turns one approved technical document into code: skeleton first, then feature by feature | Code writing starts | Source code, `SKELETON.md`, and the document's `Handoffs/<document>/HANDOFF.md` |

Skill definitions: `skills/solution-architect/SKILL.md` and `skills/software-engineer/SKILL.md`.

## Use `solution-architect` when

- designing architecture, modules, data schema, backend logic, API contracts, screens, integrations, security or deployment
- creating, extending, reviewing or revising any document in `Official Technical Documentation/`
- a design decision has to be made or recorded (ADR)
- the Lab 1 / Lab 2 material is unclear, conflicting or missing something the design needs
- an engineer's `HANDOFF.md` raises blocked items or "Notes for the architect"

## Use `software-engineer` when

- code writing starts: the user asks to build, scaffold or implement something
- generating the skeleton for a technical document
- implementing features from an approved skeleton
- resuming implementation (start from that document's `HANDOFF.md`)

## Rules for choosing

1. **No code before an approved document.** If the user asks for code and no document covers it, or the covering document is not Approved, say so and switch to `solution-architect` first. Build from a Draft only if the user explicitly says to.
2. **One skill per task.** Do not design while coding or code while designing. If a design gap appears during coding, the engineer records it in HANDOFF.md, blocks that part, and the user takes it to the architect.
3. **One document per engineering task.** The engineer builds from exactly one document at a time; name it (e.g. `04-API/API-02-Schools.md`) or the engineer will ask.
4. **Pure questions need no skill.** Explaining existing code or documents, or answering a quick question, does not need either skill.
5. **Unsure which applies?** Ask the user in one line: "design the documentation, or start writing code?"

## Handover between the skills

```
Lab 1 / Lab 2 material
        |  solution-architect
        v
Official Technical Documentation/<area>/<ID>-<Title>.md   (Draft -> In review -> Approved by user)
        |  software-engineer, one document at a time
        v
Skeleton -> user confirms -> features implemented one by one
        |  questions and gaps
        v
<area>/Handoffs/<ID>-<Title>/HANDOFF.md  -> read by solution-architect for the next document version
```

- Only the user approves documents and skeletons.
- When an approved document gets a new version, the engineer re-checks that document's HANDOFF.md before continuing.

## Sources of truth

- **Requirements:** `lab1/` and `lab 2/`. Read-only; never edit them.
- **Design:** `Official Technical Documentation/`. Code follows these documents, not the lab files directly.
- **Implementation status:** each document's `HANDOFF.md`.
- **Personal task checklist:** `PERSON_*_CHECKLIST.md` in the repo root, if present. It is git-ignored and personal to whoever works on this machine. Read it at the start of a session; whichever skill finishes a task on it ticks that item in the same turn (see `software-engineer` ground rule 8). Never commit it.
- **Local session context:** `project.json` in the repo root, if present. It is git-ignored and personal; read it for context and keep it updated, but do not rely on teammates having it.
- **Repo rule:** the README limits uploads to .pdf and .jpeg; approved documents are exported to `Official Technical Documentation/PDF/<area>/`.
