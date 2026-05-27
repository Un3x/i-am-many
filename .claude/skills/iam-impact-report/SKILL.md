---
name: iam-impact-report
description: Compose the structured close-out comment whenever the IAM CEO closes a task in Linear, even when the brief or context doesn't name this skill explicitly. Triggers on impact reports, task close-outs, Linear synthesis of freelancer outputs, or any "summarize what just shipped" moment in IAM-managed work. Apply the 7-section structure, the anti-confabulation rule, and the proxy-with-limitations convention; do not transition state or file follow-ups — that is close-out routine, not this skill.
---

# IAM Impact Report

## Role

You compose the impact-report comment for a closed IAM task. The CEO holds the judgment; you hold the structural and anti-confabulation discipline that protects the judgment from drift.

This is the **first main-agent IAM skill** — it applies to the CEO main agent, not to spawned freelancers. The `iam-scoper / iam-executor / iam-reviewer` suite is freelancer-side; this skill shapes the CEO's own output before it lands in Linear.

## What you produce

A single Linear comment with the 7-section shape, returned as the next CEO message before any `save_comment` Linear write. The CEO retains the judgment; the skill shapes the output.

## Mandatory output structure

Seven sections, headers fixed, order locked:

```
## What had to be done
(the brief)

## What was done
(the deliverable, with commit SHAs and file paths)

## Why
(reasoning)

## Measured signal
(raw automated data; cite sources)

## Judged impact
(must cite measured signal)

## Reflection learnings
(preserved for future CEOs)

## Follow-ups filed
```

**Divergence flag.** This is a 7-section comment shape, NOT the A–H letter-indexed report from `iam-scoper` and NOT the 5-field receipt from `iam-executor`. Future readers should not expect a uniform handshake across IAM skills — the close-out comment is its own shape.

## Framework references

Read first when invoked:

- `templates/CEO.CLAUDE.md` § *Impact reporting* — the canonical rule the skill derives from.
- `templates/CEO.CLAUDE.md` § *Accountability* — anti-deflection rule applies to reflections too.
- `~/.claude/CLAUDE.md` global commit conventions — relevant for *What was done* section's commit citations (why-focused messages, no `Co-Authored-By` trailer, GPG-signed).

Paths above resolve from the IAM project root. Use absolute paths when you cite files in the comment.

## Method invariants

These hold for every IAM impact-report composition:

- **Cite measured signal for every impact claim.** No bare *"high impact."* If no direct signal exists, name the proxy and its limitations explicitly, and state confidence (low / medium / high).
- **Capture both the substantive and the meta lesson in reflections.** When reflecting on a correction, capture (a) the principle the correction taught, and (b) why the wrong default fired in the first place.
- **Acknowledge the specific call.** When a correction landed mid-task, name it. Reach for the specific decision, not a "miscommunication" reframe.
- **Cite commit SHAs, absolute paths, and exact file counts.** *"~5 files"* is not a measured signal; *"3 files, 62 insertions / 44 deletions, commit 1a26884"* is.
- **Preserve reflections for future CEOs.** The reflection section is the one piece of cross-session memory; write it for a future CEO reading the comment cold.
- **Surface follow-ups explicitly.** Every close-out flags what's outstanding or what next pitch the close suggests — even if the answer is "none pending."

## IAM corpus carve-out

IAM has no external corpus and no reflection-submission endpoint. `lifecycle.md` § "Freelancer briefing format" item 6(b) reflect-at-spawn routing does not apply in IAM-managed work. Only in-comment reflection (the *Reflection learnings* section) is in scope.

## Boundaries

- Linear state transitions and follow-up issue filing are close-out routine, not this skill. Run them as separate tool calls after the comment lands.
- Mechanical tool-call sequences (`save_comment` → `save_issue` state transition) are out of scope; this skill produces the comment text, the CEO applies it.
- Composing pitches for *next* tasks is `iam-pitch-draft` territory (when that skill ships). This skill closes; that skill opens.

## Closing rule

Return the comment text as the next CEO message before any `save_comment` call, so the principal sees the draft before it lands in Linear.

---
*This skill is derived from `templates/CEO.CLAUDE.md` § Impact reporting + § Accountability. When those sections change, mirror the update here (precedent: IAM-18 / IAM-22 mirror pattern, tracked by IAM-24).*
