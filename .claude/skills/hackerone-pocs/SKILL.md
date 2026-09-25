---
name: hackerone-pocs
description: >-
  Reference library of real, publicly disclosed HackerOne vulnerability reports
  (POCs) mirrored in this repository, grouped into 119 weakness/CWE categories
  (8,670 report files). Use for defensive security research, learning a
  vulnerability class from real fixed bugs, finding disclosed examples of a bug
  type (XSS, SSRF, IDOR, SQLi, CSRF, RCE, auth bypass, etc.), studying reporter
  write-ups, or looking up severity/bounty context. Triggers on requests like
  "find HackerOne reports about <weakness>", "show real POCs for <bug class>",
  "examples of <vulnerability> from disclosed reports", or any question about the
  reports stored under weakness/ or jsonReports/.
---

# HackerOne Disclosed-Report POCs

This repository is a searchable, offline mirror of **publicly disclosed**
HackerOne reports, categorized by weakness type. Everything here is already
public (disclosed by the program and the researcher). Use it for **defensive
security, learning, and research** — understanding how real vulnerability
classes manifest, how researchers write them up, and how programs triaged and
paid them. Do not use it to target live systems.

## What's in the repo

```
weakness/<Category>/          119 categories, one folder per weakness type
  <report_id>.json            full HackerOne report JSON (one per report)
  index.md                    curated list: Title / URL / Severity / Reporter / Bounty
jsonReports/                  9,597 raw report JSONs (the full download pool)
reportLinksHackerOne          list of all report IDs
utils/                        scripts to (re)build the corpus and search it
```

Each report JSON has these useful fields:
- `title`, `url` (the hackerone.com/reports/<id> link), `weakness.name`
- `severity.score` / `severity_rating`, `formatted_bounty`
- `reporter.username`, `team.handle` (the program), `disclosed_at`
- `vulnerability_information` — **the actual write-up / POC text** (plain) and
  `vulnerability_information_html` (HTML version)
- `cve_ids`, `state`, `substate`

## How to use this skill

1. **Identify the weakness category.** Consult `references/catalog.md` — it lists
   all 119 categories with report counts and 3 representative reports each.
   Map the user's phrasing to a category name (e.g. "clickjacking" →
   `UI Redressing (Clickjacking)`, "open redirect" → `Open Redirect`,
   "prototype pollution / logic" → often under `Business Logic Errors` or
   `Violation of Secure Design Principles`).

2. **List the reports in that category.** Read `weakness/<Category>/index.md`
   for the full curated list (title, URL, severity, reporter, bounty).

3. **Read a specific write-up.** Open `weakness/<Category>/<id>.json` and read
   the `vulnerability_information` field for the researcher's POC/explanation.
   Quick extraction:
   ```bash
   jq -r '.title, .url, .severity.score, .formatted_bounty, "---", .vulnerability_information' \
     "weakness/SQL Injection/952501.json"
   ```

4. **Search across the corpus** when the category is unknown or you want to grep
   by keyword, program, reporter, CVE, etc. See `references/searching.md`.

## Guidance

- Prefer the curated `weakness/<Category>/` folders over `jsonReports/` — they're
  deduplicated and categorized. Fall back to `jsonReports/` only for a report ID
  not present under `weakness/`.
- When summarizing a report, cite the `url` so the user can read the original.
- Bounty/severity fields are frequently `null` (program didn't disclose them) —
  say "not disclosed" rather than treating null as zero.
- This corpus is a snapshot; it does not update itself. `utils/buildRepo.sh`
  re-downloads from public sources if the user wants a refresh.
- Keep the framing defensive: explain, teach, compare, and reference. Don't
  turn a disclosed write-up into an actionable attack against a specific live
  target.

## References

- `references/catalog.md` — all 119 categories, counts, representative reports.
- `references/searching.md` — grep/jq/script recipes for searching the corpus.
