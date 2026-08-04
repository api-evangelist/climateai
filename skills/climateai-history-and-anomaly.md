---
name: Pull weather history and judge whether conditions are anomalous
description: >-
  Retrieve 30+ years of historical weather for a coordinate from ClimateAi LensConnect
  and compare it against the long-term climatology baseline to say whether a period was
  or will be unusual for that place and time of year.
api: openapi/climateai-weather-openapi.yml
base_url: https://api-prod.climate.ai/weather
operations:
  - getHistoryGrid
  - getClimatology
  - getStitchedForecastStatistics
generated: '2026-08-04'
method: generated
---

# History and anomaly detection

## When to use this

The caller asks a backward-looking or comparative question: "what did rainfall actually
do at this site last season", "was last July hot for this region", "is the coming month
unusual here". History alone answers the first; history *plus* climatology answers the
other two.

## Authenticate

```
X-Api-Key: <YOUR_API_KEY>
```

## Step 1 — history: `getHistoryGrid`

`GET /v2/history`

Covers 1995–present (30+ years), ERA5-backed with automatic gap-fill for the
ERA5-to-present lag. Data is fetched on demand — there is no pre-loading step.

| Parameter | Required | Notes |
|---|---|---|
| `lat`, `lon` | yes | WGS84; snapped to the 0.25° grid |
| `var` | no | Defaults to all non-derived variables — pass it explicitly |
| `start_date`, `end_date` | no | `YYYY-MM-DD`. Omit both and you get roughly the last 3 months |
| `granularity` | no | `daily` (default), `weekly`, `monthly` |
| `use_downscaling` | no | Default `true`; entitlement-gated |

Do **not** use the legacy `getHistory` for new work — it covers only a rolling ~366
days, is daily-only, has no date-range control, and returns errors for locations that
have not been pre-loaded.

## Step 2 — baseline: `getClimatology`

`GET /v1/climatology`

This is still a legacy-only endpoint; a flexible replacement is in development. It
returns the distribution of what is *typical* at that location and time of year,
computed over a **fixed 1993–2022 reference period** that does not roll forward with
each request.

Parameters: `lat`, `lon`, `var`, `granularity` (`daily` | `weekly` | `monthly`).

It returns the fixed quantile set `[0.05, 0.25, 0.50, 0.75, 0.95]` only — no mean, no
terciles.

## Step 3 — compare

Match the granularity across both calls, then place the observed (or forecast) value
against the climatology quantiles for the same day/week/month:

- above `q95` → extreme high for that place and time of year
- `q75`–`q95` → notably high
- `q25`–`q75` → within the normal middle half
- below `q05` → extreme low

For a *forward-looking* anomaly, replace step 1 with `getStitchedForecastStatistics`
and compare its `0.50` quantile against the climatology `0.50` for the same window.

## Rules that will bite you

1. **Align the reference frames.** Climatology is a fixed 1993–2022 window; history runs
   1995–present. Do not describe climatology as "the last 30 years" — it is a fixed
   period ClimateAi refreshes periodically.
2. **Aggregation is variable-aware** on both endpoints: precipitation and
   evapotranspiration are summed within the window, temperature/humidity/wind/solar are
   averaged. Compare like with like.
3. **Only complete weeks/months are returned.**
4. **Climatology has no mean.** If you need a central value, use `0.50`.
5. **Resolution may differ between calls** if one variable is downscalable and another
   is not. Check the response meta.

## Errors

`400` `VALIDATION_ERROR` for bad coordinates/slugs/dates; `404` when the cell, range or
variable has no data; `500` retryable with backoff; live `401` when the key is missing.
See `errors/climateai-problem-types.yml`.
