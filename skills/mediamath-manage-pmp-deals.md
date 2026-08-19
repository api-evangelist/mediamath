---
name: mediamath-manage-pmp-deals
description: Work private marketplace inventory on MediaMath — find and create deals and deal groups, attach publishers and channels, and bind deals to strategies through the Marketplaces V2.0 API. Use when asked about PMP deals, deal IDs, private auctions, or exchange supply on the MediaMath Platform.
generated: '2026-08-13'
method: generated
source: openapi/mediamath-marketplaces-api-v2-openapi.yml, openapi/mediamath-supply-sources-api-openapi.yml, https://apidocs.mediamath.com/guides/marketplaces
api: MediaMath Marketplaces API V2.0
base_url: https://api.mediamath.com/deals/v1.0
operations:
  - LIST-deals
  - GET-deal
  - POST-deal
  - PUT-deal
  - LIST-deals-and-reporting-data
  - List-Deal-Strategies
  - LIST-deal-groups
  - GET-deal-group
  - POST-deal-group
  - PUT-deal-group
  - List-deal-group-strategies
  - Bulk-Create-Deal
  - Update-Bulk-Deal
  - Bulk-Create-or-Update-Deal
  - Retrieve_publishers
  - Retrieve_a_publisher_by_ID
  - POST_publishers
  - Bulk-Create-Publishers
  - List_channels
  - list-supply-sources
  - get-supply-source
---

# Manage PMP deals on MediaMath

The Marketplaces API covers PMP Direct and exchange supply. Note the path/version
mismatch up front: the product is **Marketplaces API V2.0** and it is served at
`https://api.mediamath.com/deals/v1.0`. That is correct, not a typo.

## The V2.0 rules that break V1.0 code

The Marketplaces API deliberately does **not** follow the Campaign Management
conventions. Four differences will bite:

1. **`?owner.organization_id=<entity_id>` is REQUIRED** on requests. It was optional in
   V1.0.
2. **`?full` is not supported.** Collections always return full entity properties.
3. **`?with` is not supported.** You cannot inline related entities — make a second call.
4. **The `/limit/` path component is not supported.** Filter with the documented
   query parameters instead.

## Step 1 — find inventory

- `list-supply-sources` (`GET /supply_sources`) and `get-supply-source` for exchanges.
  Supply sources are hierarchical — a source can have sub-sources
  (`sub_supply_source_id`).
- `List_channels` (`GET /channels`) for channel metadata.
- `Retrieve_publishers` (`GET /publishers`) and `Retrieve_a_publisher_by_ID` for
  publisher entities. Create with `POST_publishers` or `Bulk-Create-Publishers`.

## Step 2 — find or create the deal

- `LIST-deals` (`GET /deals`) with `owner.organization_id`.
- `LIST-deals-and-reporting-data` returns deals alongside their delivery data — use this
  instead of joining a deal list against a separate reporting pull.
- `GET-deal` (`GET /deals/{id}`) for one deal.
- `POST-deal` (`POST /deals`) to create.
- `PUT-deal` — note the operationId says PUT but the operation is **`POST /deals/{id}`**.

For volume, `Bulk-Create-Deal`, `Update-Bulk-Deal` and `Bulk-Create-or-Update-Deal`.
These return **HTTP 207 Multi-Status**; a 207 means some rows failed. Read every item.

## Step 3 — deal groups

Deal groups bundle deals so a strategy can target a set rather than enumerating IDs.

- `LIST-deal-groups` / `GET-deal-group`
- `POST-deal-group` to create, `PUT-deal-group` (served as `POST /deal_groups/{id}`) to
  update

## Step 4 — bind to strategies

- `List-Deal-Strategies` (`GET /deals/{id}/strategy_deals`) — which strategies target
  this deal.
- `List-deal-group-strategies` (`GET /deal_groups/{id}/strategy_deal_groups`) — same for
  a group.

Attaching a deal to a strategy is done in the strategy's inventory settings — see
`skills/mediamath-launch-campaign.md`.

## Troubleshooting a deal that is not spending

Work it in this order:

1. Is the deal attached to a live strategy? `List-Deal-Strategies`.
2. Is the strategy's supply configuration allowing that exchange?
   `list-supply-sources` and the strategy's inventory block.
3. Are the creatives approved on that exchange? `atomic-creatives-healthcheck` — see
   `skills/mediamath-traffic-creatives.md`.
4. Is the deal winning anything? Pull the Win/Loss and Deals datasets — see
   `skills/mediamath-pull-performance-report.md`.

## Cautions

- No idempotency key. A retried `POST-deal` after a timeout creates a second deal with
  the same external deal ID. List and check before retrying.
- 409 Conflict is declared on several operations, usually a duplicate name or a
  concurrent edit. Read the entity back rather than retrying blind.
- Authenticate with `Authorization: Bearer <token>`. If you get an unexpected 401,
  fetch the `adama_session` cookie from `GET /api/v2.0/session` and send both.
