---
name: mediamath-traffic-creatives
description: Traffic display and video creatives into MediaMath — group them into a concept, create third-party or hosted creatives, check exchange approval health, and attach them to strategies. Use when asked to upload, traffic, approve or troubleshoot creatives on the MediaMath Platform.
generated: '2026-08-13'
method: generated
source: openapi/mediamath-atomic-creatives-api-openapi.yml, openapi/mediamath-concepts-api-openapi.yml, openapi/mediamath-video-creatives-api-openapi.yml, openapi/mediamath-creatives-api-openapi.yml
api: MediaMath Campaign Management API v3.0 + Video Creatives API v1.0
base_url: https://api.mediamath.com
operations:
  - list-concepts
  - create-concept
  - get-concept
  - list-atomic-creatives
  - post-atomic_creatives
  - get-atomic-creative
  - post-atomic_creatives-atomic_creative_id
  - bulk-update-atomic-creatives
  - atomic-creatives-healthcheck
  - creatives-atomic_creative_id-include-previews
  - list-strategy-concepts
  - Get_video_asset_upload_S3_URL
  - POST_video-v2-0-creatives-video_id-upload
  - GET_video-v2-0-creatives-video_id-status
  - GET_video-v2-0-creatives-video_id-variants
  - POST_video-v2-0-creatives-validateVAST
  - GET_static_data-v1-0-iab_attributes
---

# Traffic creatives into MediaMath

Creative objects sit under an advertiser and are grouped by **concept** (the API's name
for what the UI calls a creative group — the terms are interchangeable). Strategies
reference concepts, not individual creatives, so nothing serves until a creative is in a
concept and that concept is attached to a strategy.

## Step 1 — the concept

`list-concepts` (`GET /concepts`) filtered by `advertiser_id`, or `create-concept`
(`POST /concepts`) with `advertiser_id` and a name. Status defaults to active.
Verify with `get-concept` (`GET /concepts/{concept_id}`).

## Step 2a — third-party (3PAS) display creatives

`post-atomic_creatives` (`POST /atomic_creatives`) with `advertiser_id`, a name and
dimensions. For a third-party ad server tag supply the tag body and its type
(`SCRIPT` or `IMG`).

Attach it to the concept by setting `concept_id` — either on create, or afterwards with
`post-atomic_creatives-atomic_creative_id` (`POST /atomic_creatives/{atomic_creative_id}`).

## Step 2b — hosted video creatives

Video is a two-step upload, not a single POST:

1. `Get_video_asset_upload_S3_URL` reserves the creative record and returns a
   **presigned S3 URL** with a TTL.
2. `POST_video-v2-0-creatives-video_id-upload` / a direct PUT of the asset bytes to that
   presigned URL.
3. Poll `GET_video-v2-0-creatives-video_id-status`. The creative moves
   `Pending` -> `Processing` -> `Finished` as encoding completes. Do not attach it to a
   strategy before it reaches `Finished`.
4. `GET_video-v2-0-creatives-video_id-variants` lists the encoded renditions.

For a VAST tag rather than a hosted asset, validate first with
`POST_video-v2-0-creatives-validateVAST`.

Companion banners are managed with the
`/video/v2.0/creatives/{video_id}/companions` operations. IAB attributes and verticals
required on video metadata come from `GET_static_data-v1-0-iab_attributes` and
`GET_static_data-v1-0-iab_verticals` — read them, do not guess the codes.

## Step 3 — check approval health, before you blame delivery

This is the step people skip. A trafficked creative that no exchange has approved will
not serve, and nothing else in the API tells you that.

`atomic-creatives-healthcheck` (`GET /atomic_creatives/healthcheck`) returns per-exchange
approval status — AppNexus, Google AdX, MoPub, Microsoft Ad Exchange and others — plus a
net health verdict. It accepts a single creative ID or an array of up to **100** IDs, so
audit the whole concept in one call.

If a campaign is under-delivering, run this before touching pacing or bids.

## Step 4 — previews

`creatives-atomic_creative_id-include-previews` returns visual properties, dimensions,
the ad tag and a preview URL. Lighter than a full `get-atomic-creative` when you only
need to eyeball the render.

## Step 5 — attach to strategies

`list-strategy-concepts` shows what a strategy is currently serving. Strategy creative
assignment is part of the strategy payload — see
`skills/mediamath-launch-campaign.md`.

## Bulk work

`bulk-update-atomic-creatives` updates many at once and can return **HTTP 207
Multi-Status**. Treat 207 as partial failure until you have read every item.

## Cautions

- No idempotency key exists. A retried `post-atomic_creatives` after a timeout creates a
  duplicate creative. Call `list-atomic-creatives` filtered by `advertiser_id` and
  `concept_id` and check before retrying.
- Updates are `POST` to the entity path, not `PUT`/`PATCH`.
- Concurrent writes are capped at 150 cluster-wide (30 per pod). Uploading a large batch
  in parallel will start returning `too-many-concurrent-writes`; honour `Retry-After`.
- **Native creatives** are exposed through the Infillion Agent Connector MCP tools but
  appear in no published OpenAPI. There is no documented REST path for them.
