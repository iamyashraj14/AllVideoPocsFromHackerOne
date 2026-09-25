# Injection techniques (distilled from disclosed reports)

Real patterns seen across `weakness/Cross-site Scripting*`, `SQL Injection`,
`Code Injection`, `Command Injection - Generic`, `OS Command Injection`,
`XML External Entities (XXE)`, `Deserialization of Untrusted Data`, and
`CRLF Injection`. Each pattern cites the report(s) that demonstrate it.

---

## Cross-Site Scripting (XSS)

**Root cause:** untrusted input reaches an HTML/JS/attribute/URL sink without
context-correct output encoding, or a sanitizer/filter is bypassable.

### Recurring patterns & bypasses
- **Reflected via a redirect/callback parameter.** `?kxsrc=…callback=alert(...)`
  reflected into a script context — *xss in www.uber.com* (report 145278).
- **SVG upload with XML entity to defeat an attribute allow-list.** An SVG that
  passes an element/attribute whitelist until an `<!ENTITY>` is added, after
  which `onload=` survives — *XSS via SVG icon whitelist bypass on Shopify*
  (232174). Treat uploaded SVG as active content.
- **Markdown → HTML parser confusion.** Odd interactions between `_` and `@`
  let an attacker emit a stray tag that accepts arbitrary attributes / event
  handlers — *Markdown parsing issue on HackerOne* (46916).
- **Mutation / filter-confusion payloads** against rich-text editors (TinyMCE):
  `'"><marquee><img src=x onerror=confirm(1)></marquee>…<plaintext/onmouseover=…>`,
  `data:text/html;base64,…` in `href`, drag-and-drop `setData('text/html',…)` —
  *Tinymce 2.4.0 on Shopify* (262230).
- **CSP present but HTML injection still lands** — attacker keeps arbitrary HTML
  for phishing/deanon while working on a CSP bypass — *XSS via DM deeplinks on
  twitter.com* (341908). Don't treat CSP as a substitute for encoding.
- **Encoding tricks in URL-ish fields**: `<<​/​<x>/script…><svg onload=…>` double
  bracket / broken-tag payloads (341908).

### DOM XSS (client-side sinks)
- **postMessage handler with weak origin check.** `~e.origin.indexOf("https://hq.upserve.com")`
  passes for `hq.upserve.com.attacker.com`; message data flows to `eval()` —
  *DOM XSS via postMessage on inventory.upserve.com* (603764). Check the whole
  origin against an allow-list; never `indexOf`/substring/regex-contains.
- **structured-clone bypass of postMessage escaping.** Escaping that assumes a
  string is bypassed by sending a clone-able object per the HTML5 structured
  clone algorithm — *XSS on Shopify digital_wallets dialog* (231053).
- **Chained DOM XSS**: cookie-stuffing → login CSRF → non-open redirect →
  `javascript:` navigation via `Shopify.API.setWindowLocation` postMessage event
  — *DOMXSS on Shopify Embedded SDK* (422043).
- **Common sinks to grep for:** `eval`, `innerHTML`, `document.write`,
  `location =`, `setWindowLocation`, `$(...).html(...)`, `postMessage` listeners
  without strict `event.origin` checks.

### Stored XSS
- Angular/expression-template injection in stored content:
  `{{(_="".sub).call.call({}[$="constructor"]...)()}}` stored and rendered on
  every doc page — *Stored XSS on developer.uber.com via readme.io* (131450).
- **Linkable-image markup re-enabling sanitized tags** (`{<img>}[link]`) allows
  `class`/`target` injection → full-page click hijack, phishing modal, reverse
  tabnabbing — *Stored XSS in RDoc wiki pages* (662287).

**Remediation:** context-aware output encoding; strict CSP as defense-in-depth;
sanitize on a strict allow-list (and re-test entity/mutation bypasses); validate
`postMessage` origin against an exact allow-list and never route message data to
`eval`/navigation; serve user uploads (SVG/HTML) from a sandboxed origin with
`Content-Disposition: attachment`.

---

## SQL Injection

**Root cause:** user input concatenated into SQL, or a "safe" abstraction
misused.

### Patterns
- **Blind boolean/time-based** via `sleep()` in a GET/JSON parameter:
  `city_id=(select(0)from(select(sleep(25)))v)` (786044);
  `topsort=followers or sleep(0.00…1)` where the injection is in a `WHERE` over
  many rows (295841); base64-wrapped JSON param dumping `user()`/db name a char
  at a time with `mid(user(),n,1)='c'#` (150156).
- **Vulnerable third-party/WordPress plugins** reachable unauthenticated —
  Formidable Pro preview via `admin-ajax.php?action=frm_forms_preview` +
  `[display-frm-data]` shortcode (273946); `q-and-a` plugin (135288).
- **Prepared-statement API misused.** Drupal `db_query(... IN (:name))` with a
  non-integer-keyed array (`'name'=>array('test) -- '=>...)`) breaks the
  placeholder expansion → pre-auth SQLi → RCE via crafted session (31756). A
  parameterized API is only safe when used as intended.

**Remediation:** parameterized queries / bound placeholders everywhere; least-
privilege DB accounts; keep third-party plugins patched and unauthenticated
endpoints locked down; don't build IN-lists from attacker-controlled keys.

---

## Command & Code Injection, SSTI

### OS command / argument (flag) injection
- **`--output=` / `--no-index` git flag injection.** A user-controlled `path`
  or `ref` passed to `git archive` / `git grep` is interpreted as a flag,
  giving arbitrary file **write** (overwrite `authorized_keys` → SSH → RCE) or
  arbitrary file **read** (`config.toml`) — GitLab *Gitaly path → RCE* (587854),
  *Search API `wiki_blobs` ref* (658013), *`blobs` scope* (682442). Any time
  attacker input becomes a CLI argument, guard against `--flag` injection
  (use `--` end-of-options, validate strictly).
- **Localhost command API.** EvoStream API on `localhost:7440` exposes a
  `launchprocess` command as SYSTEM → RCE if paired with an SSRF (544928).

### ImageMagick / Ghostscript ("ImageTragick")
- Image upload passed through an unpatched ImageMagick; a PostScript payload
  (`%!PS … /OutputFile (%pipe%<cmd>) … putdeviceprops`) runs via Ghostscript →
  reverse shell — *RCE on semrush logo upload* (403417), *RCE on kitcrm image
  upload* (422944). Disable PS/EPS/PDF/XPS coders in `policy.xml`; validate real
  image content; keep IM/GS patched.

### Server-Side Template Injection (SSTI)
- **Flask/Jinja2**: `{{ '7'*7 }}` → `7777777` in a profile-name → email; then
  `{{ ''.__class__.mro()[1].__subclasses__() }}` toward RCE — *uber.com Jinja2
  SSTI* (125980).
- **Node template**: `{{this}}` → `[object Object]`, `{{this.__proto__…}}` probes
  — *SSTI in Shopify Return Magic email templates* (423541). Probe strings that
  arithmetic-evaluate (`{{7*7}}`) reveal template evaluation of user input.

### Native code-execution class (memory-safety in language runtimes)
- mruby engine: use-after-free (`Array#to_h` shrinking array in `to_ary`,
  181321), TOCTTOU in `mrb_str_setbyte` (181893), type confusion in `Struct` /
  `wrap_decimal` / redefined exception classes (181879, 185051, 181871, 185041)
  → memory corruption → RCE. Callbacks into user code during a C operation that
  cached a length/pointer is the recurring root cause.

**Remediation:** avoid shelling out; if unavoidable use arg vectors (not shell
strings), `--` end-of-options, and strict input validation; never render user
input as a template; sandbox/patch media processors; fuzz language runtimes for
callback-reentrancy bugs.

---

## XML External Entities (XXE)

**Root cause:** an XML parser resolves external entities / external DTDs on
untrusted input.

### Patterns
- **Classic file read via error reflection.** `<!ENTITY file SYSTEM "file:///etc/passwd">`
  echoed back in an error message — *XXE on sms-be-vip.twitter.com SXMP* (248668,
  also confirmed outbound requests → SSRF).
- **XXE hidden inside "document" formats.** Any XML-based format is a vector:
  `sitemap.xml` in a site-audit spider (312543); OOXML — a `.pptx` is a zip,
  edit `ppt/tableStyles.xml` to add an external entity (334488); `.xlf`
  translation files (232614); Exchange `autodiscover.xml` (315837). File-upload
  and "import" features that parse XML are prime XXE surface.
- **Blind / OOB XXE** using an external DTD that triggers an outbound request to
  the attacker (334488, 315837).
- **Upload-restriction bypass → XXE.** Bypass an upload filter to place an XML,
  then get the server to parse it (`allow_file_type_list` tampering) —
  *XXE at ecjobs.starbucks.com.cn* (500515, severity 10.0).

**Remediation:** disable DOCTYPE/external entities and external DTD loading in
every XML parser (language-specific hardening); treat OOXML/SVG/`sitemap.xml`/
`autodiscover.xml` as untrusted XML.

---

## Insecure Deserialization

**Root cause:** untrusted bytes are deserialized into live objects / gadget
chains.

### Patterns
- **PHP `phar://` deserialization.** A crafted phar (any extension, uploaded as
  a "jpg") is triggered by a filesystem op (`getimagesize`, `file_exists`,
  `is_dir`) whose path an attacker controls → object injection → RCE. Vanilla
  Forums (410882 unauth, 407552, 410237), WooCommerce CSV importer (403083).
  Watch any FS call taking a user-controlled path — even read-only ones.
- **Ruby `Marshal`/YAML.** rubygems.org used `Psych.safe_load` for the spec but
  `YAML.load` (unsafe) on the checksum file, pivoted to `Marshal.load` → RCE —
  *RCE on rubygems.org* (274990). A partial safe-load is not safe.
- **Missing end-of-data check in a custom parser.** RLP transaction parser
  doesn't assert it consumed all bytes → attacker appends data that propagates &
  mines — *arbitrary data on blockchain* (396954).

**Remediation:** never deserialize untrusted data; use data-only formats (JSON)
with schema validation; in PHP disable phar stream wrapper / avoid FS calls on
user paths; in Ruby use `safe_load` everywhere; assert parsers fully consume
input.

---

## CRLF Injection / HTTP Response Splitting

**Root cause:** `\r\n` (`%0d%0a`) from user input reaches a response header /
outbound protocol.

### Patterns
- **Header/response splitting**: `…/path/%0d%0aSet-Cookie:foo` injects headers,
  enables cache-affecting response splitting — *CRLF on starbucks.com* (858650),
  *bitstrips VPN* (237357), Apache `mod_userdir` CVE-2016-4975 (409512).
- **CRLF in a library → SSRF.** `urllib` CRLF (Python bpo-35906) lets crafted
  packets hit an internal redis — report 590020.
- **SMTP header injection** via a reflected "monitor name" newline → mass
  arbitrary email (near-full phishing) — *newrelic Synthetics* (347439).
- **Homograph/newline link spoofing**: `fakewebsite.tw%0ditter.com` renders as
  one URL but hyperlinks as two — *Twitter tweet/DM link truncation* (712979).

**Remediation:** strip/reject CR/LF in anything used for headers, redirect
Locations, email headers, or outbound requests; use APIs that encode header
values.
