# MediaMath (mediamath)

MediaMath (by Infillion) is a programmatic advertising DSP with REST APIs for managing campaigns, targeting, bidding strategies, creative trafficking, audience segments, and performance analytics. The platform provides an API-first composable architecture supporting campaign management, reporting, audience onboarding, marketplaces access, and custom bidding algorithms.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/apis.yml)

## Tags

- Programmatic Advertising
- DSP
- Demand-Side Platform
- Campaign Management
- Ad Tech
- Bidding
- Audience Segments
- Creative Management
- Reporting
- Analytics

## Timestamps

- **Created:** 2026-06-13
- **Modified:** 2026-06-13

## APIs

### MediaMath Campaigns V2.0 API

REST API for programmatically creating, viewing, and updating all campaign-related entities within the MediaMath Platform, including advertisers, campaigns, strategies, creatives, and targeting parameters.

- **Human URL:** [https://apidocs.mediamath.com/docs/api/YXBpOjMyMzMyMTI4-campaigns-v2-0-api-reference](https://apidocs.mediamath.com/docs/api/YXBpOjMyMzMyMTI4-campaigns-v2-0-api-reference)
- **Base URL:** `https://api.mediamath.com`

#### Tags

- Campaign Management
- Campaigns
- Strategies
- Creatives
- Targeting

#### Properties

- [Documentation](https://apidocs.mediamath.com/docs/api/YXBpOjMyMzMyMTI4-campaigns-v2-0-api-reference)
- [Authentication](https://apidocs.mediamath.com/guides)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/openapi/campaigns-api-openapi.yaml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Plans](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/plans/mediamath-plans.yml)
- [Rate Limits](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/rate-limits/mediamath-rate-limits.yml)
- [Fin Ops](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/finops/mediamath-finops.yml)
- [Graph Q L](graphql/mediamath-graphql.md)

### MediaMath Reporting API V2

Flexible reporting API providing access to human- and machine-readable performance reports. Supports multiple datasets, custom field selection, time windowing, filtering, sorting, pagination, and streaming responses via POST requests.

- **Human URL:** [https://apidocs.mediamath.com/apis/reporting-api](https://apidocs.mediamath.com/apis/reporting-api)
- **Base URL:** `https://api.mediamath.com/reporting/v2`

#### Tags

- Reporting
- Analytics
- Performance
- Data

#### Properties

- [Documentation](https://apidocs.mediamath.com/apis/reporting-api)
- [Authentication](https://apidocs.mediamath.com/guides)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/openapi/reporting-api-openapi.yaml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Plans](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/plans/mediamath-plans.yml)
- [Rate Limits](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/rate-limits/mediamath-rate-limits.yml)
- [Fin Ops](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/finops/mediamath-finops.yml)

### MediaMath Marketplaces API V2.0

API for leveraging PMP Direct and Exchange supply sources, enabling programmatic access to private marketplace deals and exchange inventory within the MediaMath Platform.

- **Human URL:** [https://apidocs.mediamath.com/apis/marketplaces-api/marketplaces](https://apidocs.mediamath.com/apis/marketplaces-api/marketplaces)
- **Base URL:** `https://api.mediamath.com`

#### Tags

- Marketplaces
- PMP
- Exchange
- Supply
- Inventory

#### Properties

- [Documentation](https://apidocs.mediamath.com/apis/marketplaces-api/marketplaces)
- [Authentication](https://apidocs.mediamath.com/guides)
- [Plans](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/plans/mediamath-plans.yml)
- [Rate Limits](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/rate-limits/mediamath-rate-limits.yml)
- [Fin Ops](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/finops/mediamath-finops.yml)

### MediaMath Bring Your Own Algorithm (BYOA) API

API for applying custom bidding algorithms within the MediaMath platform brain, including Campaign Settings configuration and Custom Bid Router for external algorithm invocation during bid opportunities.

- **Human URL:** [https://apidocs.mediamath.com/apis/byoa-api/campaign-settings](https://apidocs.mediamath.com/apis/byoa-api/campaign-settings)
- **Base URL:** `https://api.mediamath.com`

#### Tags

- Bidding
- Custom Algorithms
- BYOA
- Optimization

#### Properties

- [Documentation](https://apidocs.mediamath.com/apis/byoa-api/campaign-settings)
- [Authentication](https://apidocs.mediamath.com/guides)
- [Plans](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/plans/mediamath-plans.yml)
- [Rate Limits](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/rate-limits/mediamath-rate-limits.yml)
- [Fin Ops](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/finops/mediamath-finops.yml)

### MediaMath Audience Onboarding API

API for ingesting audience event data into the MediaMath Platform via real-time server-side pixel events and batch event uploads. Supports UUID, mobile advertising IDs, and CTV device IDs for cross-device audience building and segment management.

- **Human URL:** [https://apidocs.mediamath.com/guides/audience-onboarding](https://apidocs.mediamath.com/guides/audience-onboarding)
- **Base URL:** `https://ingest-default.prod.octane.mediamath.com`

#### Tags

- Audience
- Segments
- Data Onboarding
- Identity
- Events

#### Properties

- [Documentation](https://apidocs.mediamath.com/guides/audience-onboarding)
- [Authentication](https://apidocs.mediamath.com/guides)
- [Plans](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/plans/mediamath-plans.yml)
- [Rate Limits](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/rate-limits/mediamath-rate-limits.yml)
- [Fin Ops](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/finops/mediamath-finops.yml)

### MediaMath Server-to-Server Data Distribution API

API for syncing audience segment data through server-to-server data distribution, supporting UUID-to-segment mappings, SFTP file transfer, and processing log access with Basic Authentication.

- **Human URL:** [https://apidocs.mediamath.com/guides/server-to-server](https://apidocs.mediamath.com/guides/server-to-server)
- **Base URL:** `https://s2s-api.datasvc.mediamath.com`

#### Tags

- Audience
- Data Distribution
- Server-to-Server
- Segments

#### Properties

- [Documentation](https://apidocs.mediamath.com/guides/server-to-server)
- [Authentication](https://apidocs.mediamath.com/guides)
- [Plans](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/plans/mediamath-plans.yml)
- [Rate Limits](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/rate-limits/mediamath-rate-limits.yml)
- [Fin Ops](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/finops/mediamath-finops.yml)

## Common Properties

- [Plans](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/plans/mediamath-plans.yml)
- [Rate Limits](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/rate-limits/mediamath-rate-limits.yml)
- [Fin Ops](https://raw.githubusercontent.com/api-evangelist/mediamath/refs/heads/main/finops/mediamath-finops.yml)
- [Documentation](https://apidocs.mediamath.com/)
- [Authentication](https://apidocs.mediamath.com/guides)
- [Blog](https://devblog.mediamath.com/)
- [Support](https://support.infillion.com/s/submit-a-case)
- [Login](https://platform.mediamath.com/)
- [Academy](https://academy.mediamath.com/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
