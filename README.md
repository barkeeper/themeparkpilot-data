# Theme Park Pilot — public data mirror

Daily-updated thrill-data.com crowd calendars + (later) historical
wait-time aggregates, mirrored by a GitHub Actions workflow in
[barkeeper/themeparkpilot](https://github.com/barkeeper/themeparkpilot).

## Why a separate repo

The main Theme Park Pilot repo is private. The Flutter app reads
these JSONs via `raw.githubusercontent.com`, which only serves
content from PUBLIC repos. Splitting the mirror into its own
public repo lets the app fetch without baking any auth token.

## Layout

```
data/
├── index.json                              # which parks have data
└── parks/
    └── <wikiId>/
        └── calendar.json                   # per-park 365-day crowd
```

`<wikiId>` is the themeparks.wiki externalId (e.g. `MagicKingdomPark`).

## Schema

`data/index.json`:

```json
{
  "generatedAt": "2026-05-12T03:00:00Z",
  "scraperVersion": "1.0.0",
  "parks": {
    "MagicKingdomPark": {
      "thrillDataSlug": "magic-kingdom",
      "lastUpdated": "2026-05-12T03:00:00Z",
      "hasCalendar": true,
      "dayCount": 365
    }
  }
}
```

`data/parks/<wikiId>/calendar.json`:

```json
{
  "parkExternalId": "MagicKingdomPark",
  "thrillDataSlug": "magic-kingdom",
  "sourceUrl": "https://www.thrill-data.com/trip-planning/crowd-calendar/magic-kingdom",
  "generatedAt": "2026-05-12T03:00:00Z",
  "days": [
    { "date": "2026-05-13", "crowdPercent": 53.3, "predicted": true }
  ]
}
```

## Updates

Updated daily at 03:00 UTC by the `thrill-data-scrape.yml` workflow
in the main repo. PRs to this repo are NOT accepted — the data is
machine-generated.

## License

Data is derived from public thrill-data.com pages; treat it as
"informational only, no warranty". Crowd-level / wait-time numbers
are best-effort predictions, not facts.
