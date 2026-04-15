# Design — `how-we-ship.md` recruiting page + `README.md` updates

**Date:** 2026-04-15
**Status:** Draft, pending user review
**Author:** Okis + Claude (brainstorming session)
**Scope:** Spec 1 of 2. Spec 2 (external-distribution case study) will be brainstormed separately after this ships.

---

## 1. Goal

Publish a dedicated page `how-we-ship.md` on careers.mlytics.com that credibly demonstrates Mlytics' AI-first product development practice to engineer candidates, using verifiable evidence from three production repos (`mlytics/aigc-mvp`, `mlytics/agent-will-smith`, `mlytics/databricks`). Simultaneously fix three inaccurate claims on the current `README.md` landing page and link the new page from both job descriptions in `roles/`.

## 2. Out of scope

- External-distribution blog post / case study (Spec 2, separate brainstorm).
- Any code changes to the three source repos.
- Jekyll plugin additions (SEO meta tuning beyond what `jekyll-theme-minimal` provides by default).
- Images, diagrams, video embeds. Text only for this pass.
- Translation to other languages beyond the bilingual quote in § 3 of `how-we-ship.md`.

## 3. Deliverables

Five file changes total:

| # | Type | Path | Purpose |
|---|---|---|---|
| 1 | NEW | `how-we-ship.md` | Long-form dedicated page (~2,170 words) |
| 2 | MODIFY | `README.md` | Insert hook section + fix three inaccurate claims |
| 3 | MODIFY | `roles/ai-powered-full-stack-engineer.md` | Add link-out line near the bottom |
| 4 | MODIFY | `roles/ai-data-engineer.md` | Add link-out line near the bottom |
| 5 | MODIFY | `_config.yml` | `exclude: [docs/]` so this spec file doesn't become a public page |

---

## 4. Content architecture — Deliverable 1: `how-we-ship.md`

**Title (H1):** `How we ship: Becoming Product Builders with Business Thinking`

**Target length:** 2,170 words (tolerance: 1,800–2,300).

**Section map:**

| § | Title | Words | Purpose |
|---|---|---|---|
| 1 | Two single-day ships in nine days | 450 | Make the tempo felt via two concrete stories |
| 2 | Why this is the default — and why it isn't everywhere yet | 450 | The 647/2,330 ratio + brownfield honesty |
| 3 | How Claude Code became our default in three weeks | 550 | Causal explanation, sourced from internal Feb 2026 guide |
| 4 | The data backbone | 320 | Credibility evidence for AI Data Engineer JD |
| 5 | Small teams, real ownership (the uncomfortable truth) | 250 | Reframe team size + filter for fit |
| 6 | What to send us | 150 | CTA, reuses existing README language |

### 4.1 § 1 — "Two single-day ships in nine days" (~450 words)

**Purpose:** Let the reader feel the tempo. Two stories, different engineers, different repos, nine days apart, to defeat the "this is cherry-picked" objection.

**§ 1.a — `aigc-mvp` video pipeline (~230 words):**

- Opening beat: "On April 1, 2026, a team of four shipped a full AI video news pipeline in six hours."
- What the pipeline does, component by component: Seedance image-to-video generator → FFmpeg subtitle burner with logo overlay → GCS upload → per-publisher opt-in flag (`video_news_enabled`) → widget-side video player.
- The merge reference: PR #158, all commits landed within a single morning before being merged to main.
- Why `per-publisher opt-in` matters: multi-tenant turns "pipeline in a day" into a harder problem than "prototype in a day" — every tenant has different configs, different schema expectations, different CSS scopes.
- One-sentence failure admission: the first version of the subtitle burner had timing drift; the fix landed in a follow-up PR two days later.
- Closing beat: "This wasn't a demo. It went into production the same day."

**§ 1.b — `agent-will-smith` brand placement (~180 words):**

- Opening beat: "Nine days later, on April 9, one engineer paired with Claude Opus 4.6 shipped a two-agent brand-integration system in a single day."
- What shipped: two new LangGraph agents (`brand_matcher`, `brand_answer_generator`), 30 files, ~1,680 lines of production Python, merged to main via PR #28 on April 13.
- Why LangGraph is the right abstraction: brand placement needs `match → compose → validate → output` — stateful, ordered, composable. This is what agent orchestration is actually for, not AI-on-everything.
- Brief reference to the 6 total agents in the platform now.

**§ 1.c — closing (~40 words):**

"Different engineers. Different repos. Nine days apart. This is the tempo now."

---

### 4.2 § 2 — "Why this is the default — and why it isn't everywhere yet" (~450 words)

**Purpose:** Prove the single-day ships aren't cherry-picked, via the 647/2,330 Claude-co-authored ratio, while being honest about brownfield lag.

**§ 2.a — headline (~80 words):**

Lead with the number. "647 of our last 2,330 commits across our three newest production codebases list Claude as a co-author — **just over a quarter of everything we shipped**. Not in a pilot, not in one team's experiment. Across all contributors, as the default."

**§ 2.b — per-repo breakdown with explanation (~150 words):**

Compact bullet list:

- `aigc-mvp`: 414 of 1,726 commits (24%), Feb 2025 → Apr 2026, ~4 engineers
- `agent-will-smith`: 135 of 298 commits (45%), Nov 2025 → Apr 2026, ~4 engineers
- `databricks`: 98 of 306 commits (32%) + 91 additional "Generated with Claude Code" trailers, Aug 2025 → Apr 2026, 6 engineers

The percentages differ *and that is itself the interesting finding*: `aigc-mvp` carries a lot of Laravel scaffolding and DB migrations where humans are faster; `agent-will-smith` is dense with prompt engineering and LangGraph state design where AI pairing gives the largest lift; `databricks` is SQL models and data pipelines, in between. Different work, different ratios. The ratio tells you which parts of software development AI is actually reshaping right now.

**§ 2.c — brownfield honesty (~140 words):**

"But these are our three newest systems. Our older products — the multi-CDN decision engine that's been routing 50M+ MAU since before Claude Code existed, legacy internal dashboards, billing integrations dating back to the original SaaS — are still being migrated. Just over a quarter isn't our ceiling. It's our leading edge. If you join us now, part of your job is bringing the remaining three-quarters and the brownfield along with it. We're transforming a profitable, scaled company into an AI-first one. That's harder than building one from scratch, and more interesting."

**§ 2.d — meta-honesty (~80 words):**

"That share is a measurement, not a goal. We didn't optimize for it. If it drops next quarter because the tooling changed, we'll write that up too."

---

### 4.3 § 3 — "How Claude Code became our default in three weeks" (~550 words) **[key section]**

**Purpose:** Narrate the cultural inflection point. Provides the causal explanation for the patterns in §§ 1 and 2.

**§ 3.a — opening (~80 words):**

"In February 2026, our Head of Technology & Growth published an internal guide to the product team. It was titled *Claude Code × Product Development: Becoming Product Builders with Business Thinking*. It was not a tools tutorial. It was a thesis about what the team should become."

**§ 3.b — the thesis as a bilingual pull-quote (~80 words):**

> 「我們不是在用 AI 寫更多程式，我們是在用 AI 解決更多商業問題。每個人都是 Product Builder，不只是工程師。」
>
> "We aren't using AI to write more code. We're using AI to solve more business problems. Everyone on this team is a Product Builder, not just an engineer."
>
> — Internal team guide, February 2026

The Traditional Chinese original is retained deliberately — both because it's the source language, and because the existence of an internal-language document is itself a signal that this is a real artifact, not marketing copy back-translated into Chinese for flavor.

**§ 3.c — the three-week rollout (~200 words):**

Walk through the adoption phases (paraphrased from the internal guide's Part 4):

- **Week 1 — Infrastructure:** everyone installed Claude Code, every repo got a `CLAUDE.md` checked into git as shared team knowledge, `.claude/settings.json` was shared team-wide, the first batch of slash commands (`/commit-push-pr`, `/deploy-staging`, `/run-tests`) was added, and `.mcp.json` configs for BigQuery, Slack, and Sentry were deployed.
- **Week 2 — Workflow:** every non-trivial task had to start in Plan mode (then switch to auto-accept-edits after plan alignment). A `PostToolUse` hook auto-formatted code to eliminate CI formatting churn. Two core subagents (`code-simplifier`, `verify-app`) were committed to git. PR reviews started tagging `@.claude` to write learnings back into CLAUDE.md directly.
- **Week 3 onward — Iteration:** weekly CLAUDE.md review, monthly efficiency audit, internal sharing sessions on individual discoveries.

**§ 3.d — the before/after table (~100 words):**

| Before | After |
|---|---|
| Review every line of diff | Test final behavior |
| File-level guidance | Requirement-level guidance |
| Understand all implementation details | Understand interface contracts |
| Humans as code reviewers | Humans as behavior verifiers |

"This sounds small on paper. In practice, it means a senior engineer's time is spent on what the system does, not on whether the semicolons are in the right places. It also means the entry bar for senior engineering at Mlytics shifted: we no longer value the ability to hand-write perfect code. We value the ability to specify and verify behavior."

**§ 3.e — four team commitments (~70 words):**

Pick the four most differentiated from the internal guide's list of seven:

- **Plan First, Code Second.** Tasks that skip Plan mode don't ship.
- **Verify, Don't Review.** Test behavior, not code.
- **Every Mistake Becomes a Rule.** Errors get written back into CLAUDE.md so the next engineer — human or AI — doesn't repeat them.
- **Ship and Iterate.** Delivery beats perfection; iteration beats planning.

**§ 3.f — closing causal claim (~20 words):**

"We published the guide in February. By April, our commit patterns had diverged from anything we'd seen before."

---

### 4.4 § 4 — "The data backbone" (~320 words)

**Purpose:** Credibility evidence specifically for the AI Data Engineer JD.

**Content beats:**

- On August 27, 2025, Tim Liu made the first commit to what would become the Mlytics company-wide data lake on Databricks. 224 days and 306 commits later, that lake spans four domains (`aigc`, `cdn-analytics`, `customer-core`, `decisive`), 9 Lakeflow pipelines, and 21 scheduled jobs.
- Stack details engineers can verify:
  - Unity Catalog managed through Databricks Asset Bundles (`schemas.yaml` as resource-as-code, not hand-written DDL)
  - 37 Silver SQL models + 28 Gold SQL models
  - MLflow Prompt Registry for versioned prompts (versioning prompts, not just versioning code)
  - Databricks Vector Search via `DeltaSyncVectorIndexSpecRequest`, syncing three Gold content tables embedded with `gemini-embedding-001` through a custom `GeminiEmbeddingProvider`
- Upstream coverage: 8 CDN providers (Akamai, Alibaba, Baishan, CDNetworks, Chunghwa, CloudFront, Tencent, VNCDN).
- Why this matters for the product: the Intent Refinery's monetization path depends on a medallion pipeline that turns raw clickstream events into ad-auction-ready features. Without this layer, every AIGC widget signal stays trapped in S3 buckets. The data work isn't supporting the AI product — it's what makes the AI product monetizable.
- Bridge sentence: "If this reads like infrastructure work you want to own end-to-end, our AI Data Engineer role is the one."

---

### 4.5 § 5 — "Small teams, real ownership (the uncomfortable truth)" (~250 words)

**Purpose:** Reframe small team size as both honest and aspirational. Explicitly exclude people who wouldn't fit, to improve self-selection.

**Content beats:**

- Team sizes stated flatly: `aigc-mvp` ~4 engineers, `agent-will-smith` ~4, `databricks` 6 (dominated by one). "Every production system at Mlytics fits around one table."
- Why we're hiring: not because we're drowning, because we keep finding more things to build than the current team can pick up. Speed creates its own problem.
- Who thrives here (3 bullets):
  - People who want end-to-end ownership (API design → production monitoring, no handoffs)
  - People who have already made AI pair programming part of their daily loop
  - People who can learn from a tech lead at Tim's or Vincent's level and want to operate next to them, not under a skip-level chain
- Who doesn't (3 bullets):
  - Specialists who want a narrow lane
  - People who want big-team process (RFCs, multi-stage approvals, async-only communication)
  - Engineers who are skeptical of AI pair programming as default
- Closing beat: "We'd rather tell you this now than at your three-month review."

---

### 4.6 § 6 — "What to send us" (~150 words)

**Purpose:** CTA. Reuse existing `README.md` language for consistency.

**Content beats:**

- Not a resume. Something that shows how you think.
- A side project, a PR you're proud of, a technical write-up, a message explaining why this caught your attention.
- careers@mlytics.com
- Links to both JDs: `roles/ai-powered-full-stack-engineer.md` and `roles/ai-data-engineer.md`.

---

### 4.7 Page footer

One-line footnote:

> "All commit statistics on this page were gathered from internal git history on 2026-04-15. Numbers shift daily; directionally they shift up."

---

## 5. Content architecture — Deliverable 2: `README.md` modifications

### 5.1 Modification A: insert new "How we ship" section

**Placement:** Between the existing `## About Mlytics` section and the `### By the numbers` subsection.

**Draft copy (final, ready to paste):**

```markdown
## How we ship

In early April 2026, a team of four at Mlytics shipped a full AI video news pipeline in six hours — Seedance image-to-video generation, FFmpeg subtitle burn-in, GCS delivery, per-publisher opt-in, and a widget-side player — all merged in a single pull request on April 1. Nine days later, one engineer paired with Claude Opus 4.6 shipped a two-agent brand-integration system in a day: 1,680 lines of production Python, two new LangGraph agents, one pull request.

Neither was a sprint. Across our three newest production codebases, **647 of our last 2,330 commits list Claude as a co-author**. We're in the middle of turning AI-first pair programming from a leading-edge practice into the default across the whole company. Some of our older systems — the legacy CDN decision engine, internal dashboards — are still catching up. This is what the transformation looks like from the inside, not the press release.

In February 2026 we wrote an internal guide on how we want to build. This is the story of what actually happened when we did:

**[How we ship → Becoming Product Builders with Business Thinking](./how-we-ship.md)**
```

### 5.2 Modification B: three corrections in existing `### By the numbers` list

| Existing line | Replacement | Notes |
|---|---|---|
| `- **4.7M** weekly active users on the AIGC intent product` | `- **Over 100K** weekly active users on our AIGC intent product` | Conservative derivation: an internal `aigc-mvp` analytics report dated 2026-03-26 documents 451,104 unique visitors over ~26 days. Okis may choose a more precise or more recent number at implementation time. |
| `- **58** live publisher integrations (finance, lifestyle, sports)` | `- **22** live publisher integrations (finance, lifestyle, sports)` | Confirmed count from the same internal report. |
| `- **2,500x** efficiency gain: $0.10 AI-generated content vs. $250 human-written` | **KEEP AS-IS** | Explicitly preserved per Okis (2026-04-15): "先保留吧，這是假設性數字" — this is an intentional hypothetical comparison figure, not a code-derived fact, and that framing is acceptable. |

### 5.3 Modification C: replace "50-second animated short" sentence in `### How we work`

**Current:**

> We produced a 50-second animated short from a 475-line transcript using 46 AI API calls in 45 minutes.

**Replacement:**

> We shipped a full AI video news pipeline — image-to-video generation, automated subtitle burn-in, per-publisher opt-in — in under six hours on April 1, 2026. Details in [How we ship →](./how-we-ship.md).

**Rationale:** The original claim has no evidence in any of the three researched repos. It may refer to a prototype that never became a repo, an old branch, or an aspirational estimate. The replacement points to a larger, verifiable, and more recent story (PR #158 in `aigc-mvp`) and cross-links to the new page.

---

## 6. Content architecture — Deliverables 3 & 4: JD link-outs

**Placement:** At the bottom of each role file in `roles/*.md`, inserted immediately before the final `---` separator or "How to Apply" section, whichever exists.

**Exact text to insert into both JDs:**

```markdown
---

**Want to see how we actually build this?** → [How we ship: Becoming Product Builders with Business Thinking](../how-we-ship.md)

---
```

**Rationale for placing at the bottom, not the top:** candidates who have already clicked into a JD are in the middle of a reading task; the link to `how-we-ship.md` is extended reading that supports the JD, not a distraction from it.

---

## 7. Content architecture — Deliverable 5: `_config.yml` update

**Current content:**

```yaml
theme: jekyll-theme-minimal
```

**New content:**

```yaml
theme: jekyll-theme-minimal
exclude:
  - docs/
```

**Rationale:** GitHub Pages with Jekyll renders every Markdown file in the repo root as a public page by default, including `docs/superpowers/specs/*.md`. Adding `docs/` to `exclude` prevents this spec file (and any future internal design docs) from leaking to careers.mlytics.com.

---

## 8. Voice and citation rules (apply to all deliverables)

- Declarative sentences. Numbers over adjectives. Thesis before explanation.
- No "rockstar" / "10x" / "ninja" / "AI-powered synergy" / "cutting-edge".
- Admit failure where it strengthens the claim. Vague positivity reads as marketing; specific honesty reads as a colleague.
- Commit references use format: `PR #N on YYYY-MM-DD` or `merged YYYY-MM-DD`. No commit hashes, no commit message quotes, no diffs, no customer names.
- Author references: aggregate wherever possible ("a team of four", "a single engineer"). Named references allowed only for Okis and Tim Liu, who are already publicly named in the existing JDs.
- Bilingual: primary language is English. Traditional Chinese appears only inside the § 3 pull-quote, preserving the original source language of the internal guide.
- **No emoji anywhere** (except where the existing README already uses them, e.g., `📧` in the CTA — preserved for consistency).

---

## 9. Evidence register

All numbers and factual claims in deliverables must trace to a source in this section. Future edits must maintain traceability.

### 9.1 `aigc-mvp` (research completed 2026-04-15)

- First commit: 2025-02-26. Latest commit: 2026-04-15. Elapsed: 413 days.
- Total commits: 1,726.
- Claude co-authored commits: 414 (24%).
- Core team: ~4 engineers (including Okis and Tim Liu as named in existing JDs; other team members not named publicly per the voice rules in § 8).
- Shipping cadence: 1,726 commits / 59 weeks = ~29 commits/week. Biggest single-day spikes: 64 commits on 2026-03-17, 63 on 2026-04-01, 60 on 2026-03-26.
- Multi-tenancy mechanism: Laravel `members` table + `member_metas` key-value per-tenant config; later `brand_profiles` + `brand_publisher_scopes` layer (April 2026).
- Confirmed tenants on intent-profiles pipeline: 22 (per an internal analytics report dated 2026-03-26).
- Confirmed unique visitors: 451,104 over ~26 days (same report).
- Video pipeline (cited in § 1.a): PR #158, merged 2026-04-01, introduces Seedance I2V generator + FFmpeg subtitle burn with logo overlay + GCS upload + `video_news_enabled` per-member flag + widget video player. All commits landed within ~6 hours on the same day.
- Clickstream SDK (secondary reference): PR #147, shipped 2026-03-20 through 2026-03-27.
- `CLAUDE.md` at repo root; `docs/superpowers/{plans,specs}` directories hold Claude-driven plan/spec artifacts.

### 9.2 `agent-will-smith` (research completed 2026-04-15)

- First commit: 2025-11-03. Latest commit: 2026-04-13. Elapsed: 161 days.
- Total commits: 298 across all branches (123 on main).
- Claude co-authored commits: 135 (~45%), breakdown: 84 Opus 4.5, 27 Opus 4.6 (1M), 16 Opus 4.6, 3 Sonnet 4.5, 2 Sonnet 4.6, 3 generic Claude.
- Core team: ~4 engineers, with one dominant contributor carrying ~48% of commits.
- Framework: LangGraph + FastAPI + Databricks.
- Six distinct agent roles: `product_recommendation`, `answer_generator`, `question_generator`, `intent_chat`, `brand_matcher`, `brand_answer_generator`.
- Brand integration ship (cited in § 1.b): 2026-04-09 (single day), three feature commits introducing `brand_matcher` (14 files, +734 LOC), `brand_answer_generator` (16 files, +946 LOC), and a transient `topic_classifier` (later absorbed into `question_generator`). Authored by a single engineer with Claude Opus 4.6 (1M) as co-author. Merged to main via PR #28 on 2026-04-13.
- `CLAUDE.md` at root (14 KB); `CODE_REVIEWS.md` (56 KB) — AI-driven code review log.
- ⚠️ **The existing README "50-second animated short / 475-line transcript / 46 API calls / 45 minutes" claim has no evidence in this repo** and is being replaced in Modification C above.

### 9.3 `databricks` (research completed 2026-04-15)

- First commit: 2025-08-27. Latest commit: 2026-04-08. Elapsed: 224 days.
- Total commits: 306 (+ 28 merged PRs).
- Claude co-authored commits: 98 (32%). Additional 91 commits carry a `Generated with Claude Code` trailer.
- Core team: 6 engineers. Tim Liu (already named in the AI Data Engineer JD) is dominant with ~60% of commits; two additional sustained contributors carry most of the rest.
- Architecture: 4 domains (`aigc`, `cdn-analytics`, `customer-core`, `decisive`), 9 Lakeflow pipeline YAMLs, 21 job YAMLs.
- SQL models: 37 Silver + 28 Gold.
- Unity Catalog: declared via DAB `schemas.yaml` resource-as-code (3 domains: `aigc`, `cdn-analytics`, `customer-core`). All Lakeflow pipelines set `catalog: ${var.catalog_name}`.
- MLflow: Prompt Registry with versioned prompts used in `content_summarization` pipeline, shared experiment at `/Shared/experiments/${catalog_name}.content_summarization_experiment`.
- Vector Search: `content_vector_index` package uses `databricks.sdk.service.vectorsearch` with `VectorIndexType.DELTA_SYNC` + `DeltaSyncVectorIndexSpecRequest`. Three Gold content tables embedded via custom `GeminiEmbeddingProvider` using `gemini-embedding-001`.
- CDN coverage: 8 providers (Akamai, Alibaba, Baishan, CDNetworks, Chunghwa, CloudFront, Tencent, VNCDN).
- `CLAUDE.md` at root (12 KB); `CODE_REVIEWS.md` (45 KB); `.claude/skills/` with custom team skills committed to git.

### 9.4 PDF source: Mlytics Claude Code Product Development Guide

- Author: Okis, Head of Technology & Growth, Mlytics.
- Published: February 2026 (internal).
- Source: internal team guide on file with the Head of Technology & Growth; excerpts authorized for public use per the brainstorming session on 2026-04-15.
- Content this spec pulls from:
  - Thesis pull-quote for § 3.b: "我們不是在用 AI 寫更多程式，我們是在用 AI 解決更多商業問題。每個人都是 Product Builder，不只是工程師。"
  - Three-week rollout plan for § 3.c (Part 4 of the guide)
  - Old-mode vs. new-mode comparison table for § 3.d (section 1.2 of the guide)
  - Four of the seven team commitments for § 3.e (from the guide's concluding section)

Okis explicitly authorized publishing excerpts from this internal guide during the brainstorming session on 2026-04-15.

---

## 10. Implementation order

Two logical commits total:

**Commit A — spec + config (internal, not user-visible):**
1. Create `docs/superpowers/specs/` directory structure (implicit via `Write` tool)
2. Write this spec file
3. Update `_config.yml` to add `exclude: [docs/]`
4. Commit

**Commit B — recruiting content (user-visible, atomic):**
1. Write `how-we-ship.md` (long form). This is the source of truth; write it first.
2. Modify `README.md`: insert hook section (Modification A), apply three corrections (Modification B), replace "animated short" sentence (Modification C).
3. Append JD link lines to both `roles/*.md` files.
4. Commit.
5. Verify on careers.mlytics.com after GitHub Pages rebuild (~1 minute).

Keeping the two commits separate lets the spec+config change land independently, so if the content commit needs revision after user review, the spec file and the Jekyll exclude are already safely in place.

---

## 11. Acceptance criteria

- [ ] `how-we-ship.md` renders correctly at `careers.mlytics.com/how-we-ship` after the GitHub Pages rebuild.
- [ ] All internal links (`./how-we-ship.md` from `README.md`, `../how-we-ship.md` from both `roles/*.md`) resolve on both github.com and careers.mlytics.com.
- [ ] Total word count of `how-we-ship.md` is within 1,800–2,300 words.
- [ ] `README.md` no longer contains the strings `4.7M`, `58 live publisher`, or `50-second animated short`.
- [ ] No customer names, API keys, commit message quotes, or code diffs appear in any published file.
- [ ] `docs/` is excluded from Jekyll build — visiting `careers.mlytics.com/docs/superpowers/specs/2026-04-15-how-we-ship-recruiting-page-design` returns 404.
- [ ] Both JDs link to `how-we-ship.md` from a prominent place near the bottom.
- [ ] All commit references (`PR #158`, `PR #28`, dates) in published files are factually correct per § 9 above.

---

## 12. Known risks and mitigations

| Risk | Mitigation |
|---|---|
| Numbers drift as new commits land (1,726, 414, 647/2,330, etc.). | Page footer dates the snapshot: "gathered on 2026-04-15". |
| Quoting an internal team document publicly. | Okis explicitly approved on 2026-04-15: "要" in response to the question "要不要大量 quote PDF 的原文". |
| Mentioning "legacy CDN decision engine" publicly could be read as disparaging the company's core profitable product. | Okis explicitly authorized the transparency on 2026-04-15: "可以公開，我想坦白". |
| The hypothetical "2,500x efficiency" figure is preserved on `README.md` despite having no code-derived backing. | Okis explicitly authorized preservation on 2026-04-15: "先保留吧，這是假設性數字". Any future reader asking about it can be told it's a designed comparison figure, not a measurement. |
| Jekyll surprise: default `theme: jekyll-theme-minimal` may render `how-we-ship.md` with an unexpected layout or missing page title. | Test on the github.io fallback URL immediately after the first push of `how-we-ship.md`, before linking it from production README. Fallback: add YAML front matter (`---\nlayout: default\ntitle: How we ship\n---`) if the default rendering is poor. |

---

## 13. Next step after this spec is approved

Per the brainstorming skill's terminal state: invoke the `superpowers:writing-plans` skill to turn this design into a step-by-step implementation plan with verification checkpoints. The plan will likely decompose Commit A and Commit B above into explicit TDD-friendly units (write file → verify → commit → verify rebuild → verify link resolution).
