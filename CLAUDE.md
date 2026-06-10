# CLAUDE.md — Giuseppe Dal Bosco Job Search Hub

This file documents the project for future Claude conversations.

---

## What This Is

A personal job search hub for **Giuseppe Dal Bosco**, a senior forestry and restoration professional (27+ years, tropical and sub-tropical, four continents). Built and maintained by ulfboge on his behalf.

The repo has two purposes:
1. A public profile page presenting Giuseppe to potential employers
2. A live job feed page aggregating relevant postings worldwide

**Live site:** https://ulfboge.github.io/giuseppe-dal-bosco/
**GitHub repo:** https://github.com/ulfboge/giuseppe-dal-bosco

---

## Pages

### `index.html` — Profile
Giuseppe's professional profile: summary, key strengths (8 cards), selected experience (5 roles), languages (5), target roles and regions, contact. Styled with `style.css`.

### `jobs.html` — Live Job Feed
- **Live feed section** — Fetches real job postings from the Adzuna API across 9 countries (GB, DE, NL, FR, US, CA, ZA, AU, SG) using 6 keyword searches, plus the ReliefWeb v2 jobs API (8 keyword queries, NGO/UN/development sector). Results are merged, deduplicated by ID, filtered by title relevance, and sorted newest-first. ReliefWeb results carry a "ReliefWeb" source badge.
- **Same-day cache** — Every job seen today is stored in localStorage (`gdb_job_cache_v1`) and merged back in on each refresh, so thin/empty API responses (Adzuna rate limits or quota) never make earlier results disappear. The cache resets the next calendar day. Per-browser only — different devices each build their own cache.
- **Target organizations** — 16 curated org career page links grouped into three categories.
- **Keywords section** — 16 click-to-copy keyword pills for use on other job boards.

---

## Adzuna API

- Credentials are embedded directly in `jobs.html` (the repo is public, the API is read-only job search)
- **Free tier limit:** 250 API calls/day — the page makes ~18 calls per load (9 searches × up to 2 countries per keyword), supporting ~13 full loads/day
- **Title relevance filter:** After fetching, results are filtered client-side — only jobs whose title contains forestry/restoration terms are shown. The filter list is in the `isRelevant()` function in `jobs.html`

---

## ReliefWeb API

- Registered appname: `dalbosco-jobsearch-x7k4sDESTKw8Q9CBJBuv` (approved 2026-06-10, stored in `RELIEFWEB_APPNAME` in `jobs.html`)
- POST to `https://api.reliefweb.int/v2/jobs` — open jobs only, sorted by date, 10 results per query
- No daily-limit concerns comparable to Adzuna; the API is free and read-only

---

## Design System (`style.css`)

All shared styles live in `style.css`. `jobs.html` adds page-specific styles in a `<style>` block.

| Token | Value |
|---|---|
| `--green-dark` | `#1a3a2a` |
| `--green-mid` | `#2d6a4f` |
| `--green-light` | `#52b788` |
| `--green-pale` | `#d8f3dc` |
| `--sand` | `#f8f4ed` |
| `--max-width` | `860px` |
| Font | Segoe UI / system-ui |

Sections alternate between `--sand` and `--white` backgrounds. Cards use left green border (`border-left: 4px solid var(--green-light)`), box-shadow, and a slight translateY hover lift.

---

## Repository Structure

```
/
├── CLAUDE.md                   ← This file
├── README.md                   ← Human-readable project overview
├── index.html                  ← Profile page
├── jobs.html                   ← Live job feed page
├── style.css                   ← Shared stylesheet
├── .nojekyll                   ← Tells GitHub Pages to skip Jekyll
├── assets/                     ← Images and static files (currently empty)
├── docs/
│   └── Profile.pdf             ← Giuseppe's CV/profile document
└── data/                       ← Supporting research and strategy documents
    ├── positioning.md          ← 5 positioning options + recommendation
    ├── job_targets.md          ← Prioritised role titles by track
    ├── search_terms.md         ← Keywords by platform (LinkedIn, Devex, FAO, etc.)
    ├── target_organizations.md ← 60+ target employers in 7 categories
    ├── scoring_framework.md    ← 6-criterion job-fit scoring system (1–5 scale)
    ├── website_content.md      ← Copywriting source for index.html
    └── automation_ideas.md     ← Enhancement ideas (see status notes within)
```

---

## Key Decisions Made

- **Standalone git repo** inside `C:\Users\galag\GitHub\giuseppe\` — the parent home-directory git repo was incorrectly pointed to `forest-compliance-offers`. A fresh `.git` was initialised inside `giuseppe/` and pointed to the new `giuseppe-dal-bosco` remote.
- **`.nojekyll`** added to root — bypasses Jekyll processing so GitHub Pages serves HTML files directly.
- **Adzuna over LinkedIn links** — LinkedIn search cards were replaced with real job listings via the Adzuna free API. LinkedIn results were keyword searches, not actual postings.
- **Client-side title filter** — Adzuna searches full job descriptions, returning some irrelevant results. The `isRelevant()` function in `jobs.html` filters on job title only.
- **No backend** — everything is static HTML/CSS/JS. No build step, no framework, no dependencies.

---

## Giuseppe's Profile Summary

- Forest Engineer, Universidad del Valle de Guatemala (1997/1999)
- 27+ years tropical and sub-tropical forestry across 10+ countries
- CEO, Fiji Hardwood Corporation — 60,000 ha state-owned mahogany plantations
- Forestry Specialist, KAYA (2023–2025) — forest landscape restoration planning, modelling, monitoring
- M&E Specialist, Rainforest Alliance TREES — 13 projects, 4 countries, USAID/IDB donors
- 20+ years independent consulting — plantation management, natural forest, financial modelling, FSC
- FSC FM/CoC certified (SW-FM/COC-1450; SW-COC-939)
- Languages: English, Spanish, Italian (native/bilingual); German (limited); Portuguese (elementary)
- Based in Hasbergen, Lower Saxony, Germany — open to international relocation
- LinkedIn: https://www.linkedin.com/in/giuseppe-dalbosco-35815b2a

---

## Target Role Categories

1. Forest Landscape Restoration (NGOs, multilaterals, restoration companies)
2. Senior Forestry / NRM Advisory (consulting, development agencies)
3. Forest Carbon & NbS (South Pole, Wildlife Works, EcoAct)
4. FSC / Certification (Preferred by Nature, FSC International)
5. Multilateral Programme Officer (FAO, UNDP, World Bank, GIZ)
6. Commercial Forestry with sustainability/restoration division

---

## What Not to Do

- Do not add Jekyll or any site generator — the site is intentionally plain HTML
- Do not commit `.claude/` directory or API keys in separate files
- Do not add the parent home-directory tracked files — the `giuseppe/.git` is standalone
