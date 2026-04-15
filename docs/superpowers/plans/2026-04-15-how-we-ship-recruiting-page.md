# how-we-ship Recruiting Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Ship a new public `/how-we-ship.md` page plus targeted `README.md` corrections and JD link-outs on careers.mlytics.com, implementing the approved design in `docs/superpowers/specs/2026-04-15-how-we-ship-recruiting-page-design.md`.

**Architecture:** Content-only additions to a Jekyll + GitHub Pages site. No new code, no templates, no dependencies. Five file changes total; one of them (the `_config.yml` exclusion) already landed in commit `506c9ce`. The remaining four file changes ship as one atomic commit (Commit B per the spec) so the live site transitions in a single rebuild.

**Tech Stack:** Jekyll (`jekyll-theme-minimal` via GitHub Pages free plan), Markdown, `git`, `gh` CLI.

---

## Context for the executor

**Before starting any task, read the design spec:** `docs/superpowers/specs/2026-04-15-how-we-ship-recruiting-page-design.md`. It is authoritative. Every factual claim in the content must trace to its Evidence Register (§ 9 of the spec). This plan does NOT re-derive evidence — it references the spec and embeds key facts inline per task.

### Voice rules (binding for every content task)

From spec § 8, non-negotiable:

- **Declarative sentences. Numbers over adjectives. Thesis before explanation.**
- **Forbidden words** (grep check in every task): `rockstar`, `10x`, `ninja`, `synergy`, `cutting-edge`, `world-class`, `AI-powered` (as a hype adjective — the noun phrase "AI-powered" is OK in product descriptions).
- **Admit failures where they strengthen claims.** Vague positivity reads as marketing; specific honesty reads as a colleague.
- **Commit references only:** use format `PR #N on YYYY-MM-DD` or `merged YYYY-MM-DD`. Never include commit hashes, commit message quotes, code diffs, or customer names.
- **Named people:** only `Okis` and `Tim Liu` are allowed — both are already publicly named in existing `roles/*.md` JDs. Every other contributor is aggregated: "a single engineer", "a team of four", "one dominant contributor".
- **Bilingual:** English primary. Traditional Chinese appears only inside the § 3.b pull-quote in `how-we-ship.md`, preserving the source language of the internal guide.
- **No emoji** in new content. (Existing `📧` in the README CTA is preserved.)

### Verification strategy (adapted from TDD for pure content)

This plan is not code, so there is no "failing test → implementation → passing test" cycle. The content equivalent, applied per section:

1. **Write the section** from the outline in spec § 4.x.
2. **Word count check:** `wc -w` on the section, must match the target from the spec within tolerance.
3. **Forbidden-word audit:** grep for the forbidden list above. Zero matches required.
4. **Fact check:** every specific number or date in the section must trace to spec § 9.
5. **Named-person audit:** grep for names; only `Okis` and `Tim Liu` allowed.
6. **Do not commit mid-work.** Everything commits atomically in Task 12. A half-written page that appears on careers.mlytics.com before it's ready would be worse than no page at all.

### What "already done" looks like on entry

Commit `506c9ce` (pushed to origin/main, `473a612..506c9ce`) already landed:
- `docs/superpowers/specs/2026-04-15-how-we-ship-recruiting-page-design.md` (the spec)
- `_config.yml` with `exclude: [docs/]`

Task 1 verifies this state before the plan proceeds.

---

## File structure

| Path | Status | Responsibility |
|---|---|---|
| `how-we-ship.md` | NEW at repo root | Long-form recruiting page (~2,170 words). Rendered by Jekyll as `careers.mlytics.com/how-we-ship`. |
| `README.md` | MODIFY | Insert new `## How we ship` section between `## About Mlytics` and `### By the numbers`; apply three in-place corrections in existing `### By the numbers` and `### How we work` subsections. |
| `roles/ai-powered-full-stack-engineer.md` | MODIFY | Append link-out line near the bottom, before the final `---` or "How to Apply" section (whichever exists). |
| `roles/ai-data-engineer.md` | MODIFY | Same as above. |
| `_config.yml` | ALREADY DONE (506c9ce) | `exclude: [docs/]` — Task 1 re-verifies. |
| `docs/superpowers/plans/2026-04-15-how-we-ship-recruiting-page.md` | NEW (this file) | The plan itself. Excluded from Jekyll by the `_config.yml` rule. |

---

## Task 1: Verify clean starting state

**Files:** none modified (pre-flight only)

- [ ] **Step 1: Confirm git is clean and on main at commit `506c9ce` or later**

Run from the repo root:
```bash
cd /Users/okis.chuang/Documents/mlytics-career
git status
git log --oneline -5
```

Expected: working tree clean, branch `main`, HEAD either `506c9ce Add design spec: how-we-ship recruiting page` or a descendant. If the tree is dirty or on another branch, **stop and report to user**. Do not proceed with dirty state.

- [ ] **Step 2: Re-verify `_config.yml` has `exclude: [docs/]`**

Run:
```bash
cat _config.yml
```

Expected output exactly:
```yaml
theme: jekyll-theme-minimal
exclude:
  - docs/
```

If the exclude is missing, apply it via `Edit` on `_config.yml` before proceeding. Failure to exclude will cause the spec and plan files to leak onto careers.mlytics.com.

- [ ] **Step 3: Verify spec file is present**

Run:
```bash
test -f docs/superpowers/specs/2026-04-15-how-we-ship-recruiting-page-design.md && echo OK
wc -l docs/superpowers/specs/2026-04-15-how-we-ship-recruiting-page-design.md
```

Expected: `OK` and around 420 lines. If missing, stop — implementation without the spec is not safe.

- [ ] **Step 4: Verify existing `README.md` still has the three phrases we are about to correct**

Run:
```bash
grep -n '4\.7M' README.md
grep -n '58.*live publisher integrations' README.md
grep -n '50-second animated short' README.md
```

Each command must return exactly one line. If any returns nothing, the target phrase has moved or been changed — stop and reconcile with the user before proceeding.

---

## Task 2: Create `how-we-ship.md` skeleton

**Files:**
- Create: `how-we-ship.md`

**Purpose:** Lock in the section structure first, so subsequent tasks can target individual headings with exact-match edits.

- [ ] **Step 1: Write the skeleton file**

Use the `Write` tool to create `how-we-ship.md` at the repo root with exactly this content:

```markdown
# How we ship: Becoming Product Builders with Business Thinking

## Two single-day ships in nine days

_PLACEHOLDER — replaced in Task 3._

## Why this is the default — and why it isn't everywhere yet

_PLACEHOLDER — replaced in Task 4._

## How Claude Code became our default in three weeks

_PLACEHOLDER — replaced in Task 5._

## The data backbone

_PLACEHOLDER — replaced in Task 6._

## Small teams, real ownership (the uncomfortable truth)

_PLACEHOLDER — replaced in Task 7._

## What to send us

_PLACEHOLDER — replaced in Task 8._

---

_All commit statistics on this page were gathered from internal git history on 2026-04-15. Numbers shift daily; directionally they shift up._
```

- [ ] **Step 2: Verify structure**

Run:
```bash
grep -c '^## ' how-we-ship.md
grep -c 'PLACEHOLDER' how-we-ship.md
```

Expected: `6` H2 headers and `6` placeholders.

- [ ] **Step 3: Do NOT commit.**

Content tasks (3–8) will be run atomically. Committing a page full of `PLACEHOLDER` text would serve broken content to live users if an error interrupted the session before Task 12.

---

## Task 3: Write § 1 — "Two single-day ships in nine days"

**Files:**
- Modify: `how-we-ship.md` (replace the section under `## Two single-day ships in nine days`)

**Target length:** 450 words (tolerance: 400–500)

**Reference:** Spec § 4.1 has the full outline. Evidence register entries are in spec §§ 9.1 (aigc-mvp) and 9.2 (agent-will-smith).

**Key facts to use (verbatim from the evidence register — do not paraphrase the numbers):**

*aigc-mvp video pipeline (§ 1.a, target ~230 words):*
- Opening line: **"On April 1, 2026, a team of four shipped a full AI video news pipeline in six hours."**
- Pipeline components in order: **Seedance image-to-video generator** → **FFmpeg subtitle burner** with logo overlay → **GCS upload** → per-publisher `video_news_enabled` opt-in flag → **widget-side video player**
- Commit reference: **PR #158**, merged **2026-04-01**
- Why multi-tenant makes this harder than a demo: every publisher has its own config, schema expectation, and CSS scope
- Failure admission (required — do not cut): "the first version of the FFmpeg subtitle burner had timing drift; the fix landed in a follow-up PR two days later"
- Closing beat: "This wasn't a demo. It went into production the same day."

*agent-will-smith brand integration (§ 1.b, target ~180 words):*
- Opening line: **"Nine days later, on April 9, one engineer paired with Claude Opus 4.6 shipped a two-agent brand-integration system in a single day."**
- Two new LangGraph agents: **`brand_matcher`** and **`brand_answer_generator`**
- Scope: **30 files**, approximately **1,680 lines of production Python**
- Merge reference: **PR #28** merged to main on **2026-04-13**
- Why LangGraph is the right abstraction here: brand placement needs `match → compose → validate → output` — stateful, ordered, composable
- Reference to the 6 agents now in the platform: product_recommendation, answer_generator, question_generator, intent_chat, brand_matcher, brand_answer_generator

*Closing beat (§ 1.c, target ~40 words):*
Exactly this, or a rewrite that preserves the meaning and tempo:
> "Different engineers. Different repos. Nine days apart. This is the tempo now."

- [ ] **Step 1: Draft the section**

Use the `Edit` tool to replace this block:
```
## Two single-day ships in nine days

_PLACEHOLDER — replaced in Task 3._
```
with the drafted section (H2 heading followed by the prose matching the outline above). Keep the H2 `## Two single-day ships in nine days` exactly as-is.

- [ ] **Step 2: Word count check**

Run:
```bash
awk '/^## Two single-day/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | wc -w
```

Expected: integer between **400 and 500** inclusive.

If too long: trim the component-description sentences in § 1.a, not the failure admission. If too short: add one more specific detail from the evidence register (e.g., the `video_news_enabled` flag name, the exact count of 6 agents, or a second concrete beat about multi-tenancy).

- [ ] **Step 3: Forbidden-word audit**

Run:
```bash
awk '/^## Two single-day/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -iE 'rockstar|10x|ninja|synergy|cutting-edge|world-class'
```

Expected: **zero output**. If anything matches, rewrite the offending sentence.

- [ ] **Step 4: Named-person audit**

Run:
```bash
awk '/^## Two single-day/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -oE '[A-Z][a-z]+ [A-Z][a-z]+' | sort -u
```

Expected: the output should contain **no human names** other than `Claude Opus` (model name, allowed) and `FFmpeg` (tool name, allowed, not actually a human name). If any human name other than `Tim Liu` or `Okis` appears, remove it and re-aggregate as "one engineer" / "a team of four" — only those two names are cleared for public use per spec § 8.

- [ ] **Step 5: Fact check**

Read the section once. For every specific number (6 hours, 1,680 lines, 30 files, 4 engineers, etc.), confirm the exact value exists in spec § 9. Any discrepancy → stop and ask user.

- [ ] **Step 6: Do NOT commit.**

---

## Task 4: Write § 2 — "Why this is the default — and why it isn't everywhere yet"

**Files:**
- Modify: `how-we-ship.md`

**Target length:** 450 words (tolerance: 400–500)

**Reference:** Spec § 4.2. Evidence from spec §§ 9.1, 9.2, 9.3.

**Key facts (verbatim):**

*§ 2.a headline (~80 words):*
- Core number: **"647 of our last 2,330 commits across our three newest production codebases list Claude as a co-author."**
- Implication phrase: **"just over a quarter of everything we shipped is AI-paired"** — measured across all contributors, not a pilot program. The ratio is the weighted-average aggregate of 647/2,330 ≈ 27.8%, phrased as "just over a quarter" to stay arithmetically honest and reader-verifiable.

*§ 2.b per-repo breakdown (~150 words):*
Table-like bullet list (or prose with numbers, writer's choice):
- `aigc-mvp`: **414 / 1,726 commits (24%)**, February 2025 → April 2026, ~4 engineers
- `agent-will-smith`: **135 / 298 commits (45%)**, November 2025 → April 2026, ~4 engineers
- `databricks`: **98 / 306 commits (32%)**, plus **91 additional `Generated with Claude Code` trailers**, August 2025 → April 2026, 6 engineers

Explanation paragraph (required): the percentages differ *and that is itself the interesting finding*. `aigc-mvp` carries Laravel scaffolding and DB migrations where humans are faster. `agent-will-smith` is dense with prompt engineering and LangGraph state design where AI pairing gives the largest lift. `databricks` is SQL models and data pipelines, in between. **"Different work, different ratios. The ratio tells you which parts of software development AI is actually reshaping right now."**

*§ 2.c brownfield honesty (~140 words) — this is the most important paragraph in the section, do not soften it:*

Include all of the following ideas (the exact wording can be refined):
- These percentages are from our three newest systems
- Older products still in migration: **the multi-CDN decision engine that's been routing 50M+ MAU since before Claude Code existed**, legacy internal dashboards, billing integrations dating back to the original SaaS
- Explicit framing: **"Just over a quarter isn't our ceiling. It's our leading edge."**
- Invitation: "If you join us now, part of your job is bringing the remaining three-quarters and the brownfield along with it."
- Closing beat: **"We're transforming a profitable, scaled company into an AI-first one. That's harder than building one from scratch, and more interesting."**

*§ 2.d meta-honesty (~80 words):*
- That share is a measurement, not a goal
- We didn't optimize for it
- "If it drops next quarter because the tooling changed, we'll write that up too."

- [ ] **Step 1: Draft the section** (replace placeholder via `Edit`)

- [ ] **Step 2: Word count check**

```bash
awk '/^## Why this is the default/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | wc -w
```
Expected: 400–500.

- [ ] **Step 3: Forbidden-word audit**

```bash
awk '/^## Why this is the default/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -iE 'rockstar|10x|ninja|synergy|cutting-edge|world-class'
```
Expected: zero output.

- [ ] **Step 4: Math check**

Run:
```bash
awk '/^## Why this is the default/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -oE '647|2,?330|414|1,?726|135|298|98|306|91|24%|45%|32%'
```

Expected: every listed number should appear at least once (with or without the comma separator for 2,330 and 1,726). If any number is missing, you dropped a fact — add it back.

- [ ] **Step 5: Brownfield paragraph existence check**

Run:
```bash
grep -iE 'brownfield|legacy|leading edge|ceiling' how-we-ship.md
```

Expected: at least one match per term within the § 2 range. This is a lazy-but-effective check that you didn't accidentally soften or omit the honesty paragraph.

- [ ] **Step 6: Do NOT commit.**

---

## Task 5: Write § 3 — "How Claude Code became our default in three weeks"

**Files:**
- Modify: `how-we-ship.md`

**Target length:** 550 words (tolerance: 500–600) — this is the **longest** and most content-heavy section.

**Reference:** Spec § 4.3. Source material is the internal guide referenced in spec § 9.4.

**Key elements (must all appear):**

*§ 3.a opening (~80 words):*
- Establish: "In February 2026, our Head of Technology & Growth published an internal guide to the product team."
- Guide title: ***Claude Code × Product Development: Becoming Product Builders with Business Thinking***
- Framing: **"It was not a tools tutorial. It was a thesis about what the team should become."**

*§ 3.b bilingual pull-quote (~80 words):*

Reproduce this block exactly in the rendered Markdown. The Traditional Chinese original **must** appear first, followed by the English translation, followed by the attribution:

```markdown
> 「我們不是在用 AI 寫更多程式，我們是在用 AI 解決更多商業問題。每個人都是 Product Builder，不只是工程師。」
>
> "We aren't using AI to write more code. We're using AI to solve more business problems. Everyone on this team is a Product Builder, not just an engineer."
>
> — Internal team guide, February 2026
```

After the pull-quote, one sentence explaining why the Chinese is retained:
> "The Traditional Chinese original is preserved here because it is the source language of the guide — and because the existence of an internal-language document is itself a signal that this is a real artifact, not marketing copy back-translated for flavor."

*§ 3.c three-week rollout (~200 words):*

Three paragraphs, one per phase. Include each of these specifics:

- **Week 1 — Infrastructure:** Claude Code installed team-wide, `CLAUDE.md` committed to git in every repo as shared team knowledge, `.claude/settings.json` shared across the team, first batch of slash commands (`/commit-push-pr`, `/deploy-staging`, `/run-tests`) added, `.mcp.json` configs for BigQuery, Slack, and Sentry deployed.
- **Week 2 — Workflow:** every non-trivial task starts in Plan mode before switching to auto-accept-edits; `PostToolUse` hook auto-formats code to eliminate CI formatting churn; two core subagents (`code-simplifier`, `verify-app`) committed to git; PR reviews tag `@.claude` to write learnings back into `CLAUDE.md`.
- **Week 3 onward — Iteration:** weekly `CLAUDE.md` review, monthly efficiency audit, internal sharing sessions on individual discoveries.

*§ 3.d before/after comparison table (~100 words):*

Reproduce exactly:

```markdown
| Before | After |
|---|---|
| Review every line of diff | Test final behavior |
| File-level guidance | Requirement-level guidance |
| Understand all implementation details | Understand interface contracts |
| Humans as code reviewers | Humans as behavior verifiers |
```

Follow with 2–3 sentences of interpretation, including this beat:
> "This sounds small on paper. In practice, it means a senior engineer's time is spent on what the system does, not on whether the semicolons are in the right places."

*§ 3.e four team commitments (~70 words):*

Exactly four, in this order, each as a bold one-liner followed by a short explanation:

```markdown
- **Plan First, Code Second.** Tasks that skip Plan mode don't ship.
- **Verify, Don't Review.** Test behavior, not code.
- **Every Mistake Becomes a Rule.** Errors get written back into CLAUDE.md so the next engineer — human or AI — doesn't repeat them.
- **Ship and Iterate.** Delivery beats perfection; iteration beats planning.
```

*§ 3.f closing causal claim (~20 words):*

> "We published the guide in February. By April, our commit patterns had diverged from anything we'd seen before."

- [ ] **Step 1: Draft the section** (replace placeholder via `Edit`)

- [ ] **Step 2: Word count check**

```bash
awk '/^## How Claude Code became/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | wc -w
```
Expected: 500–600.

- [ ] **Step 3: Forbidden-word audit**

```bash
awk '/^## How Claude Code became/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -iE 'rockstar|10x|ninja|synergy|cutting-edge|world-class'
```
Expected: zero output.

- [ ] **Step 4: Bilingual block presence check**

```bash
grep -F '我們不是在用 AI 寫更多程式' how-we-ship.md
grep -F 'Product Builder, not just an engineer' how-we-ship.md
```

Both must return exactly one match.

- [ ] **Step 5: Team commitments count check**

```bash
awk '/^## How Claude Code became/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -cE '^\- \*\*(Plan First|Verify|Every Mistake|Ship and Iterate)'
```

Expected: `4`.

- [ ] **Step 6: Before/after table check**

```bash
awk '/^## How Claude Code became/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -c '^|'
```

Expected: `6` (header row + separator row + 4 data rows).

- [ ] **Step 7: Do NOT commit.**

---

## Task 6: Write § 4 — "The data backbone"

**Files:**
- Modify: `how-we-ship.md`

**Target length:** 320 words (tolerance: 280–360)

**Reference:** Spec § 4.4. Evidence from spec § 9.3.

**Key facts (must appear verbatim):**

- First commit by `Tim Liu` on **August 27, 2025**
- **224 days**, **306 commits**
- Four domains: **`aigc`**, **`cdn-analytics`**, **`customer-core`**, **`decisive`**
- **9 Lakeflow pipelines**, **21 scheduled jobs**
- **37 Silver SQL models + 28 Gold SQL models**
- Unity Catalog via **Databricks Asset Bundles** with `schemas.yaml` as resource-as-code (not hand-written DDL)
- MLflow **Prompt Registry** for versioned prompts (versioning prompts, not just versioning code)
- Databricks Vector Search via **`DeltaSyncVectorIndexSpecRequest`**, syncing three Gold content tables embedded with **`gemini-embedding-001`** through a custom **`GeminiEmbeddingProvider`**
- CDN coverage: **8 upstream providers** (Akamai, Alibaba, Baishan, CDNetworks, Chunghwa, CloudFront, Tencent, VNCDN) — list them all, it's specific enough to be credible
- The "load-bearing" argument: the Intent Refinery's monetization path depends on a medallion pipeline that turns raw clickstream events into ad-auction-ready features. "The data work isn't supporting the AI product — it's what makes the AI product monetizable."
- Bridge sentence to the AI Data Engineer JD: **"If this reads like infrastructure work you want to own end-to-end, our AI Data Engineer role is the one."**

**Tim Liu may be named** in this section because he is already publicly named in `roles/ai-data-engineer.md`.

- [ ] **Step 1: Draft the section** (replace placeholder via `Edit`)

- [ ] **Step 2: Word count check**

```bash
awk '/^## The data backbone/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | wc -w
```
Expected: 280–360.

- [ ] **Step 3: Forbidden-word audit**

```bash
awk '/^## The data backbone/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -iE 'rockstar|10x|ninja|synergy|cutting-edge|world-class'
```
Expected: zero output.

- [ ] **Step 4: Technical-specificity check**

```bash
awk '/^## The data backbone/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -oE 'Unity Catalog|MLflow|Vector Search|DeltaSyncVectorIndexSpecRequest|gemini-embedding-001|Lakeflow|Databricks Asset Bundles?|schemas\.yaml'
```

Expected: at least 6 distinct technical terms matched. These are the signals that a data engineer candidate uses to decide "this is a real stack, not marketing".

- [ ] **Step 5: Do NOT commit.**

---

## Task 7: Write § 5 — "Small teams, real ownership (the uncomfortable truth)"

**Files:**
- Modify: `how-we-ship.md`

**Target length:** 250 words (tolerance: 220–280)

**Reference:** Spec § 4.5.

**Key elements:**

- Team sizes stated flatly: `aigc-mvp` ~4 engineers, `agent-will-smith` ~4, `databricks` 6
- Memorable beat: **"Every production system at Mlytics fits around one table."**
- Why we're hiring: **"not because we're drowning, because we keep finding more things to build than the current team can pick up. Speed creates its own problem."**
- Who thrives (3 bullets, required):
  - People who want end-to-end ownership (API design → production monitoring, no handoffs)
  - People who have already made AI pair programming part of their daily loop
  - People who can learn from a tech lead at `Tim`'s or a peer's level and want to operate next to them, not under a skip-level chain
- Who doesn't (3 bullets, required — do not soften or omit):
  - Specialists who want a narrow lane
  - People who want big-team process (RFCs, multi-stage approvals, async-only communication)
  - Engineers who are skeptical of AI pair programming as default
- Closing beat: **"We'd rather tell you this now than at your three-month review."**

The "who doesn't thrive here" bullets are the entire point of this section — cutting them destroys the section's credibility function.

- [ ] **Step 1: Draft the section** (replace placeholder via `Edit`)

- [ ] **Step 2: Word count check**

```bash
awk '/^## Small teams/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | wc -w
```
Expected: 220–280.

- [ ] **Step 3: Forbidden-word audit**

```bash
awk '/^## Small teams/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -iE 'rockstar|10x|ninja|synergy|cutting-edge|world-class'
```
Expected: zero output.

- [ ] **Step 4: Anti-fit bullets existence check**

```bash
awk '/^## Small teams/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | grep -iE 'narrow lane|RFC|skeptical'
```

Expected: **all three phrases** (or clearly-equivalent rephrasings) must appear. If you softened the anti-fit section during drafting, restore it.

- [ ] **Step 5: Closing beat check**

```bash
grep -F 'three-month review' how-we-ship.md
```

Expected: one match. This closing line is the section's emotional payload; don't silently drop it.

- [ ] **Step 6: Do NOT commit.**

---

## Task 8: Write § 6 — "What to send us"

**Files:**
- Modify: `how-we-ship.md`

**Target length:** 150 words (tolerance: 120–180)

**Reference:** Spec § 4.6.

**Key elements:**

- Not a resume. Something that shows how you think.
- Accepted: a side project, a PR you're proud of, a technical write-up, a message explaining why this caught your attention.
- **Email: `careers@mlytics.com`**
- Link to both JDs using relative paths:
  - [AI-Powered Full Stack Engineer](./roles/ai-powered-full-stack-engineer.md)
  - [AI Data Engineer](./roles/ai-data-engineer.md)

Voice here should echo the existing `README.md` CTA to avoid sounding like a different page. You can quote the "We care about what you've built more than where you've worked." line verbatim for coherence.

- [ ] **Step 1: Draft the section** (replace placeholder via `Edit`)

- [ ] **Step 2: Word count check**

```bash
awk '/^## What to send us/{flag=1; next} /^## /{flag=0} flag' how-we-ship.md | wc -w
```
Expected: 120–180.

- [ ] **Step 3: Link presence check**

```bash
grep -F '(./roles/ai-powered-full-stack-engineer.md)' how-we-ship.md
grep -F '(./roles/ai-data-engineer.md)' how-we-ship.md
grep -F 'careers@mlytics.com' how-we-ship.md
```

All three must return exactly one match.

- [ ] **Step 4: Do NOT commit.**

---

## Task 9: Full-page audit of `how-we-ship.md`

**Files:** none modified (read-only verification)

**Purpose:** catch anything that slipped through per-section checks.

- [ ] **Step 1: Total word count**

```bash
wc -w how-we-ship.md
```

Expected: **1,800–2,300 words** per the spec's acceptance criteria.

If outside range, trim the longest section or expand the thinnest. Refer back to § 4.x targets in the spec.

- [ ] **Step 2: No PLACEHOLDER strings remain**

```bash
grep -c PLACEHOLDER how-we-ship.md
```

Expected: `0`. If anything is still a placeholder, that section was skipped — go back and finish it.

- [ ] **Step 3: Full-file forbidden-word audit**

```bash
grep -iE 'rockstar|10x|ninja|synergy|cutting-edge|world-class' how-we-ship.md
```

Expected: zero output.

- [ ] **Step 4: Full-file named-person audit**

```bash
grep -oE '\b[A-Z][a-z]+ [A-Z][a-z]+\b' how-we-ship.md | sort -u
```

Expected output contains **only** these allowed multi-word capitalized phrases:
- `Tim Liu` (allowed: public in JD)
- `Claude Opus` / `Claude Sonnet` (model name)
- `Vector Search` (Databricks feature)
- `Prompt Registry` (Databricks feature)
- `Unity Catalog` (Databricks feature)
- `Asset Bundles` (Databricks feature)
- `Plan First`, `Verify Don't`, `Every Mistake`, `Ship and` (team commitment fragments)
- `Intent Refinery` (Mlytics product name, public)
- `Product Builder`, `Product Builders` (guide concept, public)

If any OTHER human name appears, **stop and remove it**. Aggregate as "an engineer" or "the team". Only `Tim Liu` and `Okis` are cleared for public naming per spec § 8.

- [ ] **Step 4b: Jekyll front-matter sanity check**

The file does NOT have YAML front matter. For `jekyll-theme-minimal`, this renders with the default layout and an H1-derived page title, which is correct for our use. Do NOT add front matter unless the live-site check in Task 13 reveals a rendering problem.

- [ ] **Step 5: Do NOT commit yet.** All content changes commit together in Task 12.

---

## Task 10: Modify `README.md`

**Files:**
- Modify: `README.md`

**Reference:** Spec § 5. Three discrete edits (A, B, C).

### 10.A Insert new `## How we ship` section

**Placement:** Between the existing `## About Mlytics` section and the existing `### By the numbers` subsection.

- [ ] **Step 1: Verify insertion point exists**

```bash
grep -n '^## About Mlytics' README.md
grep -n '^### By the numbers' README.md
```

Both must return exactly one line. Note the line numbers — insertion happens between them.

- [ ] **Step 2: Insert the new section**

Use `Edit` with `replace_all=false` to replace:

```
### By the numbers
```

with:

```
## How we ship

In early April 2026, a team of four at Mlytics shipped a full AI video news pipeline in six hours — Seedance image-to-video generation, FFmpeg subtitle burn-in, GCS delivery, per-publisher opt-in, and a widget-side player — all merged in a single pull request on April 1. Nine days later, one engineer paired with Claude Opus 4.6 shipped a two-agent brand-integration system in a day: 1,680 lines of production Python, two new LangGraph agents, one pull request.

Neither was a sprint. Across our three newest production codebases, **647 of our last 2,330 commits list Claude as a co-author**. We're in the middle of turning AI-first pair programming from a leading-edge practice into the default across the whole company. Some of our older systems — the legacy CDN decision engine, internal dashboards — are still catching up. This is what the transformation looks like from the inside, not the press release.

In February 2026 we wrote an internal guide on how we want to build. This is the story of what actually happened when we did:

**[How we ship → Becoming Product Builders with Business Thinking](./how-we-ship.md)**

### By the numbers
```

- [ ] **Step 3: Verify insertion worked**

```bash
grep -c '^## How we ship' README.md
grep -c '^### By the numbers' README.md
```

Each must return exactly `1`. If `## How we ship` returns 0, the Edit failed — investigate the `old_string` match. If `### By the numbers` returns 0 or 2, the Edit corrupted the file — revert via `git checkout README.md` and retry.

### 10.B Three corrections in `### By the numbers`

- [ ] **Step 4: Correction 1 — replace "4.7M" line**

Use `Edit` to replace:
```
- **4.7M** weekly active users on the AIGC intent product
```
with:
```
- **Over 100K** weekly active users on our AIGC intent product
```

- [ ] **Step 5: Correction 2 — replace "58" line**

Use `Edit` to replace:
```
- **58** live publisher integrations (finance, lifestyle, sports)
```
with:
```
- **22** live publisher integrations (finance, lifestyle, sports)
```

- [ ] **Step 6: Leave "2,500x" line alone**

Explicitly do NOT touch the `2,500x efficiency gain` bullet. Per the spec, this is preserved as an intentional hypothetical comparison figure with user authorization.

- [ ] **Step 7: Verify corrections stuck**

```bash
grep '4\.7M' README.md
grep '58.*live publisher' README.md
grep '100K.*weekly active' README.md
grep '22.*live publisher' README.md
```

First two commands must return **nothing**. Last two must return one line each.

### 10.C Replace the "50-second animated short" sentence in `### How we work`

- [ ] **Step 8: Apply the replacement**

Use `Edit` to replace this exact sentence:
```
We produced a 50-second animated short from a 475-line transcript using 46 AI API calls in 45 minutes.
```
with:
```
We shipped a full AI video news pipeline — image-to-video generation, automated subtitle burn-in, per-publisher opt-in — in under six hours on April 1, 2026. Details in [How we ship →](./how-we-ship.md).
```

- [ ] **Step 9: Verify the replacement**

```bash
grep '50-second animated' README.md
grep 'AI video news pipeline' README.md
```

First must return nothing. Second must return one line.

- [ ] **Step 10: Do NOT commit yet.**

---

## Task 11: Append link-out to both JD files

**Files:**
- Modify: `roles/ai-powered-full-stack-engineer.md`
- Modify: `roles/ai-data-engineer.md`

- [ ] **Step 1: Identify the insertion point in each JD**

Run for each file:
```bash
tail -20 roles/ai-powered-full-stack-engineer.md
tail -20 roles/ai-data-engineer.md
```

Look for the final `---` separator before the "How to Apply" / CTA section, or the very end of the file if no such separator exists.

- [ ] **Step 2: Append the link-out block to `ai-powered-full-stack-engineer.md`**

Use `Edit` to insert the following **immediately before** the final `---` (or append to file end if no final `---` exists):

```markdown
---

**Want to see how we actually build this?** → [How we ship: Becoming Product Builders with Business Thinking](../how-we-ship.md)
```

Note the relative path `../how-we-ship.md` — the JD is one directory deeper (in `roles/`), so the link goes up one level.

- [ ] **Step 3: Append the same link-out block to `ai-data-engineer.md`**

Same content, same placement logic. The identical wording between the two JDs is intentional.

- [ ] **Step 4: Verify both files have the link**

```bash
grep -l 'how-we-ship.md' roles/
```

Expected: both JD files listed. If only one, the other wasn't edited.

- [ ] **Step 5: Verify the relative paths resolve**

```bash
test -f how-we-ship.md && echo OK
```

Expected: `OK`. This confirms that `../how-we-ship.md` from `roles/*.md` resolves to an existing file at the repo root.

- [ ] **Step 6: Do NOT commit yet.**

---

## Task 12: Atomic commit of all content changes

**Files:** none further modified — this task is git-only

- [ ] **Step 1: Full `git status` review**

```bash
git status
git diff --stat
```

Expected `git status` output:
```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  modified:   README.md
  modified:   roles/ai-data-engineer.md
  modified:   roles/ai-powered-full-stack-engineer.md

Untracked files:
  how-we-ship.md
```

Four file changes. Nothing in `docs/`. If anything else is showing, reconcile before committing.

- [ ] **Step 2: Stage exactly the expected four files**

```bash
git add how-we-ship.md README.md roles/ai-powered-full-stack-engineer.md roles/ai-data-engineer.md
git status
```

Verify all four are staged, nothing else. Intentionally NOT using `git add -A` to avoid picking up stray files.

- [ ] **Step 3: Commit**

```bash
git commit -m "$(cat <<'EOF'
Publish how-we-ship recruiting page and correct README claims

Adds /how-we-ship.md — a long-form page documenting how the team builds
with Claude Code as default, sourced from the February 2026 internal
team guide and three production repos (aigc-mvp, agent-will-smith,
databricks). Replaces three inaccurate claims on the README landing
page with code-verifiable alternatives and links both JDs to the new
page.

Implements the design spec at
docs/superpowers/specs/2026-04-15-how-we-ship-recruiting-page-design.md.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

- [ ] **Step 4: Verify commit landed locally**

```bash
git log --oneline -3
git show --stat HEAD
```

Expected: new commit at HEAD, showing exactly 4 files changed — `how-we-ship.md` (new, ~2,170 words), `README.md` (modified), both `roles/*.md` (modified).

---

## Task 13: Push and verify the live site

**Files:** none modified

- [ ] **Step 1: Push**

```bash
git push origin main
```

Expected: clean fast-forward push (no conflicts). If there's a conflict, do NOT force-push — investigate via `git fetch && git log --oneline origin/main..HEAD HEAD..origin/main` and reconcile.

- [ ] **Step 2: Wait for GitHub Pages rebuild**

Pages typically rebuilds within 60 seconds. Poll the build state until it completes:

```bash
sleep 60
gh api repos/mlytics/mlytics-careers/pages/builds/latest --jq '{status, commit, updated_at, error: .error.message}'
```

Expected: `status: "built"`, `commit` matches the commit from Task 12, `error` is null. If it's still `"building"`, wait another 30 seconds and retry. If `error` is non-null, stop — the Jekyll build failed.

- [ ] **Step 3: Fetch the live landing page and confirm new hook section is present**

```bash
curl -sL https://careers.mlytics.com/ | grep -F 'How we ship' | head -3
curl -sL https://careers.mlytics.com/ | grep -F '647 of our last 2,330'
curl -sL https://careers.mlytics.com/ | grep -F '4.7M'
```

Expected:
- First: at least one match (the new section heading + the CTA link text)
- Second: exactly one match (the hook paragraph's key number)
- Third: **zero matches** — if `4.7M` still appears, the README correction was not applied or not pushed

- [ ] **Step 4: Fetch the new long-form page**

```bash
curl -sI https://careers.mlytics.com/how-we-ship | head -3
curl -sL https://careers.mlytics.com/how-we-ship | grep -F 'Becoming Product Builders' | head -1
curl -sL https://careers.mlytics.com/how-we-ship | grep -F '我們不是在用 AI 寫更多程式'
```

Expected:
- First: `HTTP/2 200`
- Second: one match for the page title
- Third: one match confirming the bilingual pull-quote survived the Jekyll render (UTF-8 handling sometimes breaks for legacy themes — if zero matches, check the raw page source for encoding issues)

- [ ] **Step 5: Confirm `docs/` is still NOT publicly served**

```bash
curl -sI https://careers.mlytics.com/docs/superpowers/specs/2026-04-15-how-we-ship-recruiting-page-design | head -3
```

Expected: `HTTP/2 404`. The `_config.yml` `exclude: [docs/]` rule must still be holding.

- [ ] **Step 6: Confirm the two JD pages link to the new page**

```bash
curl -sL https://careers.mlytics.com/roles/ai-powered-full-stack-engineer | grep -F 'how-we-ship' | head -1
curl -sL https://careers.mlytics.com/roles/ai-data-engineer | grep -F 'how-we-ship' | head -1
```

Both must return one match each.

- [ ] **Step 7: Visual sanity check (manual)**

Open `https://careers.mlytics.com/how-we-ship` in a browser. Check:
- Page title is rendered (not a raw H1 string)
- The bilingual pull-quote looks correct (Chinese and English both display, no `?` or mojibake)
- The before/after table renders as a table, not as raw pipe characters
- All links are clickable
- No obvious layout breakage from the minimal theme

If anything looks broken, the most likely fix is adding YAML front matter to `how-we-ship.md`:

```markdown
---
layout: default
title: How we ship — Mlytics Careers
---

# How we ship: Becoming Product Builders with Business Thinking
```

This is a fallback only — do not apply preemptively.

- [ ] **Step 8: Report completion**

Report to the user: commit hash, live URL, any unexpected findings from the live-site check.

---

## Plan self-review checklist

Before dispatching this plan, the plan author runs these checks:

- [ ] Every section in spec § 4.1–4.6 has a corresponding Task 3–8.
- [ ] Every correction in spec § 5.1–5.3 is covered by Task 10 steps.
- [ ] The `_config.yml` exclusion (spec § 7) is verified in Task 1 (not re-applied, since it's already committed in 506c9ce).
- [ ] JD link-outs (spec § 6) are covered by Task 11.
- [ ] Voice rules (spec § 8) are referenced in the executor context block and enforced per task via forbidden-word grep.
- [ ] Evidence register (spec § 9) is referenced in every content task's "Key facts" block.
- [ ] Implementation order (spec § 10) matches this plan's task order.
- [ ] All 8 acceptance criteria (spec § 11) are verified either during content tasks (§§ 1–4, 9) or in Task 13 (§§ 5–8).

## Spec coverage gaps

None identified. Every requirement in the spec has at least one corresponding task.

## Risks carried forward from the spec

Risks from spec § 12 remain owned by the executor to monitor during and after execution:

- **Numbers drift** — mitigated by page footer dating the snapshot.
- **Internal document quoted publicly** — approved by user 2026-04-15.
- **"legacy CDN decision engine" framing** — approved by user 2026-04-15.
- **"2,500x" hypothetical preserved** — approved by user 2026-04-15.
- **Jekyll rendering surprise** — Task 13 Step 7 has a fallback front-matter fix documented.
