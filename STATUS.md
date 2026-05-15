# Status — IAM
> Updated: 2026-05-13

## Doing
- **Build threshold crossed 2026-05-13.** Project moves from exploratory → build. Decision: pursue IAM v1.
- **Scope 2026-05-13 — Step 1 = personal OS.** v1 success = "works for me." No generalization, productization, or open-sourcing required at this stage. CEO and templates can be deeply opinionated to user's specific style. *Later expansion (framework / SaaS / research / Academy) is deferred, not closed* — re-evaluate after Step 1 lands.
- **Validation target: Troskapp.** Framework tested against "keep a stalled project moving without the human driving each turn."
- **Substrate decision: Claude Code.** IAM v1 is a methodology on top of Claude Code (templates + conventions + prompts), not new software.

## Survey findings (2026-05-13)
Multi-agent frameworks (MetaGPT, ChatDev, CrewAI, AutoGen, LangGraph, OpenHands) all hit the same walls:
- **Roles collapse** under cognitive load → function-based shape is exactly what fails
- **Horizontal coordination contested** — Cognition explicitly walked back from multi-agent (Devin → single-agent); Anthropic does it at ~15× token cost
- **Termination + memory drift** unsolved at framework level — daily-report cadence lives in the worst regime
- **No "set and forget"** has ever shipped. Every working system has human in loop, CI gates, budget caps
- Berkeley MAST taxonomy: ~2/3 of failures = termination + inter-agent misalignment
- Key references: Cognition "Don't Build Multi-Agents" (Yan, June 2025), MAST paper (arxiv 2503.13657)

## Shape v2 — committed 2026-05-13 (replaces v1 below)
- **One agent the user talks to: the CEO.** Persistent, holds all memory.
- **No employees. Freelance agents** spawn per task, execute, exit. Stateless, ephemeral.
- **Loop is task-volume, not time-based.** User hands CEO a subject → CEO decomposes/dispatches → freelancers execute → CEO reports back + suggests next tasks (approval-gated).
- **Scales by accretion**: start with one task, grow.
- **Why this works (vs v1):** dodges 4/5 survey walls — no role collapse (no persistent roles), no horizontal coordination cost (only vertical), no termination problem (scoped freelancers), no memory drift across N agents (only CEO persists).

### v1 (dropped 2026-05-13)
- 5 function-based horizontal agents with daily reports. Killed by survey findings: role collapse + horizontal coordination cost + memory drift across agents.

## Done (this week)
- Confirmed lens: workforce-style delegation, not chat.
- Dropped "framework must be customizable" — premature abstraction.
- Committed to building (informed by prior art, not competing with it).

## Blocked
(none)

## Next — self-hosting first (v0.5), Troskapp second (v1.0)

### Phase 0 — Bootstrap kernel ✅ (drafted 2026-05-13)
- ✅ `templates/CEO.CLAUDE.md`
- ✅ `templates/vision.md`
- ✅ `templates/state.md`
- ✅ `templates/lifecycle.md`
- ✅ `vision.md` (IAM's own)
- ✅ `state.md` (IAM's own)
- ⏳ **Linear project for IAM tasks** — user action: pick workspace (linear-bourse or linear-opi or new), set `[LINEAR_PROJECT_ID]` in CEO.CLAUDE.md when copied
- ⏳ **Read review** — user reviews the 6 drafted files; revisions before Phase 1

### Phase 1 — IAM-on-IAM (v0.5, self-hosting proof)
Instantiate the CEO against the IAM project itself. First CEO-managed task: **build out the template kit** (lifecycle.md, refined CEO.CLAUDE.md, freelancer briefing format, etc.). Easy-mode test (greenfield + perfect domain expertise). Validates the framework works at all + produces the template kit as natural output.

### Phase 2 — Troskapp pilot (v1.0, hard test)
Copy refined templates into Troskapp, run CEO's measurability audit, real-world stress test. Validates the framework works for the use case actually motivating the project.

### Honest caveat
Self-hosting (Phase 1) is necessary but not sufficient. Validates "framework works for its designer on a greenfield project with perfect context." Does NOT validate "framework works for someone else, on someone else's project, with stale context." Troskapp (Phase 2) is the real test.

## Field validation (sweep complete, 2026-05-13)
**The field converged on our design.** Lead-agent + isolated ephemeral subagents + shared artifact is now the default topology across Anthropic, OpenAI, Google SDKs and OpenHands V1 (Apr 2026). Horizontal peer-to-peer is effectively abandoned. Split is now task-shape based: wide-shallow → multi-agent (Anthropic), deep-narrow (code, coherent work, like Troskapp) → single-agent + subagents (Cognition). Our match is correct.

**New failure class to track**: agent × infrastructure coupling (PocketOS data wipe — Cursor + Railway misconfig erased 3mo of prod data). Matters when CEO dispatches freelancers that touch real infra.

## What IAM is/isn't claiming as novel (post-validation)
- **Not novel**: topology, substrate (Claude Code), memory-in-one-place — all field consensus.
- **Plausibly novel**: OKR-shaped metric layer as CEO concern; proxy design as core CEO skill; self-hosting bootstrap; proactive priority re-ordering; CEO-as-management-methodology framing.
- **Honest scoping**: IAM is *"CEO-style management applied to the converged agent topology, with strong opinions about metric design"* — not a new framework.

## Reading (when time allows)
- **"Dive into Claude Code: The Design Space"** (arxiv 2604.14228, Apr 2026) — maps Anthropic's design choices for our chosen substrate
- **"Governing Evolving Memory in LLM Agents (SSGM)"** (arxiv 2603.11768, Mar 2026) — vocabulary for memory failure modes
- **Lanham "Multi-Agent in Production in 2026: What Actually Survived"** (Apr 2026) — field-report convergence
- **MAST taxonomy paper** (arxiv 2503.13657)
- **"Coordination as an Architectural Layer for LLM-Based MAS"** (arxiv 2605.03310, May 2026)
- **Anthropic multi-agent research blog** (June 2025) — for completeness

## Acknowledged v1 limitations
- Not autonomous — CEO runs when invoked
- Metric-reached triggers need user invocation or scheduled jobs (CronCreate?)
- Cross-session memory only as good as CEO's write discipline

## Reading (when time allows)
- **Anthropic multi-agent research blog** (June 2025) — counter-view to Cognition
- **MAST taxonomy paper** (arxiv 2503.13657) — empirical failure taxonomy, most rigorous source
- **"Context Collapse in Role-Conditioned LLMs"** (arxiv 2511.15573, Nov 2025)
- **"Multi-Layer Memory Architectures"** (arxiv 2603.29194, Mar 2026) — most recent

## Acknowledged v1 limitations
- Not autonomous — CEO runs when invoked
- Metric-reached triggers need user invocation or scheduled jobs (CronCreate?)
- Cross-session memory only as good as CEO's write discipline

## Decisions (2026-05-13)
- **One CEO per project.** No general/multi-project CEO. Isolation > shared state.
- **Memory layered**: operational state in Linear (MCP), strategic state in CEO context, code in filesystem.
- **Task summary format**: what had to be done / what was done / why (lives in Linear per task).
- **Task lifecycle**: user one-liner → CEO pitch → scoping agent → CEO validates (launch/cut on economic state) → executor(s) → reviewer(s, distinct from executors) → CEO reports back + proposes next.
- **Workflow is dynamic per task.** CEO designs the right phase structure based on the task's nature. Scope/exec/review was illustrative, not template.
- **Role separation per phase** (scoper ≠ executor ≠ reviewer) — dodges role-collapse from survey.
- **Vision lives in `vision.md` in project repo.** Versioned, shared with freelancers via briefings. User-edited; CEO can propose changes but doesn't own the file.
- **CEO moat = proactive priority re-ordering.** CEO doesn't just execute tasks; it notices when the priority list is wrong and proposes shifts. This is the IAM-specific value over Claude Code.
- **Re-evaluation trigger = metric-reached.** Each priority and task has a success metric. When metric fires, CEO re-evaluates priorities. Event-driven, no timers.
- **CEO bootstrap routine**: on instantiation, walk the existing backlog with the user and pin a success metric on every priority and task before any execution starts.
- **Structure is OKR-shaped**: Vision (qualitative North Star) → Priority (outcome metric) → Task (deliverable metric + impact score on priority).
- **Post-metric-hit options**: cheap-win detection / ladder-up to new metric / close priority. CEO acts as strategic mind, not just router.
- **Stalled-metric handling**: accumulated task impact gives a progression rate. If rate is bad, the metric itself may be wrong — CEO flags, user decides.
- **CEO requires**: domain knowledge of the project, strategic reasoning, pattern memory across past task impacts. Higher bar than pure orchestration.
- **Impact quantification = automated + CEO-judged hybrid.** Automated layer = raw signal from MCPs/tools (analytics, Linear, errors, PRs). CEO-judged layer = interpretation/attribution on top, **must cite automated evidence** (anti-confabulation guardrail). Task summary in Linear becomes structured: what / why / measured signal / judged impact + rationale.
- **CEO's first delivered task = make the project measurable.** Audit + propose instrumentation plan + execute approved subset. The framework is self-hosting from day one: CEO applies the IAM workflow to its own bootstrap. (Replaces earlier "instrumentation is a precondition.")
- **Bootstrap sequence**:
  1. CEO reads `vision.md` + `state.md`, surveys repo
  2. Proposes measurability audit as first task → user approves
  3. Spawns scoping → returns instrumentation plan → CEO validates against economic state → user approves subset
  4. Spawns executor(s) → measurement layer exists
  5. Walks backlog and pins success metrics (the metric-bootstrap routine)
  6. Normal operation begins
- **Metrics are proxies, by design.** Vision is qualitative; Priority/Task metrics are proxies for what actually matters. The CEO's core skill is **proxy design under uncertainty** — building and refining the chain Vision → Priority proxy → Task proxy → Impact measurement. "Unmeasurable" is never the answer; *"this proxy with these known limits"* is. Bad proxies get refined, not abandoned.
- **User override**: in-band. User talks to CEO, CEO delegates. User says stop → CEO stops freelancers. No metric needed to interrupt.
- **Multi-agent-per-phase coordination**: CEO's discretion per task. No fixed reconciliation rule — matches "workflow is dynamic per task."
- **Staleness backstop**: every task has a staleness budget at creation (proposed default: 14d). Budget elapsed without metric-reached → surfaces in next CEO report with options (extend / re-scope / cut).
- **Strategic memory split into two files** (proposed):
  - `vision.md` — slow-moving: North Star, Current focuses, Out of scope
  - `state.md` (or Linear doc) — faster-moving: Economic state, notes for the CEO

## Parking lot (v2+, do not start)
- **CEO Academy** — shared layer where CEOs publish "success stories" / case studies; new CEOs read for transfer learning. Resolves cold-start without breaking isolation. Genuinely interesting but: requires ≥1 working CEO first, contamination risk (prompt injection across CEOs), and not a separate project — natural emergent output of IAM at scale.

---
*Exploratory project — no pressure, no timeline.*
