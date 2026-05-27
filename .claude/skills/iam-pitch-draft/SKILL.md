---
name: iam-pitch-draft
description: Draft the structured pitch whenever the IAM CEO frames a new task — translating a user one-liner, a proactive proposal, or a follow-up signal into the canonical Origin / Pitch / Direction / Success metric / Out of scope / Related issue description before any Linear write. Use even when the brief or context doesn't name this skill explicitly. Triggers on IAM pitch drafting, task framing, next-task proposals, user one-liner translation, or any "let's file an issue for X" moment in IAM-managed work. Apply the 6-section structure, the quantified-Origin discipline, and the markdown-link convention for cross-issue refs; do not save the issue or transition state — that is filing routine, not this skill.
---

# IAM Pitch Draft

## Role

You draft the pitch text for a new IAM task. The CEO holds the strategic judgment (what's in-vision, what's in-budget, what priority it serves); you hold the structural and quantification discipline that protects the judgment from drift.

This is a **main-agent IAM skill** — it applies to the CEO main agent, not to spawned freelancers. The `iam-scoper / iam-executor / iam-reviewer` suite is freelancer-side; the `iam-impact-report / iam-pitch-draft` pair is CEO-side. The impact-report closes; this one opens.

## What you produce

A single markdown pitch (issue description) with the 6-section shape, returned as the next assistant message before any `save_issue` Linear write. The CEO retains the judgment; the skill shapes the output.

## Mandatory output structure

Six sections, headers fixed, order locked:

```
## Origin
(triggering event + quantified recurrence + linked prior IAM issues)

## Pitch
(Bucket tag + strategic framing one paragraph)

## Direction
(phase-structured: Scope phase / Execute phase / Review phase; name skill invocations)

## Success metric
(Deliverable + ≥1 named proxy with target + Behavioral check when applicable)

## Out of scope
(3–4 bulleted carve-outs)

## Related
(bulleted IAM-XX refs with one-line note each)
```

**Conditionality clause.** `## Pitch` may be skipped when the Origin paragraph already establishes the Bucket tag and strategic framing self-evidently (e.g., direct follow-up pitches whose framing is implicit in the parent issue; precedent: IAM-26 was a direct execution follow-up where the parent issue's framing was implicit). Default: include `## Pitch`. Skip only when its content would purely restate Origin.

**Optional additional sections** (include when justified):

- `## Cost estimate` — when scope is unfamiliar and no precedent sets cost expectation
- `## Strategic context` — when vision-tie-in is non-obvious from issue title

**Divergence flag.** This 6-section pitch shape diverges from sibling IAM skill outputs:

- NOT the A–H letter-indexed scoping report (`iam-scoper`)
- NOT the 5-field deliverable receipt (`iam-executor`)
- NOT the 7-section close-out comment (`iam-impact-report`)

Each IAM skill carries its own role-shaped output structure. Future readers should not expect a uniform handshake across skills.

## Framework references

Read first when invoked:

- `templates/CEO.CLAUDE.md` § *Proactive proposal* + § *Task lifecycle* — pitch framing source of truth.
- `templates/lifecycle.md` § *Task anatomy* — names the 6 task fields (one-liner, pitch, scope, execution plan, success metric, staleness budget).
- The per-task strategic context from `vision.md` + `state.md` when the CEO flags them.

Paths above resolve from the IAM project root. Use absolute paths when you cite files in the pitch.

## Method invariants

These hold for every IAM pitch composition:

- **Quantify the Origin recurrence.** Every Origin paragraph names a count, percent, or session-N tally — never bare adjectives like *"many"* or *"frequent."* Examples from the corpus: *"5 closed tasks, 5 nearly-identical comment structures,"* *"6+ audit instances, ~50% brief absorption,"* *"8 pitches drafted this session."*
- **Cite cross-issue refs as `[IAM-XX](url)` markdown links, not bare strings.** Bare `IAM-XX` breaks Linear reading flow. Markdown links are universal across the IAM corpus.
- **Name a quantitative success proxy with a target value.** No bare *"ship the skill."* Every Success metric section names a measurable proxy and a target (e.g., *"-40% tokens vs. comparable session-IAM-14 brief,"* *"≥40% shorter than the IAM-23 scope brief"*).
- **Phase-structure the Direction section** with `**Scope phase**:` / `**Execute phase**:` / `**Review phase**:` bold-prefixed paragraphs in order. Name the freelancer skill each phase invokes (`invoking iam-scoper`).
- **Bullet the Out of scope section with 3–4 defensible carve-outs.** Each item rules out a concrete thing a future reader might assume is included. Maintain the band — fewer reads as omission, more reads as defensive.
- **Use absolute paths, backtick-wrapped file refs, backtick-wrapped commit SHAs.** *"`12c3281`"* not *"the recent commit;"* *"`/home/unex/Project/i-am-many/.claude/skills/iam-pitch-draft/`"* not *"the new skill directory."*

## IAM corpus carve-out

IAM has no external corpus and no reflection-submission endpoint. Only in-pitch reflection (when the CEO chooses to include a reflection note in the issue description) is in scope. `lifecycle.md` § "Freelancer briefing format" item 6(b) reflect-at-spawn routing does not apply — that's freelancer-side. The per-pitch composition does not need to repeat this carve-out — it is locked here.

## Boundaries

- Linear writes (`save_issue`, state transitions, label application) are filing routine, not this skill. Run them as separate tool calls after the pitch text lands.
- Composing impact reports for *closed* tasks is `iam-impact-report` territory. This skill opens; that skill closes. When a close-out triggers a new pitch, invoke both in sequence (impact-report on the closing issue, pitch-draft for the new one) — not as alternatives.
- Sub-agents and `skill-creator` invocations are out of scope. One pitch-draft pass, one return.

## Closing rule

Return the pitch text as the next assistant message before any `save_issue` call, so the principal sees the draft before it lands in Linear.

---
*This skill is derived from `templates/CEO.CLAUDE.md` § Proactive proposal + § Task lifecycle, and `templates/lifecycle.md` § Task anatomy. When those sections change, mirror the update here (precedent: IAM-18 / IAM-22 mirror pattern, tracked by IAM-24).*
