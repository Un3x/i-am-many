# Setup — Instantiating IAM for a new project

This document is the bootstrap layer for IAM. Run it once, per project, **before** the CEO does any operational work. Its job is to turn the `templates/` directory into a working instance:

- Linear project created and reachable
- Strategic memory files (`vision.md`, `state.md`) seeded with real content
- Project-root `CLAUDE.md` derived from the CEO template
- All template slots substituted with real values

Once this is done, the day-1 CEO can pass the Setup-complete check at the top of its Session-start routine and proceed to the bootstrap routine (measurability audit).

## Prerequisites

Before starting, the user must have:

- A Linear workspace they can administer (to create a new project and obtain its UUID)
- A git repository for the IAM-managed project (this need not be the IAM framework repo itself)
- The IAM `templates/` directory available at the repo root
- A Claude Code session with the `Agent` tool and the `linear-*` MCP server configured

## Slot inventory

Every placeholder that must be substituted, and where each appears:

| Slot | Form | Appears in |
| --- | --- | --- |
| Project name | `[PROJECT]` | `templates/CEO.CLAUDE.md` (title, Role paragraph), `templates/vision.md` (title), `templates/state.md` (title) |
| Linear project UUID | `[LINEAR_PROJECT_ID]` | `templates/CEO.CLAUDE.md` (Role bullet, Session-start step "Query Linear") |
| Date | `YYYY-MM-DD` | `templates/state.md` (Updated header) |

In addition, two sentinel markers must be removed once their files are filled:

| Sentinel | File | Removed at |
| --- | --- | --- |
| `<!-- IAM:UNFILLED -->` | `templates/vision.md` (top) | Step 3 |
| `<!-- IAM:UNFILLED -->` | `templates/state.md` (top) | Step 3 |

The CEO's Session-start Setup-complete check greps for `IAM:UNFILLED` in `vision.md` and `state.md`; presence on either file means instantiation is incomplete.

## Step 1 — Create the Linear project

1. In Linear, create a new project for this IAM instance. Recommended name: the same string used for `[PROJECT]`.
2. Capture the project's UUID. This is the value used for `[LINEAR_PROJECT_ID]` throughout the template substitutions. The CEO will use it on every session to query in-flight and recently-closed work.
3. Confirm the project is reachable through the configured Linear MCP server (e.g., `list_projects` returns it).

Output of this step: the literal string for `[LINEAR_PROJECT_ID]`.

## Step 2 — Fill template slots

Substitute the slots from the inventory across the three template files:

- `templates/CEO.CLAUDE.md` — replace every `[PROJECT]` with the project name; replace every `[LINEAR_PROJECT_ID]` with the UUID from Step 1.
- `templates/vision.md` — replace `[PROJECT]` with the project name.
- `templates/state.md` — replace `[PROJECT]` with the project name; replace `YYYY-MM-DD` with today's date.

Do this **in the template files themselves** only if you are forking IAM for a single project. If you are using IAM as a reusable framework, do the substitution as part of Step 4's derivation instead, and leave the templates untouched.

## Step 3 — Initialize strategic memory

Both `vision.md` and `state.md` ship with placeholder scaffolding and an `<!-- IAM:UNFILLED -->` sentinel at the top.

1. Open `vision.md`. With the user, fill in:
   - **North star** — qualitative anchor; 1–2 paragraphs.
   - **Current focuses** — 3–5 priorities, in priority order.
   - **Out of scope** — explicit non-goals.
2. Open `state.md`. With the user, fill in:
   - **Economic state** — budget, compute, attention, acceptable cost per task.
   - **Notes for the CEO** — current context the CEO should hold.
3. **Remove the `<!-- IAM:UNFILLED -->` line** from the top of each file. The CEO's Setup-complete check uses this string as the binary detector.

These files are user-owned thereafter. The CEO may propose changes; the user decides.

## Step 4 — Derive instance CLAUDE.md

1. Copy `templates/CEO.CLAUDE.md` to the project root as `CLAUDE.md`.
2. If Step 2 left the templates unsubstituted, apply the `[PROJECT]` and `[LINEAR_PROJECT_ID]` substitutions to the derived file now.
3. Preserve the generation footer (`*This file is a template. …*`) so the relationship between template and instance stays auditable.
4. Do **not** copy `vision.md`, `state.md`, or `lifecycle.md` into "derived" forms — `vision.md` and `state.md` are the instance files (the templates are their initial form), and `lifecycle.md` is consulted directly from `templates/`.

## Step 5 — First-session handshake

On the first session after setup, the CEO:

1. Runs the **Setup-complete check** (Session-start step 1): reads `vision.md` and `state.md`, confirms neither contains `<!-- IAM:UNFILLED -->`.
2. Walks the **Bootstrap-readiness checklist** (below) with the user, item by item.
3. If all items pass, proceeds to the bootstrap routine (measurability audit + instrumentation plan).
4. If any item fails, halts operational work and returns the user to the relevant step above.

## Bootstrap-readiness checklist

Each item is a binary check. The CEO confirms all before declaring setup complete.

- [ ] Linear project exists and is reachable via the MCP server.
- [ ] `[LINEAR_PROJECT_ID]` substituted everywhere it appears (no literal `[LINEAR_PROJECT_ID]` string remains in the project-root `CLAUDE.md`).
- [ ] `[PROJECT]` substituted everywhere it appears (no literal `[PROJECT]` string remains in `CLAUDE.md`, `vision.md`, or `state.md`).
- [ ] `vision.md` contains real content (North star, Current focuses, Out of scope all populated) and **no** `IAM:UNFILLED` sentinel.
- [ ] `state.md` contains real content (Economic state, Notes for the CEO populated; `Updated:` date set) and **no** `IAM:UNFILLED` sentinel.
- [ ] Project-root `CLAUDE.md` exists, derived from `templates/CEO.CLAUDE.md`, footer preserved.
- [ ] `templates/lifecycle.md` is reachable from the project root (sibling or via the templates directory).

When every box is checked, setup is done. The CEO proceeds to the bootstrap routine defined in `CLAUDE.md`.

---
*Run once per project, before operational work. Edit this template, not its instance, for cross-project changes.*
