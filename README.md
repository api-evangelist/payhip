# Payhip (payhip)

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
