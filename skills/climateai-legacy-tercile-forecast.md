---
name: Get probabilistic tercile forecasts (legacy v1 only)
description: >-
  Retrieve above/near/below-normal tercile probabilities for a location from the
  ClimateAi legacy subseasonal and seasonal endpoints — the one capability that has no
  equivalent on the current v2 API and cannot be recomputed client-side.
api: openapi/climateai-weather-openapi.yml
base_url: https://api-prod.climate.ai/weather
operations:
  - getSubseasonalForecast
  - getSeasonalForecast
  - getShortTermForecast
generated: '2026-08-04'
method: generated
---

# Legacy tercile forecasts

## When to use this

The caller needs categorical probabilities — "what's the chance of a wetter-than-normal
season" — expressed as terciles: `0.00–0.33` (below normal), `0.33–0.67` (near normal),
`0.67–1.0` (above normal). **Only the legacy v1 endpoints return these.** The current
`/v2/forecast/statistics` returns mean plus quantiles and nothing else, and you cannot
derive terciles from what v2 publishes — terciles need the 33rd and 67th climatology
percentiles and `/v1/climatology` exposes only `[0.05, 0.25, 0.50, 0.75, 0.95]`.

For anything that does *not* need terciles, use `climateai-forecast-a-location.md`
instead. These endpoints are superseded and this skill exists only for the gap.

## Authenticate

```
X-Api-Key: <YOUR_API_KEY>
```

## Choose the horizon

| Operation | Path | Horizon | Terciles on |
|---|---|---|---|
| `getSubseasonalForecast` | `GET /v1/forecast/subseasonal` | weeks 2–6 | `granularity=weekly` |
| `getSeasonalForecast` | `GET /v1/forecast/seasonal` | months 1–6 | `granularity=monthly` |
| `getShortTermForecast` | `GET /v1/forecast/short-term` | ~15 days | none — daily only |

Parameters are `lat`, `lon`, `var`, and `granularity` where the endpoint supports it.
**None of these accept `start_date` / `end_date`** — each call returns the current
forecast for that endpoint's fixed horizon.

Stored-location variants exist for all three
(`getShortTermForecastByLocation`, `getSubseasonalForecastByLocation`,
`getSeasonalForecastByLocation`) at `/v1/forecast/{horizon}/location/{id}`, addressed by
a server-side location ID rather than coordinates.

## Rules that will bite you

1. **You must ask for the right granularity.** Terciles appear only on subseasonal
   *weekly* and seasonal *monthly* responses. The daily variants return quantiles only.
2. **The three horizons do not concatenate cleanly.** Granularities differ and the
   weekly/monthly responses carry fields the daily ones do not. If the caller wants one
   continuous timeline, that is a v2 job — this skill is for terciles specifically.
3. **Variable availability is narrower on legacy.** `soil_moisture` is unavailable on
   seasonal; `max_wind_speed` and `max_wind_gust` are unavailable on both subseasonal
   and seasonal; `max_wind_gust` on short-term covers only the first 10 days. The full
   matrix is in `vocabulary/climateai-weather-variables.yml`.
4. **The response shape is the legacy one** — `{ meta, data }` with `data` as an array
   of per-date entries under `attributes.<var>.values`, not the v2 date-keyed object.
   It is 3–5x larger on the wire.
5. **No traceability fields.** Legacy responses carry no `init_time`, `version` or
   `generation`, so you cannot tell the caller which model run produced the numbers.
6. **These endpoints are superseded.** ClimateAi commits to supporting them "for the
   foreseeable future" but publishes no sunset date. Tell the caller they are on a
   legacy path. Migration guide: https://docs.climate.ai/guide/migration

## Errors

`400` `VALIDATION_ERROR`, `404` no data, `500` retryable, live `401` on a missing key.
See `errors/climateai-problem-types.yml`.
