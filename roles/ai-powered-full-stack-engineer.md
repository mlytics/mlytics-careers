[← Back to all positions](../README.md)

# AI-Powered Full Stack Engineer

**Location:** Singapore (PR+) / Taipei, Taiwan
**Work style:** Singapore / Malaysia (Remote) / Taiwan (Hybrid)

---

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

---

## The role

You'll be one of the first engineers dedicated to the Intent Refinery product line. You'll work directly with the Head of Product and the CEO. There is no backlog to groom — there's a revenue loop to close, and you'll have the autonomy to close it.

"End-to-end" means exactly that. We're a team of under 30. There is no DevOps team, no SRE team, no platform team. **You own the full lifecycle of what you build** — from API design to frontend experience to deployment to observability to the alert that tells you something broke at 2am. This isn't a staffing gap; it's how we believe software should be built at this stage. If you've only ever worked in organizations where "someone else handles deployment," this will feel uncomfortable. If you've been wanting the kind of ownership where your code ships to millions of users and you can trace the revenue impact the same week — this is it.

---

## What you'll actually do

**Close the loop between intent capture and revenue.** This is the job. Everything below serves this mission.

- Design and build backend services (Go / Python) with an **OpenAPI-first** approach — our APIs are evolving toward MCP-compatible agent interfaces where machines, not just humans, consume our product
- Build frontend experiences (Vue.js / Nuxt.js) that capture user intent: AI-powered Q&A widgets, conversational flows, and rich media interactions embedded across publisher sites
- Integrate LLM APIs and AI models into production features — intent classification, sponsored question matching, conversational commerce — at real scale, not as experiments
- Rapid-prototype new AI experiences and **kill or ship them within days, not months.** We produced a full AI animation pipeline in 45 minutes using 46 API calls chained together. That's the velocity we expect.
- Deploy, monitor, and operate what you build — Kubernetes (EKS), Prometheus, Grafana, Sentry. You're the first responder because you're the person who knows the system best
- Treat cloud cost as a product constraint — we operate across GCP, AWS, and multi-cloud CDN architectures, and FinOps discipline is part of engineering excellence here
- Use AI tools as your default workflow. Claude Code, Cursor (company-provided), and internal code generation aren't optional — they're how we expect you to work. If you're still writing boilerplate by hand, you're moving too slowly.

---

## What we're looking for

**The non-negotiables:**

- You've shipped production SaaS products end-to-end — frontend, backend, deployment, monitoring. Multiple times. In environments where "that's not my job" wasn't an option.
- You're comfortable in **Go or Python** on the backend and **Vue.js** on the frontend. You don't need to be an expert in all of them today, but you need to be productive in weeks, not months.
- You've integrated LLM APIs or AI models into production features that real users touched.
- You think in **API contracts and system interfaces**, not just code. You design for the next team member who hasn't been hired yet.
- You default to shipping. When the brief is messy, the requirements are half-formed, and nobody's drawn a wireframe — you make a decision, build a version, put it in front of users, and iterate. Waiting for clarity is not in your vocabulary.

**What would make you exceptional:**

- Experience in **ad tech, martech, or publisher monetization** — you understand why intent data is worth more than impression data, and you know what CPM, CPC, and ROAS mean in practice
- Familiarity with **agent frameworks and protocols** (MCP, A2A, LangGraph, n8n) and a point of view on where AI-native software architecture is headed
- You've worked at a company where the product you built directly determined whether the company raised its next round or signed its next customer
- 中文溝通能力 — 我們團隊日常混用中英文，如果你能順暢地用中文討論技術方案、參與產品討論，會是很大的加分

---

## Tech stack

| Layer | What we use |
|-------|-------------|
| Frontend | Vue.js / Nuxt.js / Vuex |
| Backend | Golang / Python / PostgreSQL / Redis |
| Infrastructure | EKS (Kubernetes) / GCP / AWS / multi-cloud CDN architecture |
| Observability | Prometheus / Grafana / Sentry / Loki |
| AI tooling | Claude Code / Cursor / internal code generation tools |
| Data | Databricks / S3 clickstream pipelines / vector search |

Our architecture spans content delivery optimization, real-time behavioral data capture, and AI model orchestration across a multi-cloud footprint. If genuine systems complexity is what excites you — not toy problems — you'll find plenty here.

---

## Why this matters right now

We're at the inflection point between "proven engine" and "proven revenue model." The CDN business is profitable. The Intent Refinery has live users, live data, and working prototypes across four monetization layers. What's missing is the proof that captured intent converts to brand revenue — and that proof determines whether we raise our next round, how we enter the US market, and what this company becomes.

The features you build in your first 90 days will be in the investor deck. The data your code generates will be in the pitch. This is not a figure of speech.

---

## How to apply

Send us something that shows how you think — a side project, a technical write-up, a PR you're proud of, or just a message explaining why this role caught your attention. We care about what you've built more than where you've worked.

📧 **[careers@mlytics.com](mailto:careers@mlytics.com)**
