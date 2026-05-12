# Careers Site Rewrite Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rewrite careers.mlytics.com with updated company positioning (AI Answer Engine + Intent Refinery), add Candidate FAQ, and create a full Traditional Chinese mirror under `zh-TW/`.

**Architecture:** Content-only Jekyll site rendered by GitHub Pages. No build step, no tests, no dependencies. All work is Markdown editing. The site uses `jekyll-theme-minimal` which renders `README.md` as the root page.

**Tech Stack:** Markdown, GitHub Pages, Jekyll (jekyll-theme-minimal)

**Spec:** `docs/superpowers/specs/2026-05-12-careers-site-rewrite-design.md`

**Source material:** `~/Documents/dev/mlytics-cortex/mlytics-talent-narrative.md`

---

## File map

| File | Action | Description |
|------|--------|-------------|
| `README.md` | Rewrite | New tagline, About, engineering culture, updated numbers |
| `faq.md` | Create | 4-question Candidate FAQ |
| `roles/ai-data-engineer.md` | Edit | Replace lines 10–22 (company intro) with compact "Mlytics in 30 seconds" |
| `roles/ai-powered-full-stack-engineer.md` | Edit | Replace lines 10–29 (company intro) with compact "Mlytics in 30 seconds" |
| `zh-TW/README.md` | Create | Traditional Chinese mirror of README |
| `zh-TW/faq.md` | Create | Traditional Chinese mirror of FAQ |
| `zh-TW/roles/ai-data-engineer.md` | Create | Chinese company intro + English role content |
| `zh-TW/roles/ai-powered-full-stack-engineer.md` | Create | Chinese company intro + English role content |

---

### Task 1: Rewrite README.md

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Rewrite README.md with full new content**

Replace the entire file with:

```markdown
[繁體中文版 →](./zh-TW/README.md)

# Mlytics Careers

> **We turn content into commerce.**
> The AI Answer Engine for the intent economy.

We're building the Intent Refinery — a platform that captures reader intent at the point of content consumption, matches it to brands, and converts it into measurable commercial outcomes. Not impressions. Not clicks. Declared purchase intent, priced on CPL.

---

## About Mlytics

Mlytics is an AI-powered Answer Engine built for the intent economy.

We help media publishers turn reader intent into measurable commercial outcomes — replacing fading CPM ad revenue with high-quality CPL revenue. We help brands stop buying impressions and start buying confirmed intent.

Our 5-layer Intent Refinery — Content → Decisive Engine → AI Q&A → Full Conversation → Lead Pilot — is live with 15+ of Taiwan's top media properties and 4M+ weekly active users.

We started as a multi-CDN company. That infrastructure — <50ms routing, multi-vendor failover — is now the substrate underneath. Same engineering rigor, much bigger ambition.

### By the numbers

- **4M+** weekly active users across the platform
- **15+** live publisher integrations (Taiwan's top media properties)
- **2,500x** efficiency gain: $0.10 AI-generated content vs. $250 human-written

---

## What we work on

- **Real distributed systems at meaningful scale.** 4M+ WAU, <50ms p95, multi-vendor failover (Cloudflare / Akamai / Fastly), real CDN economics.
- **AI agents that actually do work.** Intent classification, RAG over publisher-specific knowledge bases, multi-step agent runtime. Not chatbot demos.
- **Two-sided marketplace mechanics.** Publisher supply meets brand demand through real-time intent matching. CPL pricing. Editorial guardrails. Real money flowing.
- **Product engineering, not feature engineering.** Every engineer participates in scoping. Every slice has a paying customer gate. If it doesn't ship to a real user, it didn't ship.

---

## Open Positions

| Role | Location | Team |
|------|----------|------|
| [AI-Powered Full Stack Engineer](./roles/ai-powered-full-stack-engineer.md) | Singapore / Taipei | Product |
| [AI Data Engineer](./roles/ai-data-engineer.md) | Singapore / Taipei | Data & Innovation |

---

## How we ship

In early April 2026, a team of four shipped a full AI video news pipeline in six hours. Nine days later, one engineer paired with Claude Opus shipped a two-agent brand-integration system in a day. Across our three newest production codebases, over a quarter of all commits list Claude as a co-author. This is what AI-first engineering looks like from the inside, not the press release.

**[How we ship → Becoming Product Builders with Business Thinking](./how-we-ship.md)**

---

## How to Apply

Send us something that shows how you think — a side project, a technical write-up, a PR you're proud of, or a message explaining why this caught your attention.

📧 **[careers@mlytics.com](mailto:careers@mlytics.com)**

We care about what you've built more than where you've worked.

Questions? → [Candidate FAQ](./faq.md)
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "Rewrite careers landing page with AI Answer Engine positioning"
```

---

### Task 2: Create faq.md

**Files:**
- Create: `faq.md`

- [ ] **Step 1: Create faq.md**

```markdown
[← Back to careers home](./README.md)

# Candidate FAQ

---

### What does Mlytics actually do, in one sentence?

Mlytics is an AI Answer Engine. Media publishers have traffic but monetization is getting harder; brands have budgets but advertising is getting more wasteful. We use AI to extract purchase intent from reader traffic, match it to brands, and help both sides get better outcomes.

---

### LinkedIn still says multi-CDN — is that outdated?

Yes. We're updating all platforms this year. Multi-CDN is our history — we started there, built it well, and that technology became the infrastructure layer underneath our new products. But today Mlytics is an AI Answer Engine, not a CDN company.

---

### You've pivoted once. Will you pivot again?

No — but this is worth unpacking. Going from multi-CDN to AI Answer Engine wasn't a pivot, it was an evolution. The multi-CDN business still exists, still sells, still serves customers — it became the substrate for our upper-layer products. We widened the product line, we didn't swap it. The AI Answer Engine direction — intent to commerce — is not changing.

---

### Are you open to remote work?

Our product and engineering teams are primarily based in Taiwan and collaborate closely in-person, but remote arrangements are possible — we're open to discussing what works. Go-to-market roles (Sales, Partnerships, Customer Success) depend on the market we're hiring for; specifics are best discussed during the interview process.

---

📧 **[careers@mlytics.com](mailto:careers@mlytics.com)** · [← Back to careers home](./README.md)
```

- [ ] **Step 2: Commit**

```bash
git add faq.md
git commit -m "Add candidate FAQ page"
```

---

### Task 3: Update JD company intro sections

**Files:**
- Modify: `roles/ai-data-engineer.md` (replace lines 10–22)
- Modify: `roles/ai-powered-full-stack-engineer.md` (replace lines 10–29)

Both JDs get the same replacement. The old "## The intent refinery" section is replaced with a compact "## Mlytics in 30 seconds" section. Everything from "## The role" onward is unchanged.

- [ ] **Step 1: Edit `roles/ai-data-engineer.md`**

Replace the old_string (the entire "## The intent refinery" section):

```
## The intent refinery

We built an engine that makes real-time routing decisions across the world's content delivery infrastructure — 50 million monthly active users, every day. That engine is profitable, proven at scale, and gave us something most startups never get: real production traffic and the time to figure out what to build next.

We figured it out. **The engine doesn't change. The packet does.**

Our CDN Decision Engine used to route content delivery packets. Now we're routing something far more valuable: **user intent.** When someone reads a financial article and asks "should I invest in TSMC right now?" — that question carries a purchase intent signal worth 100x more than a pageview impression. We capture that signal in real time, classify it, score it, and match it to brands willing to pay for it.

We call this **The Intent Refinery** — raw attention goes in, commercially actionable intent comes out. Today we have **4.7 million weekly active users** generating intent signals across **58 live publisher integrations** in finance, lifestyle, and sports. Our clickstream SDK is already capturing behavioral events — scroll depth, active reading time, Q&A interactions, cross-page navigation — and landing them in S3.

**Here's the problem: the raw data is flowing, but the refinery isn't built yet.**

The gap between "events in a bucket" and "a brand paying $1.50 CPC for a verified high-intent user" is a data pipeline, a scoring model, and a matching engine. That gap is your job.
```

With new_string:

```
## Mlytics in 30 seconds

Mlytics is an AI Answer Engine. We help media publishers turn reader intent into commercial outcomes — replacing fading CPM revenue with high-quality CPL revenue. Our Intent Refinery is live with 15+ of Taiwan's top media properties, serving 4M+ weekly active users.

We started as a multi-CDN company. That infrastructure — <50ms routing, multi-vendor failover — is now the substrate underneath.

[More about Mlytics →](../README.md)
```

- [ ] **Step 2: Edit `roles/ai-powered-full-stack-engineer.md`**

Replace the old_string (the entire "## The intent refinery" section):

```
## The intent refinery

We built an engine that makes real-time routing decisions across the world's content delivery infrastructure — 50 million monthly active users, every day. That engine is profitable, proven at scale, and gave us something most startups never get: real production traffic and the time to figure out what to build next.

We figured it out. **The engine doesn't change. The packet does.**

Our CDN Decision Engine used to route content delivery packets. Now we're routing something far more valuable: **user intent.** When someone reads a financial article and asks "should I invest in TSMC right now?" — that question carries a purchase intent signal worth 100x more than a pageview impression. We capture that signal in real time, classify it, score it, and match it to brands willing to pay for it.

We call this **The Intent Refinery** — raw attention goes in, commercially actionable intent comes out. Four layers, each independently monetizable:

→ **Decisive Engine** — routing & observability ($1K/mo)
→ **AI Q&A Widget** — turns every article into an intent capture point ($5K/mo)
→ **Full Conversation** — captures strong intent through multi-turn dialog (CPL pricing)
→ **Lead Pilot** — filters and converts (performance pricing)

This isn't a slide deck. We have **4.7 million weekly active users** on the platform, **58 live publisher integrations** across finance, lifestyle, and sports verticals, and a clickstream SDK capturing behavioral signals at scale. One AI-generated article costs $0.10 vs. $250 for a human writer — a 2,500x efficiency gain. And we recently produced a 50-second animated short from a 475-line meeting transcript using 46 AI API calls in 45 minutes — a pipeline that would traditionally require six specialists and three weeks.

**The moat isn't any single AI model — everyone can access those. The moat is who can chain the entire pipeline end-to-end, on top of a real-time intent data flywheel.**

We're hiring the engineers who will build that chain.
```

With the same new_string as Step 1:

```
## Mlytics in 30 seconds

Mlytics is an AI Answer Engine. We help media publishers turn reader intent into commercial outcomes — replacing fading CPM revenue with high-quality CPL revenue. Our Intent Refinery is live with 15+ of Taiwan's top media properties, serving 4M+ weekly active users.

We started as a multi-CDN company. That infrastructure — <50ms routing, multi-vendor failover — is now the substrate underneath.

[More about Mlytics →](../README.md)
```

- [ ] **Step 3: Commit**

```bash
git add roles/ai-data-engineer.md roles/ai-powered-full-stack-engineer.md
git commit -m "Replace JD company intro sections with compact Mlytics summary"
```

---

### Task 4: Create zh-TW/README.md

**Files:**
- Create: `zh-TW/README.md`

- [ ] **Step 1: Create directory**

```bash
mkdir -p zh-TW/roles
```

- [ ] **Step 2: Create zh-TW/README.md**

```markdown
[English version →](../README.md)

# Mlytics 職缺

> **把內容變成商業交易。**
> 為意圖經濟打造的 AI Answer Engine。

我們正在打造 Intent Refinery — 在內容消費的當下捕捉讀者意圖、媒合品牌、轉化為可衡量的商業成果。不是曝光數。不是點擊數。是讀者主動表達的購買意圖，用 CPL 計價。

---

## 關於 Mlytics

Mlytics 是為意圖經濟打造的 AI Answer Engine。

媒體與出版業者的流量正在被廣告稀釋、被 AI search 侵蝕，yield 持續下滑。我們在每篇文章裡嵌入 AI Q&A，把讀者的購買意圖抓出來、匹配給品牌客戶，用 CPL 變現。Content Owner 拿到新的收入流，Brand 拿到比傳統廣告精準得多的 qualified leads。

我們的 5 層 Intent Refinery — Content → Decisive Engine → AI Q&A → Full Conversation → Lead Pilot — 已在 15+ 家台灣頭部媒體上線，服務 4M+ 週活躍使用者。

Mlytics 從 multi-CDN 起家。那套基礎設施 — <50ms 路由、multi-vendor failover — 現在是整個 refinery 的技術底層。同樣的工程紀律，更大的企圖心。

### 關鍵數據

- **4M+** 週活躍使用者
- **15+** 台灣頭部媒體已上線整合
- **2,500x** 效率提升：AI 生成內容 $0.10 vs. 人工撰寫 $250

---

## 我們在做什麼

- **有實際規模的分散式系統。** 4M+ WAU、<50ms p95、multi-vendor failover（Cloudflare / Akamai / Fastly）、真實的 CDN 經濟模型。
- **真的在做事的 AI agent。** Intent classification、publisher-specific knowledge base 上的 RAG、multi-step agent runtime。不是 chatbot demo。
- **雙邊市場的機制設計。** Publisher supply 對接 brand demand，透過 real-time intent matching。CPL 定價。Editorial guardrails。真的有錢在流動。
- **Product engineering，不是 feature engineering。** 每個工程師都參與 scoping。每個 slice 都有付費客戶的 gate。沒有 ship 給真實使用者的東西，就不算 ship。

---

## 開放職缺

| 職位 | 地點 | 團隊 |
|------|------|------|
| [AI-Powered Full Stack Engineer](./roles/ai-powered-full-stack-engineer.md) | 新加坡 / 台北 | Product |
| [AI Data Engineer](./roles/ai-data-engineer.md) | 新加坡 / 台北 | Data & Innovation |

---

## 我們怎麼做事

2026 年 4 月初，四個人的團隊在六小時內 ship 了一整套 AI 影音新聞產線。九天後，一位工程師搭配 Claude Opus 在一天內 ship 了雙 agent 品牌整合系統。在我們三個最新的 production codebase 裡，超過四分之一的 commit 以 Claude 為 co-author。這是 AI-first 工程從內部看起來的樣子，不是新聞稿。

**[我們怎麼做事 → Becoming Product Builders with Business Thinking](../how-we-ship.md)**

---

## 如何應徵

寄給我們任何能展現你思考方式的東西 — side project、技術文章、你引以為傲的 PR、或一段訊息解釋為什麼這個機會引起你的注意。

📧 **[careers@mlytics.com](mailto:careers@mlytics.com)**

我們在意的是你做過什麼，不是你待過哪裡。

有問題？→ [候選人 FAQ](./faq.md)
```

- [ ] **Step 3: Commit**

```bash
git add zh-TW/README.md
git commit -m "Add Traditional Chinese careers landing page"
```

---

### Task 5: Create zh-TW/faq.md

**Files:**
- Create: `zh-TW/faq.md`

- [ ] **Step 1: Create zh-TW/faq.md**

```markdown
[← 回到職缺首頁](./README.md)

# 候選人 FAQ

---

### Mlytics 到底在做什麼？一句話解釋。

Mlytics 是 AI Answer Engine。媒體有流量但變現越來越難、品牌有預算但廣告越來越浪費 — 我們用 AI 把流量裡的購買意圖抓出來、配給品牌，讓兩邊都拿到更好的結果。

---

### LinkedIn 上你們還寫 multi-CDN，是不是過時了？

對。我們今年正在更新所有平台。Multi-CDN 是我們的歷史 — 我們從 CDN 起家、做得很好、現在這個技術成了新產品的底層。但今天 Mlytics 是 AI Answer Engine，不是 CDN 公司。

---

### 你們已經 pivot 過一次了，會不會再 pivot？

不會 — 但這值得展開講。從 multi-CDN 到 AI Answer Engine 不是 pivot，是 evolve：multi-CDN 仍然存在、仍然在賣、客戶仍然在用，它變成了我們上層產品的 substrate。我們是把產品線加寬，不是換產品。AI Answer Engine 本身的方向 — intent → commerce — 不會變。

---

### 你們接受遠端工作嗎？

Product 跟 Engineering 團隊主要在台灣、密切協作，但 remote 是可以談的 — 我們願意討論適合的方式。GTM 相關的角色（Sales、Partnerships、Customer Success）取決於市場需求，具體狀況建議在面試過程中洽談。

---

📧 **[careers@mlytics.com](mailto:careers@mlytics.com)** · [← 回到職缺首頁](./README.md)
```

- [ ] **Step 2: Commit**

```bash
git add zh-TW/faq.md
git commit -m "Add Traditional Chinese candidate FAQ"
```

---

### Task 6: Create zh-TW/roles/ JDs

**Files:**
- Create: `zh-TW/roles/ai-data-engineer.md`
- Create: `zh-TW/roles/ai-powered-full-stack-engineer.md`

Both files use a Chinese company intro section followed by the English role-specific content (copied unchanged from the English JD, starting at "## The role").

- [ ] **Step 1: Create zh-TW/roles/ai-data-engineer.md**

Write a file that contains:

1. Back link: `[← 回到所有職缺](../README.md)`
2. Title: `# AI Data Engineer`
3. Location/work style in Chinese:
   ```
   **地點：** 新加坡（PR+）/ 台灣台北
   **工作模式：** 新加坡 / 馬來西亞（遠端）/ 台灣（混合）
   ```
4. Chinese company intro ("30 秒認識 Mlytics"):
   ```
   ## 30 秒認識 Mlytics

   Mlytics 是 AI Answer Engine。我們幫媒體出版業者把讀者意圖轉化為商業成果 — 用高品質的 CPL 營收取代日漸衰退的 CPM 廣告收入。我們的 Intent Refinery 已在 15+ 家台灣頭部媒體上線，服務 4M+ 週活躍使用者。

   Mlytics 從 multi-CDN 起家。那套基礎設施 — <50ms 路由、multi-vendor failover — 現在是整個 refinery 的技術底層。

   [更多關於 Mlytics →](../README.md)
   ```
5. Separator: `---`
6. Everything from `## The role` onward — copied verbatim from `roles/ai-data-engineer.md` (lines 26 onward, after the Task 3 edit has been applied)

- [ ] **Step 2: Create zh-TW/roles/ai-powered-full-stack-engineer.md**

Same structure as Step 1, but:
- Title: `# AI-Powered Full Stack Engineer`
- Role content copied from `roles/ai-powered-full-stack-engineer.md` (lines 33 onward from original, which becomes lines after "## The role" post-Task 3 edit)

- [ ] **Step 3: Commit**

```bash
git add zh-TW/roles/
git commit -m "Add Traditional Chinese JDs with Chinese intro and English role content"
```

---

## Metric consistency checklist

After all tasks are complete, verify these numbers appear consistently in all 8 files:

| Check | Expected |
|-------|----------|
| WAU | "4M+" everywhere (never "5M", "4.7M", "15M", or "50M") |
| Publishers | "15+" everywhere (never "22" or "58") |
| Efficiency | "2,500x" only in README files (not in JDs or FAQ) |
| Positioning | "AI Answer Engine" appears in every file's company intro |
| "Intent Refinery" | Appears in README files; JD intro says "Our Intent Refinery is live" |

Run a quick grep to confirm:

```bash
grep -rn "5M\|4\.7\|50 million\|58 live\|22 live" README.md faq.md roles/ zh-TW/
```

Expected: no matches. If any match, it's a stale number that needs fixing.
