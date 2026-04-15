# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A **content-only Jekyll site** that hosts Mlytics' public career pages (job descriptions) at **careers.mlytics.com**. There is no application code, no build step to run locally, and no tests. Everything here is Markdown rendered by GitHub Pages.

- `_config.yml` — selects `jekyll-theme-minimal`. GitHub Pages builds and serves on push to `main`.
- `CNAME` — pins the custom domain to `careers.mlytics.com`.
- `README.md` — doubles as the site's landing page (the index).
- `roles/*.md` — one Markdown file per open position. Each role links back to the index via a relative `[← Back to all positions](../README.md)` at the top.

## How the landing page works

With `jekyll-theme-minimal` and no `index.md`, **GitHub Pages renders `README.md` as the site root**. That means edits to `README.md` are edits to careers.mlytics.com's landing page — treat it as user-facing marketing copy, not an internal repo readme.

## Common workflow

Because GitHub Pages does the build, the loop is just:

1. Edit or add Markdown under `roles/` (or update `README.md` for the index).
2. Commit and push to `main`. Pages rebuilds automatically; changes appear at careers.mlytics.com within ~1 minute.
3. To preview locally (rarely needed), the standard approach for a minimal-theme Jekyll site is `bundle exec jekyll serve`, but there is **no `Gemfile` in this repo** — you would need to scaffold one first, so only do this if the user explicitly asks.

Adding a new role: create `roles/<slug>.md`, keep the `[← Back to all positions](../README.md)` header line, and add a row to the Open Positions table in `README.md` (and in `careers-repo-README.md` if the staging copies are still being maintained).

## Voice and structure conventions (derived from existing JDs)

The two existing role files establish a strong, deliberate house style. Match it when drafting or editing new JDs:

- **Opening hook is a thesis, not a company blurb.** Both JDs open with a punchy framing (e.g. "The engine doesn't change. The packet does.") and a narrative about the Intent Refinery before describing the role.
- **Specific numbers over adjectives.** 50M MAU, 4.7M WAU, 58 publisher integrations, 2,500x efficiency. Keep claims quantified and consistent with `careers-repo-README.md`.
- **Concrete stack and specs, not buzzwords.** Roles reference Databricks + Unity Catalog, medallion architecture, MLflow, vector search, second-price auction matching, etc. New roles should name real systems the candidate will touch.
- **"This is not a research role" framing.** JDs emphasize shipping against existing specs. Preserve that tone — avoid softening into generic "collaborate with stakeholders" language.
- **Bilingual team.** English and Traditional Chinese are both in active use; don't assume English-only context when making edits.

## What not to do

- Don't introduce a build toolchain, CI, linters, or package manifests unless the user asks — this is intentionally a zero-dependency Pages site.
- Don't rewrite the JD voice toward generic corporate phrasing. The specificity *is* the product.
- Don't edit `CNAME` or `_config.yml` without confirming — these affect domain routing and theme.
