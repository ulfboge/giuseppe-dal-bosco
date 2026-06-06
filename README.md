# Giuseppe Dal Bosco — Job Search Hub

> Senior Forestry Specialist & Advisor | Tropical Plantations · Landscape Restoration · Forest Investment
> Based in Hasbergen, Germany · Open to international relocation
> English · Spanish · Italian

**Live site:** https://ulfboge.github.io/giuseppe-dal-bosco/

---

## Pages

| Page | URL | Purpose |
|---|---|---|
| Profile | `/` | Professional profile — summary, experience, strengths, languages, target roles |
| Jobs | `/jobs.html` | Live job feed + curated org career pages + keyword bank |

---

## Repository Structure

```
/
├── CLAUDE.md                   ← Project context for AI-assisted development
├── README.md                   ← This file
├── index.html                  ← Profile page
├── jobs.html                   ← Live job feed page (Adzuna API)
├── style.css                   ← Shared stylesheet
├── .nojekyll                   ← Bypasses Jekyll on GitHub Pages
├── assets/                     ← Images and static files
├── docs/
│   └── Profile.pdf             ← CV / profile document
└── data/                       ← Research and strategy documents
    ├── positioning.md          ← 5 professional positioning options + recommendation
    ├── job_targets.md          ← Prioritised role titles by track
    ├── search_terms.md         ← Keywords by platform (LinkedIn, Devex, FAO, etc.)
    ← target_organizations.md  ← 60+ target employers in 7 categories
    ├── scoring_framework.md    ← 6-criterion job-fit scoring system (1–5 scale)
    ├── website_content.md      ← Copywriting source for index.html
    └── automation_ideas.md     ← Enhancement ideas and implementation status
```

---

## Live Job Feed

`jobs.html` fetches real job postings on page load via the **Adzuna API** (free tier). It queries 6 keyword searches across 9 countries — UK, Germany, Netherlands, France, US, Canada, South Africa, Australia, Singapore — deduplicates results, filters by title relevance, and sorts newest-first.

A date-range toggle (Any time / Past month / Past week / Past 24 h) re-fetches with a tighter date filter. Credentials are embedded in `jobs.html`; see `CLAUDE.md` for API details.

---

## Data Files

| File | Use for |
|---|---|
| `data/positioning.md` | Choosing which headline/summary to use per application track |
| `data/job_targets.md` | Which job titles to search on each platform |
| `data/search_terms.md` | Saved searches and alerts on LinkedIn, Devex, FAO, etc. |
| `data/target_organizations.md` | Which organisations to check directly each week |
| `data/scoring_framework.md` | Evaluating a new posting before deciding to apply |
| `data/website_content.md` | Source copy for index.html; reusable for cover letter intros |
| `data/automation_ideas.md` | Future enhancements and what has already been implemented |

---

## Profile Summary

**Giuseppe Dal Bosco** is a Forest Engineer (Universidad del Valle de Guatemala, 1997/1999) with over 27 years of experience in tropical and sub-tropical forestry.

**Key highlights:**
- CEO, Fiji Hardwood Corporation — managed 60,000 ha state-owned mahogany plantations
- Forestry Specialist, KAYA (2023–2025) — forest landscape restoration planning, modelling, and monitoring
- M&E Specialist, Rainforest Alliance TREES Programme — 13 projects, 4 countries, international donors
- 20+ years independent consulting — plantation management, natural forest, financial modelling, FSC
- Carbon forestry inventories and financial modelling
- FSC FM/CoC certified (SW-FM/COC-1450; SW-COC-939)
- Languages: English, Spanish, Italian (native/bilingual); German (limited); Portuguese (elementary)

---

## Assets to Add

- [ ] `assets/profile-photo.jpg` — professional headshot
- [ ] `assets/cv-giuseppe-dalbosco.pdf` — current CV (update `docs/Profile.pdf` or add here)
- [ ] Confirm Portuguese working level for accuracy in `data/search_terms.md`
- [ ] Confirm VCS/REDD+ project credentials before targeting carbon-specific roles

---

_Last updated: June 2026_
