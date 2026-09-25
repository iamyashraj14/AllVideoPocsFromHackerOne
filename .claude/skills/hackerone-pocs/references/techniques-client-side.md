# Client-side & redirection techniques (from disclosed reports)

Distilled from `weakness/Cross-Site Request Forgery (CSRF)`, `Open Redirect`, and
`UI Redressing (Clickjacking)`. Each pattern cites the report(s) that
demonstrate it.

---

## Cross-Site Request Forgery (CSRF)

**Root cause:** a state-changing request is accepted using only ambient
credentials (cookies) without an unpredictable, per-request token or strict
same-origin enforcement.

### Patterns & bypasses
- **CSRF on the OAuth authorize endpoint** (no token / no `state`) lets an
  attacker bind their 3rd-party app to the victim's account → full API access —
  Periscope (215381), 37signals `launchpad` (850022). Always require and verify
  a `state`/CSRF token on authorize.
- **`.json`/`.xml` suffix bypasses the CSRF check.** `POST /authorization.json`
  skipped the authenticity-token check that `POST /authorization` enforced —
  37signals (850022). Apply CSRF protection uniformly across formats/routes.
- **Token present but not really validated.** Sign-up accepted an arbitrary
  `authenticity_token` value → business-data change (994504); tokens not bound
  per-action and `_method` override + token printed in HTML enabled CSRF when
  paired with an SOP/UXSS read (103787).
- **Token exfiltrated cross-origin.** A click handler for `data-method="post"`
  links sends the `authenticity_token` to the link's `href` even cross-origin →
  CSRF despite a strict CSP — HackerOne (47472). Also open-redirect leaking the
  token (see below, 49759).
- **Origin/Referer relied upon but not always sent.** Firefox/IE omit `Origin`
  on form posts, so an Origin-only defense is incomplete (103787).
- **Deeplink CSRF on mobile.** `pscp://user/<id>/follow` triggers a
  state-changing action from a link/QR — Periscope iOS (805073).

**Remediation:** unpredictable per-session (ideally per-action) CSRF tokens,
validated on **every** route and content-type; `SameSite` cookies; verify
`Origin` where present but don't rely on it alone; require `state` on OAuth;
never emit credentials/tokens to cross-origin targets; treat custom-scheme
deeplinks as CSRF-reachable.

---

## Open Redirect

**Root cause:** a redirect target is taken from user input without an allow-list.

### Patterns & bypasses
- **`next=` / login redirect** accepting any absolute URL — MoPub
  `?next=https://google.com`, and it also allowed `javascript:` URIs → XSS
  (683298); Upserve `/http://stanko.sh/` (469803).
- **OAuth `redirect_uri` per RFC 6749.** On a bad scope/param the server
  redirects back to a *registered-but-attacker* `redirect_uri` → open redirect by
  spec (26962). Prefer returning `400` over redirecting to an unvalidated URI.
- **Loose host validation bypasses.** hostname-only checks allow
  `https://whatever@victim.tv`; non-ASCII → `?` truncation after validation;
  path-only callbacks (`a/../home`) traverse — Digits/Periscope (108113, 110293).
  `subject=/hackerone.com@google.com/` and `%2Fhackerone.com.google.com` bypassed
  a naive filter (97948).
- **Open redirect that leaks credentials.** `messages/follow?recipient=/example.com`
  sent the `authenticity_token` off-site → full account takeover (49759). Open
  redirect is not always "low" — chained it can leak tokens/OAuth codes.

**Remediation:** redirect only to a server-side allow-list (or relative paths);
reject absolute URLs, `javascript:`/`data:` schemes, `@`, backslashes, encoded
traversal, and non-ASCII tricks; on OAuth do exact `redirect_uri` matching and
error out rather than redirect on invalid input.

---

## UI Redressing / Clickjacking

**Root cause:** a sensitive page can be framed and overlaid, so the victim's
clicks/keystrokes hit hidden framed UI.

### Patterns & bypasses
- **`X-Frame-Options: SAMEORIGIN` is bypassable** via nested framing
  `twitter.com → attacker.com → twitter.com`; `ALLOW-FROM` is unsupported by
  several browsers; JS frame-busters are defeated by `sandbox` iframes —
  *wormable clickjacking in Twitter player card* (85624), Periscope (591432).
  Use CSP `frame-ancestors 'self'` (CSP2) as the real control.
- **Framing sensitive widgets to exfiltrate data.** Framing a Twitter lead-gen
  card without XFO steals the victim's email/username on click (154963).
- **`sandbox="allow-forms"` disables JS confirmation but keeps forms working** →
  a transparent payment iframe auto-submits on a click (Coinbase, 54733).
- **Framing + phishing/redirect chains.** Truncated DM links + framing → credential
  capture + malicious OAuth app install, self-propagating (643274).
- **Reverse tabnabbing.** `target=_blank` without `rel="noopener"` lets the
  opened page rewrite `window.opener.location` (662287, RDoc wiki).

**Remediation:** `Content-Security-Policy: frame-ancestors 'self'` (plus XFO for
legacy) on all sensitive pages; don't rely on `SAMEORIGIN`/`ALLOW-FROM`/JS
frame-busters; require a real (JS-backed, not form-only) confirmation for
sensitive actions; add `rel="noopener noreferrer"` to `target=_blank` links.
