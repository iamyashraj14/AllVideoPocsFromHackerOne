# SSRF & server-side techniques (from disclosed reports)

Distilled from `weakness/Server-Side Request Forgery (SSRF)`, `Path Traversal`,
`Unrestricted Upload of File with Dangerous Type`, `HTTP Request Smuggling`, and
`Denial of Service`. Each pattern cites the report(s) that demonstrate it.

---

## Server-Side Request Forgery (SSRF)

**Root cause:** the server fetches a URL/host influenced by user input, reaching
internal services, cloud metadata, or the loopback/link-local range.

### Patterns & bypasses
- **Cloud metadata theft.** Point the fetch at `169.254.169.254` /
  `metadata.google.internal`. GCP's `/computeMetadata/v1beta1/` path returned
  tokens **without** the `Metadata-Flavor: Google` header, and `?alt=json`
  forced a JSON response a screenshot pipeline would render → root over all
  Shopify instances (341876). Block link-local; require metadata headers;
  disable legacy metadata endpoints.
- **DNS-rebinding ToCToU.** Validate host → resolves to a safe IP; the fetch
  re-resolves → attacker-controlled internal IP (low/zero TTL alternating DNS).
  GitLab `UrlBlocker` (541169). Resolve once and connect to that pinned IP, or
  re-validate the *connected* IP.
- **Redirect / URL-decode smuggling.** A URL-decoded `:hash` let attacker
  smuggle query params into a gravatar fetch, chaining open redirects
  (`secure.gravatar.com` → `i0.wp.com` → arbitrary host) to a full-read
  unauthenticated SSRF — GitLab Grafana `/avatar/:hash` (878779). Follow
  redirects with the same allow-list you applied to the first URL.
- **`Host`-header-driven outbound request.** `oauth_token_url` built from the
  request `Host` → blind SSRF (GitLab Jira OAuth, 398799).
- **Feature-driven "fetch a URL" sinks.** CarrierWave `remote_attachment_url=`
  survives import attribute-cleaning → server downloads an attacker URL on
  import (826361). Any "import from URL", avatar-by-URL, webhook, PDF/screenshot
  renderer, or metadata fetcher is SSRF surface.
- **Half-blind → full SSRF** in managed k8s cloud-controller-manager (776017).
- **CRLF-in-URL → SSRF** to internal redis (urllib bpo-35906, report 590020).

**Remediation:** deny-list is insufficient — use an allow-list of destinations,
resolve-and-pin the IP (defeat rebinding), block RFC1918/link-local/loopback,
re-validate on every redirect hop, strip credentials, require metadata headers /
disable legacy metadata, and isolate egress at the network layer.

---

## Path traversal / arbitrary file read & write

**Root cause:** attacker-controlled path components reach filesystem operations
without normalization/containment.

### Patterns
- **Traversal in a "copy/move" feature.** GitLab UploadsRewriter regex captures a
  `file` with no validation → `/uploads/<secret>/../../../../etc/passwd` copied
  when moving an issue → arbitrary read (827052).
- **Traversal in a cache key.** `cache: key: ../1/cache` + no server-side check
  lets a CI job read/poison another project's cache over HTTP (301432).
- **Symlink / crafted archive escapes install dir.** RubyGems `install_location`
  used `File.realpath` on the destination (the local link dir), so a symlink
  `link -> /tmp` plus `link/HACKED` writes outside (270072); a gem `name` of
  `../../../tmp/x` writes/overwrites arbitrary files (243156). Validate the final
  resolved path is inside the target, and reject symlinks/`..` in archives.
- **Page-cache traversal → RCE.** `actionpack-page_caching` unescapes the path
  and joins it, so encoded `..` writes the cache (attacker-named content) to an
  arbitrary path → RCE (519220).
- **Arbitrary file write via `..` autosimplification** in a Windows service
  reading an attacker-writable registry path, plus CRLF into the log content →
  DoS/EoP (682774).
- **Git flag injection for read/write** (`--output=`, `--no-index`): see
  `techniques-injection.md` (587854, 658013, 682442).

**Remediation:** canonicalize then verify the resolved path is within an allowed
base; reject `..` and absolute paths; refuse symlinks when extracting archives;
never derive filesystem paths from unvalidated user input.

---

## Unrestricted / dangerous file upload

**Root cause:** the server stores and then serves/executes a file whose type or
content it did not properly validate.

### Patterns
- **Extension/content-type bypass.** Save a PHP webshell as `.jpg` and upload as
  an avatar (823588); change extension to an allowed one (`.txt`) to bypass a
  client/one-sided filter (949295); HTML upload → stored XSS + `.php` shell →
  potential RCE (900179, 722919). Validate on the server, by real content, and
  restrict to a business-need allow-list.
- **Type-display spoofing → client RCE.** Slack "Create snippet" with a long
  name + a special character makes a `.BAT` render as a benign `.CSV`; victim
  clicks and runs it (833080). Don't let display metadata diverge from the real
  file type.
- **Upload as a stepping stone**: to XXE (500515), phar deserialization
  (403083/410882), or ImageMagick RCE (403417/422944) — see
  `techniques-injection.md`.

**Remediation:** server-side content validation; allow-list extensions/types;
store uploads off the app origin, non-executable, with `Content-Disposition:
attachment`; randomize names; never trust client-supplied type or filename.

---

## HTTP request smuggling (desync)

**Root cause:** a front-end proxy and back-end server disagree on where a request
ends (`Content-Length` vs `Transfer-Encoding`), poisoning the shared connection
for the next visitor.

### Patterns
- **CL.TE / TE.CL / TE+TE.** Send both `Content-Length` and a `Transfer-Encoding:
  chunked` (often obfuscated: `tabprefix1`, a second invalid `Transfer-Encoding:
  foo`, `Transfer-encoding: identity`), so one server uses CL and the other TE —
  Slack `slackb.com` mass cookie theft (737140), Zomato `api.zomato.com` token
  theft (771666), New Relic login (498052), 37signals (867577), Basecamp cache
  poisoning (919175), labs.data.gov (726773).
- **Impact escalation.** A smuggled `GET https://<collab> HTTP/1.1` or
  `X-Forwarded-Host: attacker` makes the back-end 301-redirect victims (with
  their cookies) to attacker, or poisons a cache to make it persistent. Tools:
  `smuggler`, Burp Turbo Intruder scripts (seen throughout).

**Remediation:** normalize/reject ambiguous requests at the edge; reject messages
with both CL and TE; use HTTP/2 end-to-end where possible; ensure front-end and
back-end share identical parsing; disable connection reuse to untrusted
back-ends.

---

## Denial of Service

**Root cause:** untrusted input drives unbounded resource use or crashes a
runtime.

### Patterns
- **Runtime crashes / infinite loops from crafted input.** mruby segfaults and
  parser infinite loops from small valid/invalid programs (181828, 183356,
  182484, 187305) — sandboxes that run untrusted code inherit the host's crashes.
- **Type-confusion crashes** from redefining runtime classes/macros (185041,
  181871). These overlap with the RCE class in `techniques-injection.md`.
- **Amplification / unbounded work** — see category
  `Allocation of Resources Without Limits or Throttling` in `catalog.md`.

**Remediation:** resource limits/timeouts/quotas on any untrusted-input path;
run untrusted code in a crash-isolated, resource-capped sandbox separate from the
parent process; fuzz parsers; rate-limit expensive endpoints.
