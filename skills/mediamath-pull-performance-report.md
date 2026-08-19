---
name: mediamath-pull-performance-report
description: Pull MediaMath performance, win/loss, pixel-load and dimension reports — pick the right dataset, read its metadata, submit the query, and handle the V1-to-V2 migration. Use when asked for campaign performance, spend, delivery, win rate, or reach and frequency numbers from MediaMath.
generated: '2026-08-13'
method: generated
source: openapi/mediamath-datasets-api-openapi.yml, openapi/mediamath-reporting-api-v1-openapi.yml, examples/, lifecycle/mediamath-lifecycle.yml
api: MediaMath Reporting API V2 (and V1, deprecated)
base_url: https://api.mediamath.com/reporting/v2
operations:
  - GET_report
  - GET_report-meta
  - GET_report-validate
  - GET_performance
  - GET_performance-meta
  - GET_win_loss
  - GET_win_loss-meta
  - GET_win_loss_creative
  - Generate-Brain-Feature-Summary-report
  - Generate-Brain-Feature-Value-report
---

# Pull a MediaMath report

There are two reporting surfaces and they behave differently. Use V2 unless you have a
specific reason not to.

## Which API

**Reporting API V2** — `https://api.mediamath.com/reporting/v2`. Datasets are queried
with **POST** and a JSON body. Ten datasets:

| Dataset | Path | Use it for |
| --- | --- | --- |
| Performance | `/performance` | Spend, impressions, clicks, conversions by entity |
| Performance Hourly | `/performance-hourly` | Same, at hour granularity |
| All Dimensions and Metrics | `/all-dimensions-and-metrics` | Wide cross-tab pulls |
| Day Part | `/day-part` | Delivery by hour-of-week |
| Reach and Frequency | `/reach-frequency` | Unique reach, frequency distribution |
| Win/Loss | `/win-loss` | Auction win rate and loss reasons |
| Pixel Loads | `/pixel-loads` | Pixel fire volume |
| Deals | `/deals` | PMP/deal-level delivery |
| Brain Feature Summary | `/brain-feature-summary` | BYOA/Custom Brain model features |
| Brain Feature Value | `/brain-feature-value` | Per-value feature detail |

Request and response shapes for every one of these are captured verbatim in
`examples/` in this repo — read the matching
`reporting-post-<dataset>-request.json` before composing a query.

**Reporting API V1** — `https://api.mediamath.com/reporting/v1/std`. GET-based, 30
report endpoints each with a `/meta` sibling. **Deprecated**: the docs state it will be
removed and name Reporting V2 as the replacement. Do not build anything new on it. See
`lifecycle/mediamath-lifecycle.yml` for the dated notice.

## Step 1 — read the metadata before you query

On V1, `GET_report-meta` (`GET /{report}/meta`) returns the dimensions and metrics that
report supports, and `GET_report-validate` will check a query without running it. Use
them; a report will happily accept a dimension it cannot group by and return an empty
set rather than an error.

## Step 2 — submit the query

V2 datasets are POST-only. Send the time range, the dimensions, the metrics and the
entity filter (organization / agency / advertiser / campaign / strategy) in the body.

Authenticate with `Authorization: Bearer <token>` from
`https://auth.mediamath.com/oauth/token`.

## Step 3 — read the result

Response content types across the reporting surface include `application/json`,
`application/jsonl` and `text/csv`. Large pulls stream as JSONL or CSV — do not assume a
single JSON object.

## Practical notes

- **Scope your entity filter.** An unfiltered all-dimensions pull across a large
  organization is the fastest way to hit rate limits and time out.
- **Rate limits are per user, not per application.** Multiple scripts sharing one
  credential share one bucket. Sustained safe rate is 40 req/s; reports are heavy, so
  space them.
- **Data latency.** Hourly performance and win/loss are the freshest surfaces; standard
  performance settles later. The API does not expose a freshness timestamp — reconcile
  against the platform UI if a number looks wrong.
- **Win/Loss has a creative-level sibling** (`GET_win_loss_creative` on V1) that answers
  "which creative is losing auctions", which the campaign-level report cannot.
- On 429 or 503, back off exponentially using `Retry-After` up to 60s.

## What is not here

There is no scheduled-delivery or webhook path for reports in the public API — you poll.
For bulk raw data, the Log Level Data Service and Cloud File Transfer are separate
batch-delivery products
(`https://apidocs.mediamath.com/apis/log-level-data-service`).
