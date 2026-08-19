---
name: mediamath-launch-campaign
description: Stand up a new MediaMath programmatic campaign end to end — resolve the advertiser, create the campaign with goals and budget, then create the strategies that actually buy media. Use when asked to launch, set up, or clone a campaign on the MediaMath Platform.
generated: '2026-08-13'
method: generated
source: openapi/mediamath-campaigns-api-openapi.yml, openapi/mediamath-strategies-api-openapi.yml, openapi/mediamath-advertisers-api-openapi.yml, conventions/mediamath-conventions.yml
api: MediaMath Campaign Management API v3.0
base_url: https://api.mediamath.com/api/v3.0
operations:
  - list-advertisers
  - get-advertiser
  - list-campaigns
  - create-campaign
  - get-campaign
  - update-campaign
  - list-currency-rates
  - list-timezones
  - create-strategy
  - get-strategy
  - update-strategy
  - list-user-permissions
---

# Launch a MediaMath campaign

A campaign on MediaMath holds budget, goals and pacing. It buys nothing on its own —
**strategies** under it do the buying. A campaign with no strategies spends zero.

## Before you start

1. Get a bearer token. `POST https://auth.mediamath.com/oauth/token` with
   `audience=https://api.mediamath.com/`. Tokens last 86400 seconds.
   Send it as `Authorization: Bearer <token>` on every call.
2. Some collections have not finished migrating to OAuth2. If you get a 401 on an
   endpoint the token should cover, `GET /api/v2.0/session` with the bearer token,
   take the `adama_session` cookie from the response, and send **both** on
   subsequent requests.
3. Confirm the caller can actually write. `list-user-permissions` for the user —
   a read-only user gets a 403 on `create-campaign`, not a helpful message.

## Step 1 — resolve the advertiser

`list-advertisers` (`GET /advertisers`) with `q` to filter by name, or
`get-advertiser` (`GET /advertisers/{advertiser_id}`) if you already have the ID.

Everything downstream hangs off `advertiser_id`. Do not guess it — MediaMath IDs are
bare integers with no type prefix, so a wrong ID will often resolve to a real object
of the wrong kind.

## Step 2 — validate the reference values

Campaign creates reject unknown enum values with a generic 400 that does not name the
offending field. Read the reference collections first:

- `list-currency-rates` (`GET /currency_rates`) for a valid currency code
- `list-timezones` (`GET /timezones`) for the campaign timezone
- `list-verticals` (`GET /verticals`) if you are setting a vertical

## Step 3 — create the campaign

`create-campaign` (`POST /campaigns`). Minimum viable body: `advertiser_id`, `name`,
and a goals configuration. Then layer on budget, flights, pacing, frequency,
attribution and inventory settings.

**Attribution.** Use `attribution.merit_pixels[]` — 1 to 10 entries, each with a
unique `pixel_id`, a `weight` between 0.00 and 10.00 (max two decimal places, default
1.00, at least one greater than zero), and an optional unique `funnel_position` 1-10.
The single-pixel `attribution.merit_pixel_id` field is **deprecated**. Never send both
fields in one request — that is a documented 400.

**There is no idempotency key.** If `create-campaign` times out, do NOT blindly retry.
Call `list-campaigns` filtered by `advertiser_id` and name first; a retry will create a
second campaign.

## Step 4 — create strategies

`create-strategy` (`POST /strategies`) with the `campaign_id` from step 3, a name and a
goal configuration. Two business rules will fail your create if you miss them:

- `goal_type` cannot be `roi` or `cpa` unless `use_optimization` is `true` **and** the
  parent campaign has a merit pixel set.
- `goal_type: spend` is only supported when `use_optimization` is `false`.

Strategies carry pacing, frequency, budget, inventory (exchanges, deals, site lists),
targeting (audience, contextual, geo, daypart, technology) and creative assignments.

## Step 5 — verify

`get-campaign` (`GET /campaigns/{campaign_id}`) and `get-strategy`
(`GET /strategies/{strategy_id}`) to read back what was actually stored. Writes are
`POST` to the entity path — not `PUT` or `PATCH` — and partial-update semantics mean an
omitted field is left alone, not cleared.

## Updating

`update-campaign` is `POST /campaigns/{campaign_id}`. Only fields you send are
modified. `attribution.merit_pixels` **replaces** the whole merit configuration; send
`[]` to clear it.

For many campaigns at once use `bulk-update-campaigns`. Bulk endpoints can return
**HTTP 207 Multi-Status** — a 207 is not success. Inspect every item in the body.

## Rate limits

Sustained 40 req/s per user, burst 200 after an idle period, 150 concurrent writes.
The `X-RateLimit-*` headers report **per-pod** values (limit 10), which are 1/5 of your
real cluster-wide capacity — do not throttle yourself to the header. On 429 or 503,
honour `Retry-After` and back off exponentially to a 60s ceiling.

## Errors

Error bodies are `{"meta":{"status":"error","uuid":"..."},"errors":[{"code","message","details"}]}`.
Quote `meta.uuid` when escalating. See `errors/mediamath-problem-types.yml`.
