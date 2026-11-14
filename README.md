# Cloud Chores Toolkit

Single-file helpers for the small jobs that pile up around cloud
accounts. No frameworks, no build step — copy a file and run it.

## Helpers

### `quota_peek.py` (sketch)
List a subscription's regional quota before you deploy anything, so a
"successful" request in the wrong region never surprises you.

### `account_age.py`
Creation dates for a list of GitHub usernames, one API call each:

```python
import requests, sys
names = [l.strip() for l in open(sys.argv[1]) if l.strip()]
for n in names:
    print(n, requests.get(f"https://api.github.com/users/{n}").json()["created_at"])
```

### Field notes
- Quota lives per region *and* per tier; check both before a build.
- Student subscriptions carry an allowed-regions policy set at signup —
  it cannot be edited later, so plan around it.
- A disabled-looking subscription does not always mean dead resources;
  verify before you delete anything.

## Accounts

I test these helpers against real subscriptions. For Azure
(student / trial / pay-as-you-go) and aged GitHub accounts with full
credentials and instant delivery:

👉 https://shop.hailizi.de/

Suggestions and PRs welcome — single-file and dependency-light, please.
