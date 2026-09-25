# Access control, auth & business-logic techniques (from disclosed reports)

Distilled from `weakness/Insecure Direct Object Reference (IDOR)`,
`Improper Access Control - Generic`, `Improper Authorization`,
`Improper Authentication - Generic`, `Privilege Escalation`, and
`Business Logic Errors`. Each pattern cites the report(s) that demonstrate it.

---

## Insecure Direct Object Reference (IDOR) / Broken Object-Level Authorization

**Root cause:** the server acts on an object ID from the request without
checking the current user owns/may access that object.

### Patterns
- **ID in the request body, not just the URL.** New Relic `PUT …/dashboards/687944/filter`
  with `{"dashboard_id":687944,…}` — changing the body `dashboard_id` edits any
  account's dashboard because that field isn't validated against the path/session
  (459443). Check every identifier in *every* part of the request (body, headers,
  path).
- **Sequential / guessable IDs** that are "not secret" enable account linking:
  attacker sets `customer[uid]=VICTIM_ID` on an account-update to link accounts →
  destroy/buy subscriptions with victim's card — *customers.gitlab.com* (674195).
- **Entity IDs accepted cross-account.** Creating an alert condition on another
  account's `monitor_id`/entity (462321), or harvesting names via a Synthetics
  permissions view that skips the fix applied elsewhere (267636).
- **Predictable resource links** (certificate-warning URLs
  `?<counter>_kis_cup_<GUID>`) let a site forge privileged actions — Kaspersky
  (469372).
- **IDOR via import/rewrite features:** see path traversal in
  `techniques-ssrf-and-server.md` (GitLab UploadsRewriter 827052; upload
  overwrite by known `secret`+`filename` 534794).

**Remediation:** enforce per-object authorization server-side on every mutating
and reading endpoint; scope queries by the session's user/tenant; treat all
client-supplied IDs (including in bodies/headers) as untrusted; unguessable IDs
are hardening, not authorization.

---

## Broken authentication / auth bypass

### Patterns
- **`Host` header poisoning of OAuth redirect.** Changing `Host:` to
  `attacker.com/www.periscope.tv` makes the server build the OAuth redirect to
  the attacker → token theft → account takeover — *Periscope/Twitter* (317476).
  Also GitLab used `Host` to build `oauth_token_url` → blind SSRF (398799).
- **Unauthenticated password reset / state machine skip.** Uber
  `/rt/users/passwordless-signup` accepts `state:"CREATE_NEW_PASSWORD"` with a
  new password for any phone number → takeover (143717).
- **SAML/SSO plugin trust flaws.** OneLogin WP plugin auto-provisions a user
  from an attacker-supplied SAML assertion (no real auth), guess role
  `administrator` → admin (136169). Verify assertion signatures & don't
  auto-create privileged users.
- **OAuth `callback_url` / callback-locking bypass.** Path-only callbacks
  (`a/../home`) pass validation then traverse; non-ASCII → `?` after validation
  bypasses host checks; hostname-only checks allow `https://whatever@victim` —
  Digits/Periscope (110293, 110467, 108113). See also open redirect.
- **Session cookie disclosure = takeover.** A leaked session cookie from another
  report gave staff-level access (745324); `/skills` call disclosed all submitted
  reports (188719).

### Session / impersonation
- **Impersonation session not bound.** GitLab admin "impersonate" creates a
  session the impersonated user can see in *Active sessions*, copy, then click
  "Stop impersonating" to become admin — privilege escalation to admin (493324).
  Impersonation sessions must be isolated and non-transferable.

**Remediation:** never trust `Host`/`X-Forwarded-*` for security decisions or
URL building; enforce full state machines on sensitive flows (reset, email
change); validate SAML/OAuth signatures and redirect URIs strictly (exact
allow-list); bind sessions to their principal; rotate/scope tokens.

---

## Privilege escalation

### Patterns
- **Email-confirmation bypass → account takeover.** Race condition between an
  email-validation endpoint and an email-change (no DB transaction) confirms an
  arbitrary (victim) email → take over store/collaborator (300305); a Burp
  match-and-replace sequence to verify any `.myshopify.com` email → takeover
  non-SSO accounts (910300).
- **Mass-assignment of EE-only params.** Passing `use_custom_template` +
  `group_with_project_templates_id` + `template_name` to project-create copies
  private repos/issues/snippets from a template project — GitLab (689314). Lock
  down permitted params per role.
- **CI token confusion.** Mirror + "trigger pipelines for mirror updates" +
  making the victim an owner runs jobs as the victim using their `CI_JOB_TOKEN`
  → steal private repos (894569).
- **Local priv-esc via trusted `$PATH` / setuid.** keybase-redirector (setuid
  root) calls `fusermount` by relative path, trusts `$PATH` → root (426944);
  keybase XPC helper exposes `move`/`remove`/`createDirectory` as root (397478).
  Use absolute paths, sanitize env, authorize every privileged IPC method.
- **Subdomain takeover.** Dangling CNAME to an unclaimed cloud resource
  (`*.trafficmanager.net`) lets anyone serve content on the subdomain —
  Starbucks (383564). Audit/remove stale DNS records.

**Remediation:** transactional, idempotent sensitive flows (no races);
role-scoped mass-assignment allow-lists; scope CI/build tokens; harden setuid
binaries and privileged IPC; continuous dangling-DNS monitoring.

---

## Business-logic errors

**Root cause:** individually valid operations combine or sequence into an
unintended, exploitable state — no single "vuln" line of code.

### Patterns
- **Race conditions** on state transitions (email confirm/change, 300305) — same
  primitive as many takeovers.
- **MiTM of a local companion protocol.** Shopify PoS listens on `0.0.0.0` and
  puts the wifi IP in the QR connection string → session takeover on the LAN
  (423467). "Expected to work offline" is not a security boundary.
- **Weak format/spec validation.** Accepting non-conforming UUIDs
  (`zzzzzzzz-…`) because a regex was too loose bypassed a prior fix (423073).
- **Smart-contract economic logic (DeFi/MakerDAO).** Shutdown (`end.cage`)
  doesn't stop the savings `pot`, so DAI can still be minted after the final
  rate is fixed → drain collateral (672664); unsynchronized `drip` between
  `jug`/`pot` lets one transaction earn risk-free interest → inflation (665798).
  Model *economic* invariants, not just per-call access control.

**Remediation:** define and test system invariants across sequences and
concurrency; fuzz state machines; treat "offline"/LAN and client-side
assumptions as attacker-reachable; validate formats exactly; for contracts,
review global economic invariants and shutdown/settlement paths.
