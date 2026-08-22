# Payhip (payhip)

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

Payhip is an all-in-one e-commerce platform that lets creators sell digital downloads, online courses, memberships, coupons, and physical products directly to their audience, with hosted storefronts and checkout. Its **public REST API** (base `https://payhip.com/api/v2`) is self-serve and openly documented, but currently narrow: it exposes programmatic management of **Coupons** and verification/management of software **License Keys**. Order, customer, and transaction data is not a pollable REST resource - it is delivered to your application through signed **webhooks** (`paid`, `refunded`, `subscription.created`, `subscription.deleted`).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/payhip/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/payhip/refs/heads/main/apis.yml)

## Access Model

- **Public and self-serve.** Docs are openly readable at [payhip.com/api-reference](https://payhip.com/api-reference) and the [Developer help center](https://help.payhip.com/category/48-developer). Any account holder generates an API key and per-product secret keys from **Settings > Developer** - no partner approval or sales contact required.
- **Two credentials.** Coupon calls use the account API key via the `payhip-api-key` header. License calls use a per-product secret key via the `product-secret-key` header. A request without a key returns HTTP `401`, confirming the API is live.
- **Deliberately narrow today.** Payhip's own help center states the API "currently supports managing coupons and license keys," with more planned. There are **no Products, Customers, or Transactions REST endpoints** - that data flows only through webhooks.
- **Responses** are JSON wrapped in a `data` object; monetary amounts in webhook payloads are in cents.

## Tags

- E-commerce
- Digital Products
- Memberships
- Creators
- Coupons
- License Keys
- Webhooks
- Payments

## Timestamps

- **Created:** 2026-07-05
- **Modified:** 2026-07-05

## APIs

### Payhip Coupons API

Programmatically create, list, and retrieve discount coupons - percentage or fixed-amount, single, multi-use, or collection-scoped - including usage limits, minimum purchase amounts, start/end dates, and product or collection targeting. Authenticated with the account API key via the `payhip-api-key` header.

- **Human URL:** [https://payhip.com/api-reference](https://payhip.com/api-reference)
- **Base URL:** `https://payhip.com/api/v2`
- `POST /coupons` · `GET /coupons` · `GET /coupons/{id}`

#### Properties

- [Documentation](https://help.payhip.com/article/347-public-api)
- [API Reference](https://payhip.com/api-reference)
- [OpenAPI](openapi/payhip-openapi.yml)
- [Postman Collection](collections/payhip.postman_collection.json)
- [Open Collection](collections/payhip.opencollection.json)

### Payhip License Keys API

Verify and manage software license keys issued for Payhip products - validate a key and read its buyer, product, and usage details; enable or disable a key; and increment or decrement its usage count. Authenticated with the per-product secret key via the `product-secret-key` header.

- **Human URL:** [https://payhip.com/api-reference](https://payhip.com/api-reference)
- **Base URL:** `https://payhip.com/api/v2`
- `GET /license/verify` · `PUT /license/enable` · `PUT /license/disable` · `PUT /license/usage` · `PUT /license/decrease`

#### Properties

- [Documentation](https://help.payhip.com/article/347-public-api)
- [API Reference](https://payhip.com/api-reference)
- [OpenAPI](openapi/payhip-openapi.yml)
- [Postman Collection](collections/payhip.postman_collection.json)
- [Open Collection](collections/payhip.opencollection.json)

### Payhip Webhooks API

Receive server-to-endpoint HTTP callbacks for account events - `paid` (customer charged), `refunded`, `subscription.created`, and `subscription.deleted` - carrying transaction, customer, item, and subscription details. Each payload includes a `signature` that verifies authenticity as `hash('sha256', apiKey)`. Amounts are in cents. Endpoints must return HTTP 200; failed deliveries retry hourly for up to three hours. This is how order/customer/transaction data reaches external applications.

- **Human URL:** [https://help.payhip.com/article/115-webhooks](https://help.payhip.com/article/115-webhooks)
- **Configured under:** Settings > Developer

#### Properties

- [Documentation](https://help.payhip.com/article/115-webhooks)
- [OpenAPI](openapi/payhip-openapi.yml) (webhook payloads under the `webhooks` section)

## Pricing

Payhip is priced as a platform subscription plus a per-sale fee, not as a metered API. API and webhook access is included on every plan.

- **Free** - $0/month, **5%** per-sale Payhip fee
- **Plus** - $29/month, **2%** per-sale Payhip fee
- **Pro** - $99/month, **0%** Payhip fee

Payment processor fees (Stripe/PayPal) are separate and always apply. See [payhip.com/pricing](https://payhip.com/pricing).

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/payhip)
- [Website](https://payhip.com)
- [Documentation](https://help.payhip.com/category/48-developer)
- [API Reference](https://payhip.com/api-reference)
- [Plans](plans/payhip-plans-pricing.yml)
- [Rate Limits](rate-limits/payhip-rate-limits.yml)
- [Fin Ops](finops/payhip-finops.yml)

## Review

Does Payhip expose a documented public WebSocket API? **No.** Payhip's public surface is request/response REST (Coupons, License Keys) plus outbound signed webhooks. There is no `ws://`/`wss://` endpoint, so no AsyncAPI document was authored. See [review.yml](review.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
