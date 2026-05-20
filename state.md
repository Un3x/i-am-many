# State — IAM
> Updated: 2026-05-20

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
- **Next framework iteration:** IAM-14 (structural rewrite of `templates/CEO.CLAUDE.md` — lead with mandate, demote 'You don't', add Authority section, audit approval gates). To be threaded into the new-shape design. `setup.md` rewrite/scrap decision is its own pitch. Friction-sweep triage (~30 items from IAM-5/6/7/8) deferred to a follow-up.
- **No autonomous operation.** CEO runs when invoked. Don't try to schedule things prematurely.

---
*Edited by the user. CEO may propose changes; user decides. Updates more often than `vision.md`.*
