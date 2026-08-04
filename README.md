# State of US Trade

Monthly dispatch on US goods trade — imports, exports, tariffs, and AI-related
products — published as a swipeable web report and served from GitHub Pages.

**Live:** https://tradewartracker.github.io/state-of-us-trade/
**Archive:** https://tradewartracker.github.io/state-of-us-trade/archive.html

Part of [tradewartracker.com](https://www.tradewartracker.com).

## What's in here

This repo is **publish-only**. It holds built output, no source code.

```
docs/
  index.html      always a copy of the most recent edition
  archive.html    list of all editions
  2026-06.html    June 2026  (issue 06)
  2026-05.html    May 2026   (issue 05)
  2026-04.html    April 2026 (issue 04)
  2026-03.html    March 2026 (issue 03)
```

Each edition is a single self-contained HTML file (~43KB) — charts are inline
SVG, there are no external assets and no CDN dependencies, so a file works
offline and can be dropped on any static host.

## Where it comes from

Built by the `trade-miner` pipeline (`C:\heroku\trade-miner`, not public) from
the US Census Bureau FT900 monthly release:

```
python -m miner.synthesis      # writes brief.json for the month
python -m miner.flipbook       # renders flipbook.html
```

Prior months regenerate with `--asof YYYY-MM`.

## Monthly update

1. Run the miner for the new month (see the trade-miner `RUNBOOK.md`).
2. Copy `output/state-of-us-trade/<month>/flipbook.html` → `docs/<month>.html`.
3. Copy that same file over `docs/index.html`.
4. Add a row to `docs/archive.html`.
5. Commit and push — Pages redeploys automatically.

## tradewartracker.com

The site (Weebly) **links out** to these pages rather than embedding them — the
deck is full-viewport and never scrolls, so it does not survive a fixed-height
iframe, worst on mobile.

- `weebly-embed.html` (repo root, not published) is a promo card to paste into a
  Weebly **Embed Code** element. Evergreen — no month or figures — so it never
  needs editing when a new edition ships.
- The nav entry is a Weebly page of type **External Link** pointing at
  `archive.html`.

## Notes

- Back editions are computed from the **current** data vintage, so they include
  Census revisions and can differ slightly from what the figures were on the
  original release day.
- The tariff rate shown is an **implied effective rate**: customs duties divided
  by import value.

Source: US Census Bureau. Nothing here is auto-posted.
