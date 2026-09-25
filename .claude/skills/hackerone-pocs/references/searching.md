# Searching the POC corpus

All reports are plain JSON, so standard tools work. Run these from the repo root.

## By weakness category (fastest)

Categories are folders under `weakness/`. List them and their sizes:

```bash
for d in weakness/*/; do printf '%5d  %s\n' "$(ls "$d"*.json 2>/dev/null | wc -l)" "$d"; done | sort -rn
```

Full list of reports in one category:

```bash
cat "weakness/Server-Side Request Forgery (SSRF)/index.md"
```

## By keyword in the write-up

Search the `vulnerability_information` text (and everything else) across a
category or the whole corpus:

```bash
# within one category
grep -rli "prototype pollution" "weakness/Code Injection/"

# across all categorized reports
grep -rli "graphql" weakness/ | head
```

## Structured queries with jq

```bash
# Title + URL + severity + bounty for one report
jq -r '.title, .url, .severity.score, .formatted_bounty' "weakness/Open Redirect/<id>.json"

# All reports in a category with a bounty over $1000
for f in "weakness/SQL Injection/"*.json; do
  jq -r 'select((.bounty_amount // "0")|tonumber > 1000)
         | "\(.formatted_bounty)\t\(.title)\t\(.url)"' "$f"
done

# Reports mentioning a CVE
for f in weakness/*/*.json; do
  jq -e '.cve_ids | length > 0' "$f" >/dev/null 2>&1 && \
    jq -r '"\(.cve_ids|join(","))\t\(.title)\t\(.url)"' "$f"
done

# Reports for a specific program (team handle)
grep -rl '"handle":"gitlab"' weakness/ | head
```

## Using the repo's own search script

`utils/searchIntoJson.sh` searches by JSON key/value (needs `gron` for -s/-r):

```bash
cd utils
./searchIntoJson.sh -k                       # list all available JSON keys
./searchIntoJson.sh normal weakness.name     # files containing that key (grep-based)
./searchIntoJson.sh search weakness.name ssrf  # key=value match (requires gron)
./searchIntoJson.sh raw   weakness.name        # raw values for a key (requires gron)
```

## Tips

- `severity.score`, `formatted_bounty`, and `bounty_amount` are often `null`;
  guard `tonumber` conversions with `// "0"`.
- `weakness/<Category>/index.md` is the human-readable summary; the `.json`
  files hold the full data including the POC write-up.
- For a report ID that isn't under `weakness/`, check `jsonReports/<id>.json`.
