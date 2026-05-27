---
name: iam-session-start
description: Run the canonical IAM session-start protocol at the first turn of every new IAM CEO invocation, even when the user opens with a direct request and doesn't name this skill. Triggers on session start, session open, first turn of a new IAM session, fresh CEO instantiation, "where are we" / "what's the state" / "what should I work on" opening prompts, or any IAM-managed conversation that hasn't yet established current state. Apply the 7-step protocol — setup-sentinel check, vision.md + state.md read, working-tree audit, Linear enumeration across all live states, formatted state summary — before responding to the user's opening ask; do not skip steps because the user's first message looks scoped.
---

# IAM Session Start

## Role

You run the IAM session-start protocol — hydrate the CEO's state from `vision.md`, `state.md`, the working tree, and Linear before responding to the user's opening ask. The CEO holds the focus judgment (which active priority deserves this session's attention); you hold the procedural discipline that ensures the judgment is grounded in current state, not stale memory.

This is a **main-agent IAM skill**, sibling to `iam-impact-report` and `iam-pitch-draft`. It is the only IAM skill that fires once per session at session open; sibling skills fire many times per session at task-shape moments.

## What you produce

A sequence of tool calls (read, bash, Linear MCP) followed by a one-line state summary to the user, returned before any task work begins. Not a text artifact for downstream consumption.

## Mandatory output structure

Seven actions in fixed order:

1. **Sentinel check** — grep `<!-- IAM:UNFILLED -->` in `vision.md` and `state.md`. If matched, **halt operational work** and walk the user through `setup.md`'s bootstrap-readiness checklist. The sentinel is the only legitimate session-start short-circuit.
2. **Read `vision.md`** — strategic anchor.
3. **Read `state.md`** — economic state, current notes. (Actions 2 and 3 are typically issued as parallel tool calls.)
4. **Run `git status`.** If output flags `CLAUDE.md`, `state.md`, or any path under `templates/` as modified, run `git diff` on each match. Uncommitted changes in load-bearing areas are part of current state.
5. **Query Linear** via the configured MCP server. Enumerate ALL live states: `backlog` + `unstarted` + `started` + recent `completed`. Do not pre-filter unless a stated reason applies (default filters routinely miss meta-issues sitting in Backlog).
6. **Emit the summary line** in exactly this format: `"Active: <N>. Stalled: <N>. Last closed: <issue-id> (<title>)."`
7. **Ask** the user what to focus on. State-then-ask is the protocol invariant; ask-first would short-circuit hydration.

**Divergence flag.** This skill's output is a tool-call sequence plus a one-line state summary, NOT:

- the A–H scoping report (`iam-scoper`)
- the 5-field deliverable receipt (`iam-executor`)
- the verdict block (`iam-reviewer`)
- the 7-section close-out comment (`iam-impact-report`)
- the 6-section pitch markdown (`iam-pitch-draft`)

Each IAM skill carries its own role-shaped output structure. Future readers should not expect a uniform handshake across skills.

## Framework references

Read first when invoked:

- `templates/CEO.CLAUDE.md` § *Session start* — the 7-step protocol source of truth.
- `vision.md` + `state.md` — the strategic memory files this skill hydrates from.
- The configured Linear MCP server — workspace-scoped enumeration target.

Paths above resolve from the IAM project root. Use absolute paths when you cite files in your summary.

## Method invariants

These hold for every IAM session-start pass:

- **Run the sentinel check before any other read.** If `<!-- IAM:UNFILLED -->` appears in `vision.md` or `state.md`, setup is incomplete — halt operational work and route to `setup.md`. The sentinel is the only legitimate session-start short-circuit.
- **Read both `vision.md` and `state.md` every session, in full.** Sessions are stateless to the CEO main agent; no skipping based on prior-session memory.
- **Treat uncommitted changes in load-bearing files as current state.** When `git status` flags `CLAUDE.md`, `state.md`, or `templates/`, run `git diff` on each before summarizing. Diffs in these areas modify what the session-start summary should say.
- **Enumerate Linear across all live states explicitly.** `backlog` + `unstarted` + `started` + recent `completed`. Pre-filter only with a stated reason. Narrow queries hide the thing that would change the conclusion.
- **Emit the summary in the locked format.** `"Active: <N>. Stalled: <N>. Last closed: <ID> (<title>)."` Variation erodes the principal's session-open scanning habit.
- **Ask the principal what to focus on after the summary — never before.** State-then-ask is the protocol invariant.

## IAM corpus carve-out

IAM has no external corpus and no reflection-submission endpoint. Only in-session reflection (when the CEO chooses to surface session-start observations to the user) is in scope. `lifecycle.md` § "Freelancer briefing format" item 6(b) reflect-at-spawn routing does not apply — that's freelancer-side. The per-session protocol does not need to repeat this carve-out — it is locked here.

## Boundaries

- **Session-open only.** Mid-session state re-checks (e.g., *"what's in Linear now?"* after a task closes) are normal tool calls, not this skill. This skill fires once per CEO invocation, at the first turn.
- **State hydration, not action.** The skill ends at the focus-ask. Acting on a chosen focus (drafting a pitch, spawning a freelancer, closing a task) is downstream of this skill.
- Sub-agents and `skill-creator` invocations are out of scope. One protocol pass per session.

## Closing rule

Emit the state summary and the focus-ask as the next assistant message. The CEO acts on the principal's focus response in subsequent turns; this skill terminates at the ask.

---
*This skill is derived from `templates/CEO.CLAUDE.md` § Session start. When that section changes, mirror the update here (precedent: IAM-18 / IAM-22 mirror pattern, tracked by IAM-24).*
