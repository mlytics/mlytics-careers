# Design Spec: Careers Site Rewrite with Talent Narrative

**Date:** 2026-05-12
**Source material:** `mlytics-talent-narrative.md` from `mlytics-cortex` repo
**Scope:** Full rewrite of careers.mlytics.com content + Traditional Chinese mirror

---

## 1. Goals

- Align the careers site with the updated company positioning: **AI Answer Engine + Intent Refinery** (coexisting, not one replacing the other)
- Update all public-facing metrics to current numbers (4M+ WAU, 15+ publishers)
- Add a Candidate FAQ page to address the "I still don't understand what you do" problem
- Provide a full Traditional Chinese mirror of the site under `zh-TW/`

## 2. Scope

### In scope

| File | Action |
|------|--------|
| `README.md` | Full rewrite — new tagline, new About, new engineering culture section, updated numbers |
| `faq.md` | New file — 6 questions selected from talent narrative |
| `roles/ai-data-engineer.md` | Replace company intro section only; role-specific content unchanged |
| `roles/ai-powered-full-stack-engineer.md` | Replace company intro section only; role-specific content unchanged |
| `zh-TW/README.md` | Full Traditional Chinese mirror of the English README |
| `zh-TW/faq.md` | Full Traditional Chinese mirror of the English FAQ |
| `zh-TW/roles/ai-data-engineer.md` | Chinese company intro + English role-specific content |
| `zh-TW/roles/ai-powered-full-stack-engineer.md` | Chinese company intro + English role-specific content |

### Out of scope

- `how-we-ship.md` — no changes (numbers will be temporarily inconsistent)
- `_config.yml` / `CNAME` — no changes
- New role postings — not adding Senior AI Engineer, Brand PM, or Senior Designer
- JD role-specific content (responsibilities, requirements, tech stack) — unchanged

## 3. Unified metrics

All files must use these numbers consistently:

| Metric | Value |
|--------|-------|
| User scale | 4M+ weekly active users |
| Publishers | 15+ live publisher integrations |
| Efficiency | 2,500x (AI-generated content vs. human-written) |
| Team size | ~20-30 people |
| Positioning | AI Answer Engine + Intent Refinery (coexisting) |

## 4. README.md structure

### 4.1 Language switcher

Top of file:
```markdown
[繁體中文版 →](./zh-TW/README.md)
```

### 4.2 Tagline

```markdown
# Mlytics Careers

> **We turn content into commerce.**
> The AI Answer Engine for the intent economy.
```

Followed by a 2-3 sentence summary that introduces both "AI Answer Engine" and "Intent Refinery" concepts. Explains what we do in concrete terms: capture reader intent, match to brands, convert via CPL. Ends with "Not impressions. Not clicks. Declared purchase intent."

### 4.3 About Mlytics

Structure (approximately 150-200 words):

1. **Mission sentence** — help publishers turn reader intent into commercial outcomes; help brands stop buying impressions and start buying confirmed intent
2. **5-layer refinery** — one sentence: Content → Decisive Engine → AI Q&A → Full Conversation → Lead Pilot
3. **History** — "We started as a multi-CDN company. That infrastructure — <50ms routing, multi-vendor failover — is now the substrate underneath."
4. **No "Attention Economy to Intent Economy" academic framing** — speak in commercial actions, not theory

### 4.4 By the numbers

Updated bullet list:
- **4M+** weekly active users
- **15+** live publisher integrations (Taiwan's top media properties)
- **2,500x** efficiency gain: $0.10 AI-generated content vs. $250 human-written

Removed items:
- "Over 100K WAU on AIGC intent product" (too small relative to 4M)
- "Multi-cloud architecture spanning GCP, AWS" (moved to engineering culture section)

### 4.5 What we work on

Replaces the old "How we work" section. Four bullets from the talent narrative:

1. **Real distributed systems at meaningful scale.** 4M+ WAU, <50ms p95, multi-vendor failover (Cloudflare / Akamai / Fastly), real CDN economics.
2. **AI agents that actually do work.** Intent classification, RAG over publisher-specific knowledge bases, multi-step agent runtime. Not chatbot demos.
3. **Two-sided marketplace mechanics.** Publisher supply meets brand demand through real-time intent matching. CPL pricing. Editorial guardrails. Real money flowing.
4. **Product engineering, not feature engineering.** Every engineer participates in scoping. Every slice has a paying customer gate. If it doesn't ship to a real user, it didn't ship.

### 4.6 Open Positions

Same table as current, no changes to the two listed roles:

| Role | Location | Team |
|------|----------|------|
| AI-Powered Full Stack Engineer | Singapore / Taipei | Product |
| AI Data Engineer | Singapore / Taipei | Data & Innovation |

### 4.7 How we ship

Condensed to 2-3 sentence summary + link to `how-we-ship.md`. No longer repeating the long narrative on the front page.

### 4.8 How to Apply

Preserve current structure. Add FAQ link:
```markdown
Questions? → [Candidate FAQ](./faq.md)
```

### 4.9 Removed sections

- **"Why Mlytics now"** — decided against a standalone section; the About and What We Work On sections carry enough conviction without a listicle-style pitch
- **"Our thesis"** — academic framing removed

## 5. faq.md

Four questions, sourced from talent narrative Section 5. Written in English for international candidates.

1. **What does Mlytics actually do, in one sentence?**
2. **LinkedIn still says multi-CDN — is that outdated?**
3. **You've pivoted once. Will you pivot again?**
4. **Are you open to remote work?**

Removed from talent narrative's FAQ:
- "Can 20-30 people really pull this off?" (draws unnecessary attention to team size as a concern)
- Competitive comparison with Cloudflare / Perplexity / TheTradeDesk (risk of inaccuracy; better suited for recruiter calls)
- Funding status (needs Finance alignment before publishing)
- "Can I talk to current employees?" (process detail, better in email)
- "How do I explain Mlytics to friends/family?" (internal training, not public page)

Each answer follows the talent narrative's content but written in the careers site's direct, specific, no-bullshit voice.

## 6. JD updates (both roles)

### What changes

Replace the "The intent refinery" section at the top of each JD (everything before "## The role") with a compact company intro:

```markdown
## Mlytics in 30 seconds

Mlytics is an AI Answer Engine. We help media publishers turn
reader intent into commercial outcomes — replacing fading CPM
revenue with high-quality CPL revenue. Our Intent Refinery is
live with 15+ of Taiwan's top media properties, serving 4M+
weekly active users.

We started as a multi-CDN company. That infrastructure — <50ms
routing, multi-vendor failover — is now the substrate underneath.

[More about Mlytics →](../README.md)
```

### What stays

Everything from "## The role" onward is unchanged.

## 7. zh-TW/ mirror

### Structure

```
zh-TW/
├── README.md
├── faq.md
└── roles/
    ├── ai-data-engineer.md
    └── ai-powered-full-stack-engineer.md
```

### Translation principles

- **Not a word-for-word translation.** Rewritten in natural Traditional Chinese, drawing on the talent narrative's original Chinese voice.
- **Technical terms stay in English:** Databricks, LangGraph, CPL, WAU, CDN, RAG, etc.
- **JD structure:** Chinese company intro section ("Mlytics in 30 seconds" equivalent) + English role-specific content (unchanged from English version).
- **zh-TW README.md top:** `[English version →](../README.md)`
- **zh-TW JD back links:** point to `../README.md` (the zh-TW index)

### What gets rewritten in Chinese

- README.md (all sections)
- faq.md (all questions and answers)
- JD company intro section only

### What stays in English (within zh-TW files)

- JD role-specific content (The role, What you'll do, What we're looking for, Tech stack, etc.)
- Technical terms throughout

## 8. Files not modified

| File | Reason |
|------|--------|
| `how-we-ship.md` | User decision — update separately later. Numbers will be temporarily inconsistent with the rest of the site. |
| `_config.yml` | No structural changes needed. `docs/` already excluded. `zh-TW/` will be served by GitHub Pages automatically. |
| `CNAME` | No change. |
