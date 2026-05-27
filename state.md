# State — IAM
> Updated: 2026-05-27

## Economic state

- **Budget**: zero monetary. No paid infra, no third-party services.
- **Compute**: Claude Code (Opus 4.7) via existing subscription. No additional spend.
- **Attention**: side-project tier. Priority projects are Passemarche and Bangun; IAM gets leftover focus. Sessions are short and infrequent.
- **Acceptable cost per task**: low. Multi-hour agent runs are not affordable in the short term. Token-cheap operations preferred.

## Notes for the CEO

- **User is the designer of IAM.** Has full context. Has strong opinions about scope. Don't propose features that conflict with the personal-OS scope.
- **Side-project rules apply**: track, don't push. Don't nag if IAM stalls — that's normal for side projects in this vault.
- **Field has converged on IAM's topology** (lead-agent + isolated ephemeral subagents). Don't reinvent. Reference papers: arxiv 2503.13657 (MAST), arxiv 2603.11768 (SSGM), arxiv 2604.14228 (Claude Code design space).
- **Phase 1 self-hosting complete (2026-05-16).** Stage-1 templates Phase-2-ready (validated via dry-run; 0 blocks). Four tasks ran the full lifecycle: IAM-5 (walk), IAM-6 (first fix), IAM-7 (dry-run / Trusting Trust check), IAM-8 (iterate + re-validate).
- **Phase 2 strategy was: skill-shaped IAM, prototyped on a fresh project first.** Both parallel-directory and direct-Troskapp approaches rejected. New direction: the CEO is the project's default voice (lives in project `CLAUDE.md` + `vision.md` + `state.md`); freelancers spawned by the CEO get behavior from dedicated skills, NOT from inheriting the project `CLAUDE.md`. Prototype on a fresh project (no existing `CLAUDE.md` to convert) before tackling Troskapp's existing-stack integration. `setup.md` and `templates/CEO.CLAUDE.md` are likely scrapped, not patched. See [[iam-deployment-shape]] in auto-memory. IAM-9 (parallel-directory pitch) cancelled.
- **Phase 2 closed (2026-05-20).** Prototype hypothesis held: deployment shape validated; AISS CEO operates correctly post-patch. Three behavioral gaps (IAM-11/12/13) patched as stopgaps. Meta-finding IAM-14 (template biased passive/deferential) is the live framework-iteration anchor — folds into next templates/CEO.CLAUDE.md rewrite + new-shape design.
- **Phase 2 prototype testbed (bootstrapped 2026-05-16): AI Success Story.** A blog of first-person AI-authored success stories — dual scoreboard (product candidate + IAM testbed). Repo: `/home/unex/Project/ai-success-story/`. Lives in its own Linear workspace with its own MCP server (set up by user out-of-band; not reachable from i-am-many session). Main project ID inside that workspace: `5eb1786a-045e-49b1-9e8b-9d4d1ca602a2`. Phase umbrella issue: IAM-10. Friction signal cycles back to i-am-many Linear as new framework-tier issues. (`7a350c3b-…` mistakenly created in iammany workspace during bootstrap — cancelled. See IAM-11 for the framework gap that caused the mistake.) Now operational with patched CEO behavior; IAM-10 closed 2026-05-20.
- **Dry-run friction logs archived** at `_archive/dryrun-friction-logs/{v1,v2}.md` after deleting the `iam-dryrun*` workspaces.
- **Friction-sweep backlog**: ~30 friction-tier items deferred across IAM-5/6/7/8. Largely targets `setup.md` procedure — likely obsoleted if `setup.md` is rewritten/deleted under the new shape. Defer triage until Phase 2 prototype concludes.
- **2026-05-27 — framework iteration complete.** CEO template structurally rewritten (IAM-14, commit `1a26884`, mandate-led foundation, ~80/20 affirmative). `setup.md` resolved as trim+keep (IAM-19; supersedes the "likely scrapped" framing above). AISS instance synced (IAM-22, commit `2ba1e38`). Skill library built end-to-end: freelancer-side `iam-{scoper,executor,reviewer}` (IAM-23 + IAM-26) and CEO-side `iam-{impact-report,pitch-draft,session-start}` (IAM-28 + IAM-29 + IAM-30). 6 skills total at `.claude/skills/iam-*/`. Polish bundle landed (IAM-27, commit `9d9a4b3`). Brief-shrinkage on `iam-scoper`: ~70% multi-instance stable across 4 real uses.
- **Phase 3 (real-project test) redirected**: Troskapp → idle-game project (user call 2026-05-27). Idea-stage; not yet specified. Pre-requirements: IAM-25 (setup.md propagation for `.claude/skills/` to new IAM projects).
- **Pending observation, next session**: does the harness auto-trigger CEO-side skills on the main agent? (`iam-session-start` at session open; `iam-impact-report` on close-outs; `iam-pitch-draft` on new tasks.) If yes → build `iam-next-task-proposal` (last named CEO-side candidate). If no → redesign main-agent skill discovery before extending the library.
- **Open follow-ups**: IAM-20 (setup.md trim against new template), IAM-21 (Operating-constraints dedup CEO.CLAUDE.md ↔ lifecycle.md), IAM-24 (lifecycle.md ↔ skills sync routine), IAM-25 (setup.md skill propagation). Friction-sweep triage (~30 items from IAM-5/6/7/8) still deferred.
- **No autonomous operation.** CEO runs when invoked. Don't try to schedule things prematurely.

---
*Edited by the user. CEO may propose changes; user decides. Updates more often than `vision.md`.*
