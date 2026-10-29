# ClimateAI

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

ClimateAi (climate.ai) is a climate-intelligence company that turns global weather, climate and extreme-event modeling into decision-grade forecasts for agriculture, food and beverage, manufacturing, energy, finance, retail and federal/defense customers. Its ClimateLens products cover risk screening, monitoring and adaptation, and its developer surface is the LensConnect API — a REST weather and climate data API addressed by latitude and longitude that returns 30+ years of history (1995-present, ERA5-backed), a fixed 30-year climatology baseline, and AI-stitched probabilistic forecasts running from short-term through seasonal (~6 months) in a single continuous timeline, at ~25 km resolution with optional 1 km downscaling for select variables. A separate ClimateAI Platform gateway handles accounts, users, roles, permissions, device API keys and product routing.

**Areas:** Company · Weather · Climate · Climate Intelligence · Forecasting · Agriculture · Data · Supply Chain · Risk Management · Sustainability

## ClimateAI on APIs.io

Everything profiled for ClimateAI is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/climateai/](https://apis.io/providers/climateai/)** — or go straight to one of the APIs or properties below.

### APIs (15)

- [ClimateAI Platform API](https://apis.io/apis/climateai/platform/) — ClimateAI authentication and routing gateway for platform services. Covers accounts, account configuration, users, roles, permissions, device API keys,…
- [ClimateAI Account API](https://apis.io/apis/climateai/climateai-account-api/) — account related operations
- [ClimateAI Account Config API](https://apis.io/apis/climateai/climateai-account-config-api/) — account config related operations
- [ClimateAI Auth API](https://apis.io/apis/climateai/climateai-auth-api/) — authentication related operations
- [ClimateAI Current (v2) API](https://apis.io/apis/climateai/climateai-current-v2-api/) — Modern endpoints (recommended). Faster grid-index lookups, blended multi-model forecasts, explicit downscaling control, and a compact, date-keyed response…
- [ClimateAI Device API](https://apis.io/apis/climateai/climateai-device-api/) — device api key related operations
- [ClimateAI Email API](https://apis.io/apis/climateai/climateai-email-api/) — email sending operations
- [ClimateAI Legacy (v1) API](https://apis.io/apis/climateai/climateai-legacy-v1-api/) — Original endpoints. Stable and supported, but superseded by the Current (v2) endpoints where noted. Default response shape is the `{ meta, data }` envelope,…
- [ClimateAI Permission API](https://apis.io/apis/climateai/climateai-permission-api/) — permission related operations
- [ClimateAI Platform API](https://apis.io/apis/climateai/climateai-platform-api/) — platform label related operations
- [ClimateAI Product API](https://apis.io/apis/climateai/climateai-product-api/) — product listing
- [ClimateAI Report API](https://apis.io/apis/climateai/climateai-report-api/) — report related operations
- [ClimateAI Role API](https://apis.io/apis/climateai/climateai-role-api/) — user role related operations
- [ClimateAI Routing API](https://apis.io/apis/climateai/climateai-routing-api/) — routing and proxy operations
- [ClimateAI User API](https://apis.io/apis/climateai/climateai-user-api/) — user related operations

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [climateai-weather](https://apis.io/servers/climateai/climateai-weather/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Climateai Agentic Access](https://apis.io/agentic-access/climateai/climateai-agentic-access/)

#### Collections (14)

Postman and Open Collection request collections.

- [ClimateAI Platform Account API](https://apis.io/collections/climateai/open-climateai-account-api/)
- [ClimateAI Platform Account Config API](https://apis.io/collections/climateai/open-climateai-account-config-api/)
- [ClimateAI Platform Auth API](https://apis.io/collections/climateai/open-climateai-auth-api/)
- [ClimateAI Weather Current (v2) Current (v2) API](https://apis.io/collections/climateai/open-climateai-current-v2-api/)
- [ClimateAI Platform Device API](https://apis.io/collections/climateai/open-climateai-device-api/)
- [ClimateAI Platform Email API](https://apis.io/collections/climateai/open-climateai-email-api/)
- [ClimateAI Weather Legacy (v1) Legacy (v1) API](https://apis.io/collections/climateai/open-climateai-legacy-v1-api/)
- [ClimateAI Platform Permission API](https://apis.io/collections/climateai/open-climateai-permission-api/)
- [ClimateAI Platform API](https://apis.io/collections/climateai/open-climateai-platform-api/)
- [ClimateAI Platform Product API](https://apis.io/collections/climateai/open-climateai-product-api/)
- [ClimateAI Platform Report API](https://apis.io/collections/climateai/open-climateai-report-api/)
- [ClimateAI Platform Role API](https://apis.io/collections/climateai/open-climateai-role-api/)
- [ClimateAI Platform Routing API](https://apis.io/collections/climateai/open-climateai-routing-api/)
- [ClimateAI Platform User API](https://apis.io/collections/climateai/open-climateai-user-api/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Climateai Platform Overlay](https://apis.io/overlays/climateai/climateai-platform-overlay/)
- [Climateai Weather Overlay](https://apis.io/overlays/climateai/climateai-weather-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Climateai Authentication](https://apis.io/security/climateai/climateai-authentication/)
- [Climateai Domain Security](https://apis.io/security/climateai/climateai-domain-security/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://climate.ai/)
- [Documentation](https://docs.climate.ai/)
- [Getting started](https://docs.climate.ai/guide/getting-started)
- [API reference](https://docs.climate.ai/climateai-weather-api)
- [Sign up](https://climate.ai/get-started/)
- [Blog](https://climate.ai/blog/)
- [Terms of service](https://climate.ai/terms-of-use/)
- [Privacy policy](https://climate.ai/privacy-policy/)
- [GitHub](https://github.com/ClimateAI)

## API Evangelist rating

**Kin Score 42.9** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 50.2 |
| Contract governance | 19.7 |
| Operational transparency | 10.5 |
| Developer ergonomics | 58.9 |
| Access clarity | 34.2 |

**Agent readiness 23.9** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 24.5** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/climateai/](https://apis.io/providers/climateai/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for ClimateAI: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/climateai/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
