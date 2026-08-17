<div style="display:flex;justify-content:space-between;align-items:baseline;margin-bottom:20px">
<a href="/">← Back to all positions</a>
<a href="/zh-TW/roles/senior-backend-engineer-decisive-engine.html">繁體中文版</a>
</div>

# Senior Backend Engineer — Decisive Engine

## Mlytics in 30 seconds

Mlytics is an AI Answer Engine. We help media publishers turn reader intent into commercial outcomes — replacing fading CPM revenue with high-quality CPL revenue. Our Intent Refinery is live with 15+ of Taiwan's top media properties, serving 4M+ weekly active users.

We started as a multi-CDN company. That infrastructure — <50ms routing, multi-vendor failover — is now the substrate underneath.

[More about Mlytics →](../README.md)

---

## The role

The Decisive Engine is one of the most valuable systems at Mlytics. It is the backend decision layer behind our multi-CDN product: real-time routing, scoring, contextual bandit logic, attribution, and the Kafka / Redis / ClickHouse data path that keeps those decisions moving.

This is not a role where you receive a clean service and add endpoints around the edges. You will become the primary technical owner of a complex, proven system operating at PB-scale traffic — understand why it was built the way it was, keep what works, challenge what no longer does, and make it faster, safer, and more capable.

The next chapter is not maintenance. We want the engine to become accessible to the agent ecosystem: **OpenAPI-first today, MCP-compatible interfaces and A2A possibilities next.** Your job is to deepen the backend we already have while creating the interfaces it will need in an agentic world.

---

## What you'll actually do

**Take ownership of the core decision engine — then move it forward.**

- Own and evolve the real-time decision pipeline across **routing, scoring, contextual bandits, and attribution**, keeping decisions stable, correct, observable, and low-latency as traffic grows.
- Design and optimize high-throughput services and data flows using **Go / Python, PostgreSQL / Redis, Kafka, ClickHouse, and EKS**. Work through concurrency, state, attribution latency, candidate cardinality, and horizontal scaling — not just CRUD APIs.
- Improve a large existing system without waiting for a rewrite. Add the tests, observability, migration paths, and architectural seams that let us change it safely while it remains in production.
- Move the product toward an agentic interface: design **OpenAPI-first** contracts, prototype MCP-compatible access and A2A integration, and use the smallest implementation that can validate whether a new access point creates real value.
- Use **Claude Code, Cursor, and other AI tools as your default development workflow**. AI should multiply your output without replacing engineering judgment, and the practices that work should become reusable knowledge for the rest of the team.
- Own features end to end in a team without a separate DevOps function: scope, design, implementation, CI/CD, deployment, observability, on-call, incident response, and follow-through after production feedback.
- Treat performance and cost as part of the product. Make the tradeoff between latency, compute, storage, and reliability visible, then improve unit traffic cost with evidence.

---

## End-to-end means production too

The person who designs a decision path should also know how it behaves under real traffic. You will share on-call responsibility for the services you own, respond when the decision pipeline degrades, restore service, and turn the incident into a durable improvement — code, monitoring, automation, or a runbook.

This is not an operations-first position, and success is not measured by how many fires you fight. Production ownership is the feedback loop that makes you a better backend engineer: it exposes the failure modes, performance cliffs, hidden coupling, and cost assumptions that architecture diagrams miss.

---

## What we're looking for

**The non-negotiables:**

- 5+ years of backend engineering experience at a senior level, with hands-on work in **distributed systems, high concurrency, and real-time data processing**.
- Deep proficiency in **Go or Python**, backed by strong fundamentals in concurrency, data structures, algorithms, and systems design.
- Production experience with several of **PostgreSQL, Redis, Kafka, ClickHouse, Kubernetes (EKS), GCP, and AWS**. You can reason about throughput, latency, state, failure, and cost across the whole path.
- Experience taking over and evolving a large or complex existing backend. You know how to build context, reduce risk, and improve architecture without treating greenfield development as the only satisfying work.
- Experience building with AI / LLMs or agent technologies such as **RAG, MCP, or agent interfaces**, and evidence that AI tools are already part of how you develop software.
- The ability to take an ambiguous product problem, choose a workable scope, and ship it end to end with limited supervision.

**What would make you exceptional:**

- Experience with routing, scoring, online learning or contextual bandits, attribution, multi-CDN systems, or another real-time decision engine where latency and correctness both matter.
- A track record of connecting backend architecture to a business outcome: retention, gross margin, infrastructure unit cost, or a new product interface.
- Experience defining OpenAPI contracts and turning an existing capability into an interface that other services or agents can reliably consume.
- You actively share AI-assisted development practices through code review, documentation, or technical sessions and make the engineers around you faster.
- 中文溝通能力 — our team works in both English and Chinese, and being able to discuss architecture and product tradeoffs in Chinese is a meaningful advantage.

**You might not be a fit if:**

- You only want greenfield work and would rather rewrite a mature system than understand and improve it.
- You see AI coding tools as a threat or an optional experiment instead of part of a modern engineering workflow.
- You consider your job complete when the code is merged and expect someone else to own deployment, performance, cost, and production behavior.
- You optimize for technically elegant output without asking what it changes for the product, the user, or the business.

---

## Tech stack

| Layer | What we use |
|-------|-------------|
| Core services | Go / Python |
| Decision systems | Routing / scoring / contextual bandits / attribution |
| Data path | Kafka / Redis / ClickHouse / PostgreSQL |
| Infrastructure | EKS (Kubernetes) / GCP / AWS / multi-cloud CDN architecture |
| Observability | Prometheus / Grafana / Sentry / Loki |
| Agent interfaces | OpenAPI / MCP-compatible services / A2A exploration |
| AI tooling | Claude Code / Cursor / internal code generation tools |

The tools are real, but the job is bigger than the stack. We need someone who can trace one routing decision across services, data, and infrastructure — and still explain why that decision matters to the product.

---

## What success looks like

- The Decisive Engine remains available, correct, and low-latency as traffic and decision complexity grow.
- p99 latency and unit traffic cost improve because the system is better understood and deliberately optimized.
- Features and fixes move from design to production faster without increasing incidents, regressions, or MTTR.
- A concrete OpenAPI / MCP milestone makes part of the decision engine usable through an agent-compatible interface.
- You own a meaningful service or module end to end with low supervision, including how it behaves in production.
- AI-native development practices improve not only your velocity, but also the team's through documented, reusable patterns.

---

## Why this matters right now

Mlytics began with multi-CDN routing. That decision engine is not legacy to be kept alive while the company moves on — it is the backend foundation the next product is being built on.

The engineer in this role will decide whether that foundation merely survives growth or becomes a deeper product capability: faster decisions, better economics, safer iteration, and a new interface for the agent era. If you want to inherit a hard system, make it unmistakably better, and open the next surface from it, this is that role.

---

**Want to see how we actually build this?** → [How we ship: Becoming Product Builders with Business Thinking](../how-we-ship.md)

---

## How to apply

Send us something that shows how you think about backend systems — a complex service you took over, a latency or concurrency problem you solved, a production incident that changed your design, or an AI-native workflow you made real. We care about what you shipped, what you measured, and what became better because you owned it.

📧 **[career@mlytics.com](mailto:career@mlytics.com)**
