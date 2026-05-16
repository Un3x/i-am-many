# State — IAM
> Updated: 2026-05-16

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
- **Phase 2 strategy: dress-rehearsal first.** Apply IAM to a fake project before Troskapp. Troskapp is a real app — don't conflate "does IAM work" with "does IAM help Troskapp." Trailbook (the synthetic project used in dry-runs, at `/home/unex/Project/iam-dryrun-v2/`) is a plausible continuation candidate.
- **Friction-sweep backlog**: ~30 friction-tier items deferred across IAM-5/6/7/8. Batch when Phase 2 dress-rehearsal surfaces what actually matters in practice.
- **No autonomous operation.** CEO runs when invoked. Don't try to schedule things prematurely.

---
*Edited by the user. CEO may propose changes; user decides. Updates more often than `vision.md`.*
