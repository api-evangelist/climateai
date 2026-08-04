---
name: Forecast weather and climate risk for a location
description: >-
  Get a probabilistic weather forecast for any coordinate on Earth from ClimateAi
  LensConnect — from today through roughly six months — as either summary statistics or
  raw ensemble members, at the granularity you need.
api: openapi/climateai-weather-openapi.yml
base_url: https://api-prod.climate.ai/weather
operations:
  - getStitchedForecastStatistics
  - getStitchedForecast
generated: '2026-08-04'
method: generated
---

# Forecast a location

## When to use this

The caller wants a forward-looking weather or climate signal for a specific place —
"how much rain will this field get over the next six weeks", "what's the temperature
outlook for this port through the season". One call covers the whole horizon; you do not
need to stitch short-term, subseasonal and seasonal together yourself.

## Authenticate

Every request carries the key in a header. There is no OAuth, no token exchange, no
scope model.

```
X-Api-Key: <YOUR_API_KEY>
```

Keys are not self-service — they are provisioned by ClimateAi
(`sales@climate.ai`). If you get a `401 application/json`, the key is missing or wrong.

## Default path: `getStitchedForecastStatistics`

`GET /v2/forecast/statistics`

Use this unless the caller explicitly needs the full distribution. It returns the mean
plus quantiles over the ~31-member ensemble, optionally aggregated in time.

| Parameter | Required | Notes |
|---|---|---|
| `lat` | yes | −90 to 90 |
| `lon` | yes | −180 to 180 |
| `var` | no | Variable slug(s). Single, comma-separated, or repeated. Defaults to the endpoint's full set — always pass it explicitly to keep payloads small. |
| `start_date` / `end_date` | no | `YYYY-MM-DD` |
| `granularity` | no | `daily` (default), `weekly`, `monthly` |
| `statistics` | no | Comma-separated quantiles in `[0, 1]`. Default `0.05,0.25,0.50,0.75,0.95` |
| `use_downscaling` | no | Default `true` |

Valid `var` slugs are in `vocabulary/climateai-weather-variables.yml`. Passing an
invalid slug or an out-of-range coordinate returns `400` with
`{"message": "...", "code": "VALIDATION_ERROR"}`.

## When you need the distribution: `getStitchedForecast`

`GET /v2/forecast`

Same parameters minus `statistics` and `granularity`. Returns the raw ensemble members
so you can compute your own risk metrics — threshold exceedance probabilities, tail
risk, custom percentiles. Use it when the caller asks "what's the chance that…" rather
than "what will it be".

## Rules that will bite you

1. **Aggregation is variable-aware.** At `weekly`/`monthly`, precipitation and
   evapotranspiration are *summed* within the window; temperature, humidity, wind and
   solar radiation are *averaged*. Do not re-average a summed variable.
2. **Only complete windows are returned.** `weekly` uses ISO weeks (Mon–Sun) and
   `monthly` uses calendar months; partial periods are dropped. A caller asking for
   "the next 10 days, weekly" gets one week, not two.
3. **Resolution is an account entitlement, not a request flag.** `use_downscaling=true`
   is the default but has effect only if the key is provisioned for 1 km *and* the
   variable is downscalable (`temp_mean`, `temp_max`, `temp_min`, `solar_radiation`).
   Read `downscaled` in the response meta — never assume you got 1 km.
4. **Coordinates snap to the 0.25° grid.** The v2 response returns
   `location.requested` alongside `location.closest_location`. Report the closest
   location back to the caller when the offset matters.
5. **No terciles on v2.** If the caller specifically needs probabilistic terciles, this
   skill cannot serve them — see `climateai-legacy-tercile-forecast.md`.

## Errors

| Status | Meaning | Do |
|---|---|---|
| 400 | `VALIDATION_ERROR` — bad coordinate, slug, date or granularity | Fix the parameter; do not retry unchanged |
| 404 | No data for that cell/range/variable | Widen the range or drop the variable |
| 500 | Server error | Retry with backoff — all operations are safe GETs |
| 401 | Missing/invalid key (live behavior; not in the spec) | Stop and surface it |

No rate-limit contract is published — no `429`, no `Retry-After`, no `X-RateLimit-*`
headers. Apply your own conservative pacing.

Full detail: `conventions/climateai-conventions.yml`, `errors/climateai-problem-types.yml`.
