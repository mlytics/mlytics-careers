[← 回到所有職缺](../README.md)

# AI Data Engineer

**地點：** 新加坡（PR+）/ 台灣台北
**工作模式：** 新加坡 / 馬來西亞（遠端）/ 台灣（混合）

---

## 30 秒認識 Mlytics

Mlytics 是 AI Answer Engine。我們幫媒體出版業者把讀者意圖轉化為商業成果 — 用高品質的 CPL 營收取代日漸衰退的 CPM 廣告收入。我們的 Intent Refinery 已在 15+ 家台灣頭部媒體上線，服務 4M+ 週活躍使用者。

Mlytics 從 multi-CDN 起家。那套基礎設施 — <50ms 路由、multi-vendor failover — 現在是整個 refinery 的技術底層。

[更多關於 Mlytics →](../README.md)

---

## The role

You'll join the **Data & Innovation team**, reporting to our Data & Innovation Lead, Tim. Tim has built the foundation: Databricks with Unity Catalog, medallion architecture for CDN usage data, MLflow for experiment tracking, vector search and embedding pipelines for the AIGC product. The architectural choices are made. What's missing is the person who turns the intent data specs into production systems.

This is not a research role. We've already designed the behavioral tracking pipeline (Bronze → Silver → Gold), defined 6 composite intent signal tiers with specific CPC pricing, built the intent taxonomy framework, and spec'd a second-price auction matching engine. The specs exist. **Your job is to make them real** — and then make them better based on what the data actually tells you.

You'll work closely with the full-stack product engineer (building the widget and API layer), with Tim (on ML experimentation and model selection), and directly with the Head of Product and CEO on what the data means commercially. When the BD team walks into a meeting with a financial services brand and says "we can show you which users are actively considering retirement planning vs. casually browsing" — the confidence behind that claim comes from your pipeline.

---

## What you'll do in your first 90 days

**Month 1 — Ship the behavioral tracking pipeline.**

Our clickstream SDK captures 8 event types (page_enter, scroll_depth, active_time, page_exit, widget_visible, qa_click, qa_read, cross_page) from 58 publisher sites. This data lands in S3 as JSON. Your first deliverable is the production pipeline on Databricks:

- **Bronze:** Auto Loader streaming ingestion from S3 into raw Delta tables
- **Silver:** Parsed, validated, GeoIP-enriched event records with session stitching
- **Gold:** Hourly session_summary aggregation — engagement tier, scroll depth, active time, Q&A interaction depth, search intent signals

By the end of month 1, the pipeline is live, monitored, and processing events from all 58 publishers with <5 minute end-to-end latency.

**Month 2 — Implement intent scoring and make it queryable.**

The session_summary Gold table feeds a composite intent scoring model that classifies users into tiers with dramatically different commercial value:

- **Deep Reader + Decision Click** → CPC $1.50–$2.00 (active >60s, scroll >75%, decision-stage Q&A clicked)
- **Search Intent + Q&A Engagement** → CPC $1.50–$2.00 (search referrer + 2+ Q&A clicks + >10s read time)
- **Multi-Article Researcher** → CPC $1.00–$1.50 (3+ pages, >3 min active)
- Down to **Bounce** → do not monetize (<10s, <25% scroll, 0 clicks)

Build a Genie Room on top of this so the commercial team can self-serve: "Show me high-intent users on cnyes.com in the investment vertical this week" should return an answer in seconds, not require a data team ticket.

**Month 3 — Build the matching engine foundation.**

Connect intent signals to advertiser campaigns. Implement the core matching logic: intent classification → campaign filter (vertical, publisher, intent L1/L2/L3) → score (bid × confidence × profile richness × historical CTR) → second-price auction. This is where your pipeline meets the full-stack engineer's Sponsored Questions product — the first revenue-generating integration of the Intent Refinery.

---

## What we're looking for

**The non-negotiables:**

- You've built production data pipelines that business teams actually depend on — not just notebooks that run once. Streaming ingestion, transformation, aggregation, monitoring, alerting.
- You're proficient in **Python and SQL** at production scale. You've written Spark jobs, not just pandas scripts.
- You have hands-on experience with **Databricks** or a comparable lakehouse platform (Delta Lake, Unity Catalog, Structured Streaming). You understand medallion architecture and why governance matters.
- You can implement ML scoring models and deploy them as production features — not hand them off to "the engineering team." You've operationalized a model that runs continuously, not just trained one that sits in a notebook.
- You think about data as a **product**, not a warehouse. You care about latency, freshness, accuracy, and whether the downstream consumer (human or API) can actually use what you produce.

**What would make you exceptional:**

- Experience building **real-time user scoring or segmentation systems** in ad tech, martech, or fintech — you've seen what "intent signals" look like in production and you know the difference between a useful signal and noise
- Familiarity with **MLflow** for experiment tracking and model management — Tim uses it extensively, and you'll collaborate on model selection and A/B testing
- Experience with **vector search and embeddings** for content or user similarity — this feeds into cross-site intent profiles and content-to-intent matching
- You've built systems where the data quality directly determined revenue — pricing engines, recommendation systems, fraud scoring, or ad auction mechanics
- 中文溝通能力 — 我們團隊日常混用中英文，如果你能用中文討論技術方案和數據定義，會是很大的加分

---

## Tech stack

| Layer | What we use |
|-------|-------------|
| Platform | Databricks / Unity Catalog / Delta Lake |
| Compute | Spark Structured Streaming / Databricks Workflows |
| ML | MLflow / Python / embeddings / vector search |
| Storage | S3 (clickstream) / PostgreSQL / Redis |
| Languages | Python / SQL / some Go for service integration |
| Infra | GCP / AWS / CloudFlare Workers (collection endpoint) |
| Observability | Databricks SQL dashboards / Grafana / alerting |

---

## How this role connects to the bigger picture

The Intent Refinery has four monetization layers. Your pipeline powers all of them:

| Product | Pricing | How your data makes it work |
|---------|---------|---------------------------|
| Sponsored Questions | CPC $0.50–$2.00 | Intent classification triggers real-time ad auction |
| Intent Display Network | CPM $15–$40 | User intent profiles enable premium targeting |
| Intent Micro-sites | CPL $5–$20 | Cross-site intent graphs identify high-value leads |
| Full Conversation | Performance | Multi-turn dialog scoring determines conversion readiness |

The commercial target is $70–100K+ MRR by month 6. The features the full-stack engineer builds are the surface. **Your pipeline is the engine underneath.**

---

## Why this matters right now

We're raising our next round. The investment thesis is that real-time intent data captured at the point of content consumption is structurally more valuable than historical behavioral data or contextual targeting. That thesis is only as strong as the data system that proves it.

Right now, a brand prospect asks "how is this different from contextual advertising?" and we show them a spec. After you ship, we show them a live dashboard where a Deep Reader + Decision Click user is worth $1.50 CPC and a Casual Browser is worth $5 CPM — a 30x spread. That's the difference between a hypothesis and a business.

---

**Want to see how we actually build this?** → [How we ship: Becoming Product Builders with Business Thinking](../how-we-ship.md)

---

## How to apply

Send us something that shows how you think about data systems — a pipeline you've built, an architecture decision you made and why, a scoring model you operationalized. We care about what you've shipped more than what tools you've used.

📧 **[careers@mlytics.com](mailto:careers@mlytics.com)**
