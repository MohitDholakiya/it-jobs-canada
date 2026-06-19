# IT Jobs Canada

Hourly snapshot of Canadian IT job postings, auto-refreshed by an automated pipeline.

## Files

- **`it_jobs_canada.xlsx`** — Excel workbook (formatted, with clickable URL column)
- **`it_jobs_canada.csv`** — CSV version of the same data
- `it_jobs_canada.xlsx` and `.csv` are overwritten every hour, on the half-hour.

## Columns

| Column | Description |
| --- | --- |
| Position Name | Job title |
| Company Name | Hiring company |
| Location (City, Province) | City and 2-letter province code, e.g. `Toronto, ON` |
| Posted date | Date the posting appeared (YYYY-MM-DD) |
| URL | Apply link (Google News redirect to LinkedIn / company ATS) |
| Source | Where it came from: `linkedin` (via Google News), `remotive`, `remoteok`, `authentic` |

## Sources

- **LinkedIn** — scraped via Google News RSS (LinkedIn has no public job RSS/API). 15 role-specific queries.
- **Remotive** — `remotive.com/api/remote-jobs`
- **RemoteOK** — `remoteok.com/api`
- **AuthenticJobs** — `authenticjobs.com/api`

Indeed is excluded — their RSS is gated behind Cloudflare and returns 404 to non-browser clients.

## Caveats

- LinkedIn URLs are Google News redirect URLs (`news.google.com/rss/articles/...`); click to be forwarded.
- Remote-friendly roles are included alongside on-site Canadian roles.
- The script caps at jobs posted within the last 14 days.
- Updates are idempotent — running it again just refreshes the file in place.

## Pipeline

Cron job `0dc7e214134f` runs the scraper hourly. Source: `hourly_jobs.py` in the Hermes skills directory.
