# How we ship: Becoming Product Builders with Business Thinking

## Two single-day ships in nine days

On April 1, 2026, a team of four at Mlytics shipped a full AI video news pipeline in six hours. The pipeline takes a news article, generates the visuals with a Seedance image-to-video model, runs the output through an FFmpeg subtitle burner that also overlays the publisher's logo, uploads the finished file to GCS, exposes a `video_news_enabled` opt-in flag per publisher, and renders inside the widget with a native video player. All of that — generator, stitcher, delivery, per-tenant opt-in, front-end player — was designed, written, reviewed, and merged as PR #158 before lunch.

Shipping a pipeline in a day is not hard. Shipping a *multi-tenant* pipeline in a day is harder by an order of magnitude. Every publisher we serve has its own tenant row in `members`, its own per-tenant config in `member_metas`, its own expected schema shape, and its own CSS scope inside the widget. A prototype can ignore all of that. Production cannot. Getting the opt-in flag wired through every layer — database, admin UI, orchestration job, widget client — alone, would have cost a week six months ago.

We also broke it. The first version of the FFmpeg subtitle burner had timing drift — subtitles appearing a beat behind the scene change — and the fix landed in a follow-up PR two days later. We're telling you this deliberately. This wasn't a demo. It went into production the same day, for real publishers, serving real readers.

Nine days later, on April 9, one engineer paired with Claude Opus 4.6 shipped a two-agent brand-integration system in a single day: two new LangGraph agents — `brand_matcher` and `brand_answer_generator` — across 30 files and roughly 1,680 lines of production Python. The agents were drafted, their state graphs wired up, their prompts tuned, and the integration merged to main as PR #28 four days later on April 13.

We chose LangGraph for this feature on purpose. Brand placement, done well, is not a single AI call. It's a pipeline: `match` the right brand to the article intent, `compose` a draft answer that integrates the brand naturally, `validate` that the result doesn't break the host publisher's tone or compliance posture, and `output` the final answer back into the widget. That's stateful, ordered, and composable — exactly what agent orchestration is actually for, and it's why we didn't try to compress the whole thing into a single prompt. Our multi-agent platform now runs six distinct roles: product recommendation, answer generation, question generation, intent chat, brand matching, and brand-aware answer composition.

Different engineers. Different repos. Nine days apart. This is the tempo now.

## Why this is the default — and why it isn't everywhere yet

647 of our last 2,330 commits across our three newest production codebases list Claude as a co-author — just over a quarter of everything we shipped. Not a pilot, not one team's experiment, not the result of a top-down mandate. A measurement across every engineer, every repo, and every working day we could audit.

Here's the per-repo breakdown, which is where it gets more interesting than a single average suggests:

- **`aigc-mvp`** — our multi-tenant AIGC product: **414 of 1,726 commits (24%)**, spanning February 2025 to today, written by roughly four engineers.
- **`agent-will-smith`** — our multi-agent orchestration platform: **135 of 298 commits (45%)**, spanning November 2025 to today, written by roughly four engineers.
- **`databricks`** — our company-wide medallion data lake: **98 of 306 commits (32%)**, plus another **91 commits** carrying a `Generated with Claude Code` trailer that don't list a co-author. Spanning August 2025 to today, written by six engineers.

The percentages differ, and that difference is more honest than a single headline would be. `aigc-mvp` carries a lot of Laravel scaffolding, Eloquent migrations, and plain CRUD that a human can bang out faster than a planning loop. `agent-will-smith` is dense with prompt engineering, LangGraph state design, and agent-role definition — exactly the kind of work where AI pairing gives the largest lift, because the search space is big and the correctness signal is fast. `databricks` is SQL models and data pipelines, in between. Different work, different ratios. The ratio tells you which parts of software development AI is actually reshaping right now. It also tells you where the friction is — a 45% AI-pair rate is not the same as a 45% productivity gain, because some of those commits are the planner and the engineer figuring out together that the first approach was wrong, and restarting.

But these are our three newest systems. Our older products — the multi-CDN decision engine that's been routing 50M+ monthly active users since well before Claude Code existed, legacy internal dashboards, billing integrations dating back to the original SaaS — are still being migrated. Just over a quarter isn't our ceiling. It's our leading edge. If you join us now, part of your job is bringing the remaining three-quarters and the brownfield along with it. We're transforming a profitable, scaled company into an AI-first one. That's harder than building one from scratch, and more interesting.

That share is a measurement, not a goal. We didn't optimize for it. If it drops next quarter because the tooling changed or because a particular project had unusually high infra work, we'll write that up too. The point of measuring is not to defend the number, it's to know when we're lying to ourselves.

## How Claude Code became our default in three weeks

In February 2026, our Head of Technology & Growth published an internal guide to the product team. It was titled *Claude Code × Product Development: Becoming Product Builders with Business Thinking*. It was not a tools tutorial. It was a thesis about what the team should become.

The thesis, verbatim:

> 「我們不是在用 AI 寫更多程式，我們是在用 AI 解決更多商業問題。每個人都是 Product Builder，不只是工程師。」
>
> "We aren't using AI to write more code. We're using AI to solve more business problems. Everyone on this team is a Product Builder, not just an engineer."
>
> — Internal team guide, February 2026

We've preserved the Traditional Chinese original here for two reasons: it is the language the guide was written in, and the existence of an internal-language document is itself a signal that this is a real artifact, not marketing copy back-translated into Chinese for flavor.

The guide came with a three-week rollout plan, and we ran it:

- **Week 1 — Infrastructure.** Every engineer installed Claude Code. Every production repo got a `CLAUDE.md` checked into git as shared team knowledge — project architecture notes, naming conventions, test standards, and common pitfalls, kept around 2.5k tokens so the file stays in context on every task. `.claude/settings.json` was shared across the team so permissions were consistent between people. The first batch of slash commands — `/commit-push-pr`, `/deploy-staging`, `/run-tests` — landed in `.claude/commands/`. MCP configs for BigQuery, Slack, and Sentry went into `.mcp.json` so the model could reach the tools we actually use.
- **Week 2 — Workflow.** Every non-trivial task had to start in Plan mode, then switch to auto-accept-edits once the plan was aligned. A `PostToolUse` hook auto-formatted code to eliminate CI formatting churn. Two core subagents — `code-simplifier` and `verify-app` — were committed to git so everyone had the same review loop. PR reviews started tagging `@.claude` to write learnings back into `CLAUDE.md` directly, so the next PR would benefit from the last PR's mistakes.
- **Week 3 onward — Iteration.** Weekly `CLAUDE.md` review. Monthly efficiency audit. Internal sharing sessions on individual discoveries. The point of the first two weeks was to stop having the same argument twice; the point of week three onward is to compound.

The underlying shift is a change in what a senior engineer actually does with their time:

| Before | After |
|---|---|
| Review every line of diff | Test final behavior |
| File-level guidance | Requirement-level guidance |
| Understand all implementation details | Understand interface contracts |
| Humans as code reviewers | Humans as behavior verifiers |

This sounds small on paper. In practice, it means a senior engineer's time is spent on what the system does, not on whether the semicolons are in the right places. And the entry bar for a senior role here shifted with it: we no longer hire for the ability to hand-write perfect code. We hire for the ability to specify and verify behavior.

Four of the commitments from the guide are load-bearing for that shift:

- **Plan First, Code Second.** Tasks that skip Plan mode don't ship.
- **Verify, Don't Review.** Test behavior, not code.
- **Every Mistake Becomes a Rule.** Errors get written back into `CLAUDE.md` so the next engineer — human or AI — doesn't repeat them.
- **Ship and Iterate.** Delivery beats perfection; iteration beats planning.

We published the guide in February. By April, our commit patterns had diverged from anything we'd seen before.

## The data backbone

On August 27, 2025, Tim Liu made the first commit to what has become the Mlytics company-wide data lake on Databricks. 224 days and 306 commits later, that lake spans four domains — `aigc`, `cdn-analytics`, `customer-core`, and `decisive` — with 9 Lakeflow pipelines and 21 scheduled jobs. 37 Silver SQL models stage and conform the incoming data. 28 Gold SQL models expose it to the rest of the company. This is the backbone.

The stack is specific enough to verify. Unity Catalog is managed through Databricks Asset Bundles, which means every schema and grant lives as resource-as-code in `schemas.yaml` — not handwritten DDL in a notebook somebody ran once. MLflow's Prompt Registry is in active use, so prompts are versioned the same way code is versioned and rolled back the same way code is rolled back. Databricks Vector Search runs via `DeltaSyncVectorIndexSpecRequest`, with three Gold content tables embedded through a custom `GeminiEmbeddingProvider` using Google's `gemini-embedding-001`, kept in sync automatically by Delta sync so the search index is never more than a micro-batch behind the source of truth. Upstream, eight CDN providers — Akamai, Alibaba, Baishan, CDNetworks, Chunghwa, CloudFront, Tencent, and VNCDN — feed normalized usage data through the CDN analytics domain.

None of this is decorative. The Intent Refinery's entire monetization path depends on a medallion pipeline that turns raw clickstream events — scroll depth, active reading time, Q&A interactions, cross-page navigation — into ad-auction-ready features. Without this layer, every AIGC widget signal would stay trapped in S3 buckets and nothing would ever turn into revenue. The data work isn't supporting the AI product — it's what makes the AI product monetizable.

If this reads like infrastructure work you want to own end-to-end, our AI Data Engineer role is the one.

## Small teams, real ownership (the uncomfortable truth)

Our AIGC product has roughly four engineers. Our multi-agent platform has roughly four engineers. Our data lake has six. Every production system at Mlytics fits around one table.

We're not hiring because we're drowning. We're hiring because we keep finding more things to build than the current team can pick up — the Intent Refinery has more threads than the team has hands. Speed creates its own problem.

Who thrives here:

- People who want end-to-end ownership — API design, database schema, deployment, production monitoring, user feedback, all of it, no handoffs and no "that's the platform team's problem".
- People who have already made AI pair programming part of their daily loop and want to work somewhere that treats that as the floor, not the ceiling.
- People who want to operate next to a tech lead — someone like Tim Liu on the data side — rather than under four layers of skip-level reporting.

Who doesn't:

- Specialists who want a narrow lane. There isn't one to give you here; the scope for every role is too wide.
- People who want big-team process: multi-stage RFC reviews, staged approvals, async-only communication, three sign-offs per merge. Our cadence breaks under that kind of ceremony.
- Engineers who are skeptical of AI pair programming as a default working mode. We can't retrofit that conviction in onboarding.

We'd rather tell you this now than at your three-month review.

## What to send us

Not a resume. Something that shows how you think.

A side project you've shipped. A pull request you're proud of. A technical write-up that taught you something. A message explaining why any of this caught your attention and what you'd try to build if you got here. Prototypes you abandoned count. So does code you wish you'd written differently — we're more curious about how you think than about polish. Whatever you send, expect us to ask about one decision you could have made differently.

**Email: [careers@mlytics.com](mailto:careers@mlytics.com)**

Two roles we're currently hiring for:

- [AI-Powered Full Stack Engineer](./roles/ai-powered-full-stack-engineer.md) — Product team, Singapore / Taipei
- [AI Data Engineer](./roles/ai-data-engineer.md) — Data & Innovation team, Singapore / Taipei

We read what you send within a week. If we don't think there's a fit, we'll tell you why — not a form letter.

We care about what you've built more than where you've worked.

---

_All commit statistics on this page were gathered from internal git history on 2026-04-15. Numbers shift daily; directionally they shift up._
