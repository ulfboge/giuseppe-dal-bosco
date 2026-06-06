# Automation & Repository Expansion Ideas

_Optional enhancements for the job-search repository — Giuseppe Dal Bosco, June 2026_
_Ordered from simplest to most complex. Do not overbuild._

---

## Philosophy

This repository is a practical tool, not a project. Every addition should save time or reduce friction. If it takes longer to set up than it saves in the first month, skip it.

---

## Tier 1 — Manual Tracking (No Code Required)

### 1.1 Job Log Spreadsheet (CSV)

Add a file `data/job_log.csv` with columns:

```
date_found, title, organisation, source, url, deadline, score_total, status, notes
```

Status values: `identified` → `scored` → `applied` → `interview` → `offer` → `closed`

Open in any spreadsheet app (Excel, LibreOffice, Google Sheets). Commit updates weekly.

**Why this works:** A flat CSV in the repo is version-controlled, portable, and editable without any tools.

---

### 1.2 Saved Searches Bookmark File

Create `data/saved_searches.md` with a table of saved search URLs for each platform, annotated with last-checked date. Review weekly, update date manually.

```markdown
| Platform | Search Name | URL | Last Checked |
|---|---|---|---|
| LinkedIn | Forest Restoration Specialist | https://... | 2026-06-01 |
| Devex | Forestry Senior | https://... | 2026-06-01 |
```

---

### 1.3 Weekly Review Checklist

Add `CHECKLIST.md` with a simple weekly review routine:

```markdown
## Weekly Job Search Review

- [ ] Check LinkedIn Jobs saved searches (5 mins)
- [ ] Check Devex (5 mins)
- [ ] Check ReliefWeb + ImpactPool (5 mins)
- [ ] Check FAO iRecruitment (5 mins)
- [ ] Check target org careers pages (10 mins — rotate 3/week)
- [ ] Score any new roles using scoring_framework.md
- [ ] Update job_log.csv
- [ ] Draft any applications due this week
```

---

## Tier 2 — Simple Automation (Basic Scripts, ~1–2 hours setup)

### 2.1 GitHub Actions: Weekly Reminder

Add a `.github/workflows/weekly-reminder.yml` that creates a GitHub Issue every Monday titled "Weekly job search review — [date]". Free, requires no external services.

```yaml
name: Weekly Review Reminder
on:
  schedule:
    - cron: '0 8 * * 1'  # Every Monday at 08:00 UTC
jobs:
  remind:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/github-script@v7
        with:
          script: |
            github.rest.issues.create({
              owner: context.repo.owner,
              repo: context.repo.repo,
              title: `Weekly job search review — ${new Date().toISOString().slice(0,10)}`,
              body: 'Review saved searches, score new roles, update job_log.csv.'
            })
```

---

### 2.2 Python Script: RSS Feed Monitor

Several job boards publish RSS feeds. A simple Python script (`scripts/check_feeds.py`) can:
1. Fetch RSS from Devex, ReliefWeb, FAO, ImpactPool
2. Filter titles containing keywords from `data/search_terms.md`
3. Print or save new results to `data/new_jobs.md`

Run manually (`python scripts/check_feeds.py`) or via cron/GitHub Actions.

**Boards with RSS:** ReliefWeb (yes), Devex (yes), FAO (yes), ImpactPool (yes)

---

### 2.3 Static Site with GitHub Pages ✅ DONE

GitHub Pages is live at **https://ulfboge.github.io/giuseppe-dal-bosco/**

- `index.html` — professional profile page
- `jobs.html` — live job feed (see section 2.4 below)
- `.nojekyll` added to bypass Jekyll processing
- Custom domain (e.g. giuseppedalbosco.com) can still be added via one DNS record

### 2.4 Live Job Feed via Adzuna API ✅ DONE

`jobs.html` fetches real job postings on page load using the **Adzuna free API** (250 calls/day). This is more effective than RSS feeds (2.2) for this use case — no script to run, always current, works in any browser.

- 6 keyword searches × 9 countries = ~18 API calls per page load
- Client-side title relevance filter removes off-topic results
- Date-range toggle (Any time / Past month / Past week / Past 24 h)
- Countries covered: GB, DE, NL, FR, US, CA, ZA, AU, SG

RSS feeds (2.2) for Devex, ReliefWeb, ImpactPool, and FAO remain useful as a complement — those platforms are not covered by Adzuna.

---

## Tier 3 — Moderate Automation (Half-day setup)

### 3.1 Python + GitHub Actions: Automated Feed Check

Extend 2.2 to run automatically every weekday via GitHub Actions:
- Fetch RSS feeds
- Filter by keywords
- Create a GitHub Issue or commit results to `data/new_jobs.md` with date
- Only report jobs not seen before (track seen URLs in `data/seen_jobs.txt`)

Cost: Free (GitHub Actions free tier covers this easily).

---

### 3.2 Airtable or Notion Sync

Replace `job_log.csv` with a public-read Airtable base or Notion database. Embed a filtered view on the webpage (e.g. "roles I'm actively considering"). More visual, but adds a dependency.

**When to do this:** Only if manually updating the CSV becomes a friction point.

---

### 3.3 LinkedIn Job Alert Emails → Email Filter → Folder

Not code, but effective automation:
1. Set up LinkedIn Job Alerts for each saved search (LinkedIn sends weekly emails)
2. Create a Gmail filter: sender = `jobalerts@linkedin.com` → label "Job Search"
3. Review the folder weekly

Same for Devex, ReliefWeb, ImpactPool — all support email alerts.

---

## Tier 4 — Do Not Build Yet

The following are tempting but over-engineered for a personal job search:

- ❌ Full scraper (LinkedIn blocks scrapers; maintenance cost high)
- ❌ Automated scoring (requires AI API + context; easier to score manually in 3 minutes)
- ❌ CRM-style application tracker (Notion/Airtable is faster to set up than custom code)
- ❌ Personalised AI cover letter generator in the repo (use Claude/ChatGPT directly)

---

## Recommended Starting Point

1. Add `data/job_log.csv` now — start tracking from day one
2. Create saved searches on LinkedIn, Devex, ReliefWeb and paste URLs into `data/saved_searches.md`
3. Enable email alerts on all platforms
4. Enable GitHub Pages — takes 2 minutes
5. Add the GitHub Actions weekly reminder (copy-paste the YAML above)

That is a complete, low-maintenance system that will work for months without further investment.
