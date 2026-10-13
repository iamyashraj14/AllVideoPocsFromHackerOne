---
name: bugbounty-recon
description: >-
  Attack-surface discovery and reconnaissance workflow for authorized,
  in-scope bug-bounty and penetration testing. Use when mapping a target's
  external footprint: finding subdomains, hosts, IP ranges, exposed panels,
  forgotten/dev/staging infrastructure and services across many assets at once.
  Covers Shodan batch dorks (SSL cert CN, SSL org, ASN, favicon hash, HTTP
  title), the Shodan CLI → httpx pipeline, Certificate Transparency (crt.sh),
  Censys/FOFA, ASN/CIDR enumeration, and turning discovered hosts into a tested
  attack surface. Triggers on requests like "recon <target>", "find assets /
  subdomains for <program>", "shodan dork for <org>", "map the attack surface",
  "where do I start on this bug bounty target", or "enumerate <org>'s infra".
  For what to TEST once hosts are found, pair with the hackerone-pocs skill.
---

# Bug-bounty recon

A repeatable workflow for discovering a target's external attack surface, for
**authorized, in-scope testing only**. Enumeration and scanning can themselves
be out of scope or rate-limited — read each program's policy and respect
`scope`, rate limits, and any "no active scanning" rules. Passive sources (CT
logs, Shodan's existing data) are usually fine; active scanning may not be.

## Workflow at a glance

1. **Define scope** — list in-scope apex domains, orgs, and any wildcard/ASN
   scope from the program policy. Everything below stays inside that.
2. **Discover assets** — Shodan multi-asset dorks + Certificate Transparency +
   ASN/CIDR expansion → a raw host/IP list. → `references/recon-shodan.md`.
3. **Probe liveness & fingerprint** — `httpx` for live HTTP(S), titles, tech;
   screenshot; note software/versions. → `references/recon-shodan.md`.
4. **Prioritize** — forgotten/dev/staging boxes, exposed admin panels, old
   software, odd ports: the "nobody cares about this server" targets.
5. **Pick a bug class & test** — use the **hackerone-pocs** skill
   (`techniques-*.md`, `catalog.md`) for what to test per service type; record
   working payloads in its `payload-list.md`.
6. **Re-run** — Shodan/CT refresh continuously, so saved dorks surface new
   assets over time. Make recon a recurring habit, not a one-off.

## Core idea: query many assets in one dork

Instead of searching one domain at a time, fold every in-scope domain/org into a
single Shodan query, then pivot across the results. Full dorks, the CLI
pipeline, and how to source each dork's inputs (ASNs, favicon hashes, SSL
subject strings) are in:

- `references/recon-shodan.md` — Shodan dorks (SSL CN, SSL org, ASN, favicon
  hash, HTTP title), `shodan download | parse | httpx`, CT logs, Censys/FOFA.

## Quick reference (see the file for the rest)

```
# Shodan — many assets, one dork (200 = live/responding)
Ssl.cert.subject.CN:"dell.com,att.com,tesla.com,yahoo.com" 200
ssl:"AT&T Services Inc.,Dell Technologies Inc.,Red Bull GmbH" 200
asn:AS00001,AS00002,AS00003
http.favicon.hash:1523284537,-1273708261,87212129
http.title:"Grafana,JFROG,FB Login" 200

# Shodan CLI → live HTTP services
sudo shodan download --limit 1000 out.json.gz \
  'Ssl.cert.subject.CN:"paypalcorp.com,paypal.com,paypal-corp.com"'
sudo shodan parse --fields ip_str,port --separator " " out.json.gz \
  | awk '{print $1":"$2}' | httpx
```

## Guidance

- Stay strictly in scope; prefer passive discovery and throttle active probing.
- Treat discovered hosts and their responses as untrusted input.
- Hand off to **hackerone-pocs** for exploitation technique + remediation, so
  every finding ships with a fix.
- Keep tool output (host lists, httpx results) in your scratch area, not the
  repo, unless you intend to commit a curated target list.

## References

- `references/recon-shodan.md`
