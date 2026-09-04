# Aptronix Service — Executive Dashboard (simple / no access tiers)

This is the **interim, single-link setup** — everyone with the URL sees
everything, no login required. Good for getting back up and running
quickly; the tiered access-control version (Admin / Area Manager / Centre
Manager, gated by Cloudflare Access) is a separate, more involved setup you
can move to whenever you're ready — ask for it again and I'll walk you
through it, same as before.

## How it works

```
source/master.xlsx  →  scripts/build_data.py  →  data.json  →  index.html
   (you edit this)      (runs automatically)     (generated)   (reads this)
```

1. Edit `source/master.xlsx`, push.
2. The GitHub Action (`.github/workflows/update-dashboard.yml`) rebuilds
   `data.json` and commits it back automatically.
3. GitHub Pages redeploys on every commit.

## Set up GitHub Pages (one time)

1. **Settings → Pages** in this repo.
2. **Source: Deploy from a branch** → **Branch: main**, folder **/ (root)**.
3. Save. Your site publishes at `https://<your-username>.github.io/<repo-name>/`
   within a minute or two.

## Updating data

Just replace `source/master.xlsx` and push — the rest happens automatically.
If you ever push a change and don't see it reflected, check the **Actions**
tab for a green checkmark before assuming something's broken; that's the
single most useful thing to check.

## Setting a License Target

Licenses are tracked as both **revenue** and a plain **unit count** (how
many licenses sold), and the target is a unit count — "sell 40 licenses,"
not a rupee figure. To add it, create a new sheet named exactly
**"License Target"** with the same layout as the existing "Revenue Target"
sheet:

- Row 4: `Branch ID` in column A, then one column per month (e.g. `Apr 24`,
  `May 24`, …)
- Row 5 onward: one row per centre, with the target **count** in each
  month's column (e.g. `40`, not `₹40` or `40L`)

You don't need to fill in every centre or every month — any blank cell is
just treated as "no target set for that centre/month," and both the
Targets tab and the Licenses tab will show real sales figures for those
centres regardless, just without an achievement percentage until a target
exists.

## Quick date filters (Today / WTD / MTD)

Three buttons at the top of the filter bar set the date range to today,
week-to-date (Monday through today — Sunday's a closed day), or
month-to-date. They apply everywhere, not just one tab, since they just
set the same date range you'd otherwise pick by hand.

## Note on privacy

This setup has **no access control** — GitHub Pages on a public repo means
anyone with the link sees everything, including via browser dev tools. If
that's a problem for your data, the tiered Cloudflare setup is the answer
whenever you're ready for it.
