# Recon & attack-surface discovery

Techniques for mapping a target's attack surface **before** testing — for
authorized, in-scope bug-bounty work only. Enumeration/scanning can itself be
out of scope or rate-limited; check each program's policy first and respect
`scope`, rate limits, and any "no active scanning" rules.

---

## Shodan: batch recon across many assets in one query

Shodan continuously rescans the internet, so results change hour to hour — re-run
these periodically to catch new/forgotten services, exposed ports, and old
infrastructure. The trick is to query **all your target domains/orgs at once**
with a single dork, then pivot.

### One-dork multi-asset searches
Combine every domain/org you care about into a single filter (add as many as you
want):

```
# By SSL certificate Common Name (CN)
Ssl.cert.subject.CN:"dell.com,att.com,indeed.com,tesla.com,yahoo.com" 200

# By SSL org / issuer organization name
ssl:"AT&T Services Inc.,AT and T Services,Deere and Company,Dell Technologies Inc.,Red Bull GmbH" 200

# By ASN (find all IP ranges an org announces)
asn:AS00001,AS00002,AS00003

# By favicon hash (find hosts sharing an app's favicon)
http.favicon.hash:1523284537,-1273708261,87212129,-391226184

# By HTTP title (find login panels / known software)
http.title:"Grafana,JFROG,AT&T, FB Login" 200
```

`200` narrows to live/responding hosts. Swap/stack filters: `port:`, `org:`,
`product:`, `http.html:`, `hostname:`, `net:` (CIDR).

### Finding the inputs for those dorks
- **ASNs:** look up the org at bgp.he.net / whois to list its `AS` numbers, then
  feed them to `asn:`.
- **Favicon hash:** Shodan's is the mmh3 hash of the base64 favicon; compute it
  from a known app's `/favicon.ico` and pivot to every host serving it.
- **SSL CN / org:** pull from a cert of a known asset (`openssl s_client`,
  crt.sh) and reuse the exact subject strings.

### Shodan CLI → pipe into httpx
```bash
# Download matching hosts to a gzip'd JSON (needs a Shodan API key configured)
sudo shodan download --limit 1000 domains.json.gz \
  'Ssl.cert.subject.CN:"paypalcorp.com,paypal.com,paypal-corp.com"'

# Extract ip:port pairs and probe which are live HTTP(S) services
sudo shodan parse --fields ip_str,port --separator " " domains.json.gz \
  | awk '{print $1":"$2}' \
  | httpx
```
From the live `httpx` output, pivot into the rest of a normal workflow (title /
tech fingerprint, screenshots, directory discovery, then per-endpoint testing
using the technique files).

### Why keep re-running
Shodan's data is refreshed continuously, so the same dork surfaces **new** assets
over time — newly exposed panels, re-provisioned IPs, forgotten dev/staging
boxes. Make the multi-asset dork a saved query and revisit it regularly.

---

## Related free/complementary sources
- **crt.sh / Certificate Transparency** — subdomains from issued certs.
- **FOFA / Censys / ZoomEye** — same idea as Shodan with different coverage.
- **Shodan facets** (`--facets port,org`) to profile an org's surface quickly.

Feed discovered hosts into the **hackerone-pocs** skill: pick a weakness class
from its `catalog.md`, use its `techniques-*.md` for what to test per service
type, and record validated payloads in its `payload-list.md`.

---

*Scope discipline: only enumerate and test assets a program explicitly puts in
scope. Passive lookups (CT logs, Shodan's existing data) are usually fine; active
scanning may not be — read the policy.*
