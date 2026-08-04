# MediaMath (mediamath)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
