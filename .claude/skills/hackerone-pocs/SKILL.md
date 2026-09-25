---
name: hackerone-pocs
description: >-
  Comprehensive, technique-level knowledge base distilled from real, publicly
  disclosed HackerOne vulnerability reports (POCs) mirrored in this repository —
  119 weakness/CWE categories, 8,670 report files. Use for defensive security
  research, learning how a vulnerability class actually manifests and gets
  exploited in the wild, recognizing vulnerable code/config patterns, reviewing
  code or designs for a bug class, explaining root causes and remediations, and
  finding disclosed real-world examples (XSS, SSRF, IDOR, SQLi, CSRF, RCE/SSTI,
  XXE, deserialization, request smuggling, auth bypass, privilege escalation,
  business-logic, path traversal, open redirect, clickjacking, info disclosure,
  and more). Triggers on requests like "how does <bug class> work with real
  examples", "find HackerOne reports about <weakness>", "review this for <bug
  class>", "what are common <weakness> bypasses", or any question about the
  reports under weakness/ or jsonReports/.
---

# HackerOne Disclosed-Report POCs — Technique Knowledge Base

This repository is an offline mirror of **publicly disclosed** HackerOne
reports (POCs), categorized by weakness type. Everything here is already public.
Use it for **defensive security, learning, code review, and research**:
understanding how real vulnerability classes arise, recognizing the vulnerable
patterns, and citing concrete disclosed examples. Do not use it to attack
systems you are not authorized to test.

The `references/` files below are **distilled from the actual write-ups** in
this corpus — each recurring technique is tied to the real reports that
demonstrate it (by title and `hackerone.com/reports/<id>` URL).

## Repository layout

```
weakness/<Category>/          119 categories, one folder per weakness type
  <report_id>.json            full HackerOne report JSON (one per report)
  index.md                    curated list: Title / URL / Severity / Reporter / Bounty
jsonReports/                  9,597 raw report JSONs (the full download pool)
reportLinksHackerOne          list of all report IDs
utils/                        scripts to (re)build the corpus and search it
```

Key JSON fields: `title`, `url`, `weakness.name`, `severity.score`,
`formatted_bounty`, `reporter.username`, `team.handle` (program),
`vulnerability_information` (**the write-up / POC**), `cve_ids`, `disclosed_at`.

## How to use this skill

- **To explain or teach a bug class** (with real examples), or **review code /
  a design** for it → read the matching technique reference below. Each lists
  root-cause patterns, real disclosed examples, recurring bypass tricks, and
  remediation.
- **To find disclosed reports for a category** → `references/catalog.md` maps
  all 119 categories to report counts and representative reports; then open
  `weakness/<Category>/index.md` for the full list.
- **To read one write-up** → open `weakness/<Category>/<id>.json` and read
  `vulnerability_information`:
  ```bash
  jq -r '.title, .url, .severity.score, .formatted_bounty, "---", .vulnerability_information' \
    "weakness/SQL Injection/<id>.json"
  ```
- **To search across the corpus** by keyword / program / CVE → `references/searching.md`.

## Technique references (distilled from the reports)

- `references/techniques-injection.md` — XSS (reflected/stored/DOM, mutation,
  SVG/markdown, postMessage), SQL injection, command/code injection, SSTI,
  ImageMagick/Ghostscript, git flag injection, XXE, insecure deserialization
  (incl. PHP phar), CRLF/response splitting.
- `references/techniques-access-control.md` — IDOR, broken access control,
  authorization/authentication bypass, OAuth/SAML flaws, session issues,
  privilege escalation, subdomain takeover, business-logic abuse (race
  conditions, smart-contract econ bugs).
- `references/techniques-ssrf-and-server.md` — SSRF (cloud metadata, DNS-rebind
  ToCToU, blocklist/redirect bypasses, blind SSRF), path traversal / arbitrary
  file read & write, unrestricted file upload, HTTP request smuggling, DoS.
- `references/techniques-client-side.md` — CSRF (token/Origin gaps, OAuth-CSRF,
  `.json` suffix bypass), open redirect (OAuth `redirect_uri`, `next=`), UI
  redressing / clickjacking, reverse tabnabbing.
- `references/methodology.md` — cross-cutting patterns the corpus keeps showing:
  chaining low-severity bugs into criticals, where high-bounty bugs cluster,
  recon habits, and a defensive review checklist.

## Guidance

- Prefer the curated `weakness/<Category>/` folders over `jsonReports/`.
- When you cite a technique, name the real report and its `url` so the user can
  read the original write-up.
- `severity.score` / `formatted_bounty` are often `null` (not disclosed) — say
  "not disclosed" rather than treating null as zero.
- Keep the framing defensive: explain, teach, recognize, remediate. Don't turn a
  write-up into an operational attack against a specific live target.
- This corpus is a snapshot; `utils/buildRepo.sh` re-downloads from public
  sources if a refresh is wanted.

## References

- `references/techniques-injection.md`
- `references/techniques-access-control.md`
- `references/techniques-ssrf-and-server.md`
- `references/techniques-client-side.md`
- `references/methodology.md`
- `references/catalog.md` — all 119 categories, counts, representative reports.
- `references/searching.md` — grep/jq recipes for querying the corpus.
