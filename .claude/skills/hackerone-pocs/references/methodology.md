# Cross-cutting patterns & defensive review checklist

Observations that recur across the whole corpus, independent of any single
weakness category. Useful for teaching, threat modeling, and code/design review.

## The corpus at a glance

- **119 weakness categories, 8,670 report files.** The mass is in a handful of
  classes: Information Disclosure (1,019), XSS-Generic (915), Violation of Secure
  Design Principles (723), Improper Authentication (610), CSRF (416), Stored XSS
  (415), DoS (357), Reflected XSS (324), Privilege Escalation (320), Memory
  Corruption (314), Improper Access Control (293), Open Redirect (261). Full
  breakdown in `catalog.md`.
- **Where the big bounties cluster:** memory-safety/RCE in language runtimes
  (mruby $18–20k), SSRF to cloud metadata/root ($25k), business-logic &
  auth/account-takeover ($10–25k), git-flag-injection & template-injection RCE
  ($10–15k), request-smuggling mass cookie/token theft ($5–6.5k).

## Recurring meta-patterns

1. **Chaining beats single bugs.** The highest-impact reports are chains:
   open redirect → token leak → account takeover; SSRF → metadata token → cloud
   root; cookie-stuffing → login CSRF → redirect → DOM XSS; upload → phar/XXE/
   ImageMagick → RCE. Rate a "low" finding by what it unlocks, not in isolation.
2. **Validate-then-use gaps (TOCTOU).** DNS re-resolution after an IP check
   (SSRF), array length cached before a callback (mruby), email validate vs
   change race (takeover), impersonation session reuse. Any check separated in
   time from the use it guards is suspect.
3. **Trusting request-controlled context.** `Host`/`X-Forwarded-*` used to build
   URLs or make security decisions (OAuth redirect, SSRF, cache poisoning) shows
   up again and again. Request metadata is attacker-controlled.
4. **"Safe" abstraction used unsafely.** Parameterized SQL with attacker-keyed
   arrays; `safe_load` on one path but `YAML.load` on another; allow-list SVG
   filter defeated by an XML entity; a partial fix bypassed by a loose regex or a
   sibling endpoint (`.json` suffix). A safe API is only safe when used correctly
   and uniformly.
5. **Format/type confusion at boundaries.** OOXML/SVG/sitemap = XML (XXE); phar
   masquerading as jpg (deserialization); `.BAT` shown as `.CSV` (upload);
   structured-clone object vs string (postMessage). Anywhere a parser or a
   display disagrees with the real bytes is a bug source.
6. **Identifiers trusted from the wrong place.** IDs in the request body/headers,
   not just the URL, routinely skip authorization (IDOR).
7. **Client-/LAN-/offline-side assumptions.** PoS on `0.0.0.0`, "expected to work
   offline", client-side upload filters, JS frame-busters — none are security
   boundaries.

## A defensive review checklist (mapped to the technique files)

When reviewing code, a design, or an endpoint, ask:

- **Input → dangerous sink?** HTML/JS/attribute (XSS), SQL (SQLi), shell/CLI args
  (command & flag injection), template (SSTI), XML parser (XXE), deserializer,
  response header (CRLF), filesystem path (traversal). → `techniques-injection.md`,
  `techniques-ssrf-and-server.md`.
- **Server fetches a URL/host from input?** Metadata/loopback/rebinding/redirect
  bypasses. → `techniques-ssrf-and-server.md`.
- **Every object access authorized server-side**, for IDs in body/headers/path,
  per tenant/user? → `techniques-access-control.md`.
- **Sensitive flows** (login, reset, email/role change, OAuth, impersonation)
  transactional, signature-verified, redirect-URI allow-listed, state-validated,
  race-free? → `techniques-access-control.md`.
- **State-changing requests** carry a validated CSRF token on every route/format,
  with `SameSite`? Redirects allow-listed? Sensitive pages `frame-ancestors`? →
  `techniques-client-side.md`.
- **Uploads** validated by real content, stored non-executable off-origin? →
  `techniques-ssrf-and-server.md`.
- **Untrusted input can exhaust resources or crash a runtime?** Limits, timeouts,
  crash isolation. → `techniques-ssrf-and-server.md` (DoS).
- **Front-end/back-end parse requests identically** (no CL/TE ambiguity)? →
  `techniques-ssrf-and-server.md` (smuggling).
- **Dangling DNS / unclaimed cloud resources** for any subdomain? →
  `techniques-access-control.md` (subdomain takeover).

## Using the corpus while reviewing

To pull real precedents for whatever you're reviewing:

```bash
# real examples of a pattern in the write-ups
grep -rli "dns rebinding\|toctou\|time of check" weakness/ | head
# highest-impact reports in a class (by bounty)
for f in "weakness/Server-Side Request Forgery (SSRF)/"*.json; do
  jq -r 'select((.bounty_amount//"0")|tonumber>0) | "\(.bounty_amount)\t\(.title)\t\(.url)"' "$f"
done | sort -rn | head
```

See `searching.md` for more recipes and `catalog.md` for the category map.
