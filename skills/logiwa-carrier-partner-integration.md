---
name: logiwa-carrier-partner-integration
description: Integrate a third-party carrier, TMS or rate-shopping service with Logiwa — pull orders and item detail, select a label externally, and return the label image and tracking number to Logiwa.
api: Logiwa Integration API
base_url: https://{environment}.logiwa.com/en/api/IntegrationApi
operations:
  - WarehouseOrderSearch
  - InventoryItemSearch
  - UploadDocument
generated: '2026-08-25'
method: generated
source: https://developer.logiwa.com/?id=654e30abe6466c26c496d014
---

# Integrate a carrier with Logiwa

This is the flow **Logiwa itself publishes** on *How to Integrate to Logiwa as a Carrier Partner*.
Label generation is not a Logiwa API capability — Logiwa lists "Creating carrier labels" on its
published list of operations **not** available through the API. The carrier generates the label;
Logiwa stores it.

## Before you start

- You need a Logiwa API user. It is **provisioned by Logiwa sales/customer success under a
  contract** — there is no self-service sign-up, no sandbox and no trial key.
- Get a bearer token: `POST https://{environment}api.logiwa.com/token` with
  `Content-Type: application/x-www-form-urlencoded` and body `grant_type=password`, `username`,
  `password`. Read `access_token` from the JSON response. Tokens last roughly two weeks —
  refresh before expiry.
- Send `Content-Type: application/json` on every other call. Everything is a **POST**.

## Steps

1. **Pull the orders you need to rate and label.**
   `POST /en/api/IntegrationApi/WarehouseOrderSearch`
   Set `IsGetCustomerAddressInfo` to get the ship-to address, and `IsGetOrderDetails` to get the
   order lines. Order-line detail returns description, barcode, sales unit price, item weight, and
   the planned / allocated / picked / sorted / packed / canceled quantities per line.

2. **Fill in anything the order response did not carry.**
   `POST /en/api/IntegrationApi/InventoryItemSearch`
   Use this for fuller product master data (dimensions, pack types, categories) when your box
   suggestion or dimensional-weight algorithm needs it.

3. **Run your own rate shopping, box suggestion and label generation.**
   Entirely on your side. Logiwa has no rate or label endpoint.

4. **Return the label and tracking number to Logiwa.**
   `POST /en/api/IntegrationApi/UploadDocument`
   Upload the label image as a document against the order. Packers then print it from the Logiwa
   UI. Use `ListOrderDocuments` and `DownloadDocument` to verify or re-retrieve.

## Rules you must follow

- **Never trust the HTTP status line.** Logiwa does not use HTTP status codes for outcome. A
  business failure comes back as HTTP 200 with `{"Success": false, "Errors": ["..."]}`. Read
  `Success` on **every** response before you act on it.
- **There is no idempotency key.** No Logiwa operation accepts one. If a POST times out you
  cannot safely retry it blind — search first (`WarehouseOrderSearch`,
  `ListOrderDocuments`) to see whether the first attempt landed, then decide.
- **Respect the quota.** Standard API users get 60 requests/minute (1 per second), Enterprise 530,
  Premium 1200. Exhaustion returns **HTTP 403** — not 429 — and the retry delay is embedded in
  the message prose as `{t}` milliseconds. There are no `RateLimit-*` or `Retry-After` headers to
  read, so parse the message or back off on a fixed schedule.
- **Paginate.** Search operations take `PageSize` (default and max **200**) and
  `SelectedPageIndex` (1-based) in the body, and return `PageCount` and `RecordCount`.
- **Dates going in** use `MM.DD.YYYY hh:mm:ss` in **US Pacific Time**. Dates arriving on webhooks
  use an ISO-8601-like form. Convert in both directions; do not assume the caller's timezone.

## Reversibility

Uploading a document is additive. If you need to stop an order you have not yet labelled, see
`logiwa-order-intake-and-fulfillment` — cancellation closes once picking or packing starts, and
there is **no documented un-ship or label-void operation**.

## Reference

- Carrier partner flow — <https://developer.logiwa.com/?id=654e30abe6466c26c496d014>
- Getting Started (limits, pagination, error envelope) — <https://developer.logiwa.com/?id=5df0d8bfe6466c2eec992f31>
- Conventions — `conventions/logiwa-conventions.yml`
- Errors — `errors/logiwa-error-codes.yml`
