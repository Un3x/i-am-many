# Setup — Instantiating IAM for a new project

This document is the bootstrap layer for IAM. Run it once, per project, **before** the CEO does any operational work. Its job is to turn the `templates/` directory into a working instance:

- Linear workspace reachable via the configured MCP server
- Strategic memory files (`vision.md`, `state.md`) seeded with real content and promoted to the project root
- Project-root `CLAUDE.md` derived from the CEO template
- All template slots substituted with real values

Once this is done, the day-1 CEO can pass the Setup-complete check at the top of its Session-start routine and proceed to the bootstrap routine (measurability audit).

**Who runs this:** the setup-runner — the user, possibly with an assistant in the loop. This document never assumes a second human is present; wherever the runner needs input that only the user can provide (vision content, economic state), the runner gathers it from the user as the sole authoritative source.

**Conventions used here** (audience tags, path resolution, slot delimiters): see `lifecycle.md#framework-conventions`. Each section below carries an `Audience:` tag at the top, with one of two values:

- `Audience: setup-runner` — imperative; actions to perform.
- `Audience: CEO` — descriptive / handoff; for the CEO once setup is complete.

## Prerequisites

*Audience: setup-runner*

Before starting, you must have:

- A Linear workspace you can administer, with an MCP server registered for that workspace in your Claude Code config
- A git repository for the IAM-managed project (this need not be the IAM framework repo itself)
- The IAM `templates/` directory available inside that project repo (see Step 0)
- A Claude Code session with the `Agent` tool and the `linear-*` MCP server configured

## Step 0 — Get `templates/` into the project repo

*Audience: setup-runner*

`setup.md` operates on files under `templates/`. Before running any other step, ensure that directory exists inside the project repo. Two supported branches:

1. **Fork-for-single-project.** The IAM framework repo (or a clone) **is** the project repo. You will keep editing `templates/` directly during Step 2, and the derived `CLAUDE.md` will sit alongside `templates/` at the repo root.
   - Action: `git clone <iam-framework-repo-url> <project-name> && cd <project-name>`.
   - Step 2 will mutate `templates/` in-place.

2. **Reusable framework.** The project repo is separate; IAM is consumed as a reusable bundle. `templates/` is copied (or vendored as a git submodule / subtree) into the project repo without being mutated, and Step 2's substitutions are deferred to Step 4.
   - Action (copy):
     ```bash
     cp -r <path-to-iam-framework>/templates <project-repo>/templates
     ```
   - Or (submodule):
     ```bash
     git -C <project-repo> submodule add <iam-framework-repo-url> iam-framework
     ln -s iam-framework/templates <project-repo>/templates
     ```
   - Step 2 will be a no-op on the templates; substitution happens only on the derived `CLAUDE.md` in Step 4.

Pick one branch and remember which — Step 2 and Step 4 both reference the choice.

## Slot inventory

*Audience: setup-runner*

Every placeholder that must be substituted, and where each appears. Slots use the `{{X}}` delimiter (see `lifecycle.md#framework-conventions`); the `[X]` form in prose is **not** a slot and must be left as-is.

| Slot | Form | Appears in |
| --- | --- | --- |
| Project name | `{{PROJECT}}` | `templates/CEO.CLAUDE.md` (title, Role paragraph), `templates/vision.md` (title), `templates/state.md` (title) |
| Date | `{{DATE}}` | `templates/state.md` (Updated header) |

In addition, two sentinel markers must be removed once their files are filled:

| Sentinel | File | Removed at |
| --- | --- | --- |
| `<!-- IAM:UNFILLED -->` | `templates/vision.md` (top) | Step 3 |
| `<!-- IAM:UNFILLED -->` | `templates/state.md` (top) | Step 3 |

The CEO's Session-start Setup-complete check greps for `IAM:UNFILLED` in the project-root `vision.md` and `state.md`; presence on either file means instantiation is incomplete.

## Step 1 — Verify Linear workspace + MCP connectivity

*Audience: setup-runner*

1. Confirm you have a Linear workspace you can administer for this project. (Each IAM CEO operates against one Linear workspace; sub-projects within the workspace are the CEO's own organizational tool, not its identity.)
2. Register a Linear MCP server pointing at that workspace in your Claude Code config. The CEO will use this MCP on every session to query in-flight and recently-closed work.
3. Verify connectivity: `claude mcp list` should show the Linear MCP as connected. If a workspace query (`list_issues`) returns results (even an empty list), the CEO can reach the workspace.

Output of this step: a working MCP connection. No UUIDs or project IDs are required — the CEO operates at workspace scope.

## Step 2 — Fill template slots

*Audience: setup-runner*

Substitute the slots from the inventory across the three template files:

- `templates/CEO.CLAUDE.md` — replace every `{{PROJECT}}` with the project name.
- `templates/vision.md` — replace `{{PROJECT}}` with the project name.
- `templates/state.md` — replace `{{PROJECT}}` with the project name; replace `{{DATE}}` with today's date.

Do this **in the template files themselves** only if you took the fork-for-single-project branch in Step 0. If you took the reusable-framework branch, leave the templates untouched and defer substitution to Step 4 (it will operate on the derived `CLAUDE.md` only).

Leave the `[PROJECT]` string in the `CEO.CLAUDE.md` generation footer untouched — it is a documentation reference, not a slot marker (see `lifecycle.md#framework-conventions`).

## Step 3 — Initialize strategic memory

*Audience: setup-runner*

Both `vision.md` and `state.md` ship with placeholder scaffolding and an `<!-- IAM:UNFILLED -->` sentinel at the top. At this point they still live under `templates/`; Step 4 promotes them to the project root.

1. Open `templates/vision.md`. Gather from the user and fill in:
   - **North star** — qualitative anchor; 1–2 paragraphs.
   - **Current focuses** — 3–5 priorities, in priority order.
   - **Out of scope** — explicit non-goals.
2. Open `templates/state.md`. Gather from the user and fill in:
   - **Economic state** — budget, compute, attention, acceptable cost per task.
   - **Notes for the CEO** — current context the CEO should hold.
3. **Remove the `<!-- IAM:UNFILLED -->` line** from the top of each file. The CEO's Setup-complete check uses this string as the binary detector.

The user is the sole authoritative source for the content of these files. The setup-runner is the scribe.

These files are user-owned from this point on. The CEO may propose changes; the user decides.

## Step 4 — Derive instance CLAUDE.md and promote strategic memory

*Audience: setup-runner*

1. Copy `templates/CEO.CLAUDE.md` to the project root as `CLAUDE.md`.
2. Apply slot substitutions to the derived `CLAUDE.md` based on which Step 0 branch you took:
   - **Fork-for-single-project branch** (Step 2 already substituted the templates): copy with no additional substitution needed.
   - **Reusable-framework branch** (Step 2 was a no-op): apply the `{{PROJECT}}` → project name substitution to the derived `CLAUDE.md` now.
3. Preserve the generation footer (`*This file is a template. …*`) verbatim. The footer references `[PROJECT]` as documentation, not as a slot marker — do not substitute that occurrence. The footer must remain intact so the relationship between template and instance stays auditable.
4. **Promote strategic memory to the project root.** Move (or copy, if you want the template originals preserved) `templates/vision.md` and `templates/state.md` to the project root:
   ```bash
   mv templates/vision.md vision.md
   mv templates/state.md state.md
   ```
   After this step, `vision.md` and `state.md` at the project root are the operational instances the CEO reads on every session. The CEO does **not** consult `templates/vision.md` or `templates/state.md` at runtime.
5. `lifecycle.md` is consulted by the CEO directly from `templates/lifecycle.md`; no promotion required. (Path references inside `CLAUDE.md` resolve from the project root per `lifecycle.md#framework-conventions`, so the CEO finds `lifecycle.md` via either location.)

## Step 5 — First-session handshake

*Audience: CEO*

On the first session after setup, the CEO:

1. Runs the **Setup-complete check** (Session-start step 1): reads project-root `vision.md` and `state.md`, confirms neither contains `<!-- IAM:UNFILLED -->`.
2. Walks the **Bootstrap-readiness checklist** (below) item by item.
3. If all items pass, proceeds to the bootstrap routine (measurability audit + instrumentation plan).
4. If any item fails, halts operational work and surfaces the failing item back to the user so the relevant earlier step can be repeated.

## Step 6 — Setup-runner self-check

*Audience: setup-runner*

Before declaring setup complete, walk the **Bootstrap-readiness checklist** (below) yourself, item by item. If any item fails, return to the relevant earlier step and fix it before handing off to the CEO. The same checklist is re-run by the CEO on its first session; passing it here saves a round-trip.

## Bootstrap-readiness checklist

*Audience: setup-runner and CEO*

Each item is a binary check. The setup-runner walks the checklist at the end of Step 6 (self-check); the CEO re-walks it on its first Session-start before declaring setup complete and starting operational work. Either side flags a failure by halting and returning to the relevant step.

- [ ] Linear workspace is reachable via the configured MCP server (`claude mcp list` shows it connected).
- [ ] `{{PROJECT}}` substituted everywhere it appears (no literal `{{PROJECT}}` string remains in `CLAUDE.md`, `vision.md`, or `state.md`).
- [ ] `vision.md` and `state.md` exist **at the project root** (Step 4 promotion complete; not only present under `templates/`).
- [ ] `vision.md` contains real content (North star, Current focuses, Out of scope all populated) and **no** `IAM:UNFILLED` sentinel.
- [ ] `state.md` contains real content (Economic state, Notes for the CEO populated; `Updated:` date set) and **no** `IAM:UNFILLED` sentinel.
- [ ] Project-root `CLAUDE.md` exists, derived from `templates/CEO.CLAUDE.md`.
- [ ] Project-root `CLAUDE.md` footer is intact (matches the template footer verbatim) and contains no substituted slot values — its `[PROJECT]` occurrence is a documentation reference and must remain literal.
- [ ] `templates/lifecycle.md` is reachable from the project root (sibling or via the templates directory).

When every box is checked, setup is done. The CEO proceeds to the bootstrap routine defined in `CLAUDE.md`.

---
*Run once per project, before operational work. Edit this template, not its instance, for cross-project changes.*
