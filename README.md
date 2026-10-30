# Logiwa

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

Logiwa is a Chicago-based cloud fulfillment software company whose flagship product, Logiwa IO, is a warehouse management and fulfillment management system (WMS/FMS) built for high-volume B2C and DTC brands, wholesalers and third-party logistics providers (3PLs). Logiwa exposes a documented Integration API covering products, shipment orders, purchase orders, receipt orders, inventory, locations, count plans, documents, warehouse tasks, transaction history and 3PL billing, plus an eleven-topic webhook surface for order, inventory, movement and shipment tracking events. The API is an RPC-over-POST design: 81 documented operations, all reached by POST to /en/api/IntegrationApi/{Method} on a per-tenant host, authenticated with an OAuth 2.0 password grant that yields a bearer token. Logiwa publishes no OpenAPI, AsyncAPI or other machine-readable contract, and no first-party SDKs; the reference is a JavaScript-rendered developer portal and API credentials are provisioned by sales rather than self-service.

**Areas:** Company · Warehouse Management · Fulfillment · Logistics · Supply Chain · Inventory · Order Management · Third Party Logistics · E-Commerce · Shipping · Webhook · Software-as-a-Service

## Logiwa on APIs.io

Everything profiled for Logiwa is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/logiwa/](https://apis.io/providers/logiwa/)** — or go straight to one of the APIs or properties below.

### APIs (2)

- [Logiwa Integration API](https://apis.io/apis/logiwa/logiwa-integration-api/) — The Logiwa Integration API is an RPC-over-HTTP interface with 81 documented operations covering products and kits, shipment orders and order details,…
- [Logiwa Webhooks](https://apis.io/apis/logiwa/logiwa-webhooks/) — Logiwa's outbound event surface. Eleven documented topics deliver order status, receipt and purchase order status, inventory change, location update,…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Logiwa Webhooks](https://apis.io/asyncapis/logiwa/logiwa-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Logiwa MCP server](https://apis.io/servers/logiwa/logiwa-mcp-server/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Logiwa Authentication](https://apis.io/security/logiwa/logiwa-authentication/)
- [Logiwa Domain Security](https://apis.io/security/logiwa/logiwa-domain-security/)
- [Logiwa Trust Center](https://apis.io/security/logiwa/logiwa-trust-center/)
- [Logiwa Vulnerability Disclosure](https://apis.io/security/logiwa/logiwa-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Logiwa Scopes](https://apis.io/scopes/logiwa/logiwa-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Logiwa Plans Pricing](https://apis.io/plans/logiwa/logiwa-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Logiwa Rate Limits](https://apis.io/rate-limits/logiwa/logiwa-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.logiwa.com/)
- [Documentation](https://developer.logiwa.com/?id=5df0d8bfe6466c2eec992f31)
- [Getting started](https://developer.logiwa.com/?id=5df0d8bfe6466c2eec992f31)
- [API reference](https://developer.logiwa.com/)
- [Pricing](https://www.logiwa.com/pricing)
- [Support](https://www.logiwa.com/contact-us)
- [Blog](https://www.logiwa.com/blog)
- [Privacy policy](https://www.logiwa.com/privacy-policy)

## API Evangelist rating

**Kin Score 46.6** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 39.0 |
| Contract governance | 18.2 |
| Operational transparency | 39.5 |
| Developer ergonomics | 58.9 |
| Access clarity | 36.8 |

**Agent readiness 34.4** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 35.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/logiwa/](https://apis.io/providers/logiwa/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Logiwa: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/logiwa/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
