---
name: logiwa-order-intake-and-fulfillment
description: Push shipment orders into Logiwa from an OMS or storefront, follow them to shipment, and cancel them while cancellation is still possible.
api: Logiwa Integration API
base_url: https://{environment}.logiwa.com/en/api/IntegrationApi
operations:
  - LookUp
  - InsertShipmentOrder
  - InsertShipmentOrderWithBulkResult
  - WarehouseOrderSearch
  - WarehouseOrderStatusReportSearch
  - WarehouseOrderDetailSearch
  - CancelShipmentOrder
generated: '2026-08-25'
method: generated
source: https://developer.logiwa.com/?id=5df0dad1e6466c2eec992f49
---

# Send orders to Logiwa and follow them to shipment

## Step 0 — resolve your reference ids first

`POST /en/api/IntegrationApi/LookUp`

One call returns 28 reference lists as `Id`/`Description` pairs — `WarehouseList`,
`DepositorList`, `CarrierList`, `ChannelList`, `ShipmentOrderStatusList`,
`ShipmentMethodList`, `ShipmentOrderTypeList`, `OrderCancelReason` and more. An empty body
returns all of them; send a `LookupList` array of type numbers to narrow it.

**Cache these.** Do not resolve a warehouse id on every order — you have 60 requests/minute on the
Standard tier and you will spend your whole budget on lookups. Note that LookUp data is refreshed
**5 minutes after** the underlying transaction, so a warehouse created moments ago will not be there yet.

## Step 1 — create the orders

- `POST /en/api/IntegrationApi/InsertShipmentOrder` — up to **50 orders** per call, **400 lines** total.
- `POST /en/api/IntegrationApi/InsertShipmentOrderWithBulkResult` — same, **240 lines**, returns a
  per-item result so you can tell which members of the batch failed.

Prefer the bulk-result variant for anything non-trivial: with the plain variant a partial failure
gives you one `Errors` array and no reliable way to map an error back to an input row.

## Step 2 — follow the order

- `POST /en/api/IntegrationApi/WarehouseOrderSearch` — list orders; set `IsGetOrderDetails` for lines.
- `POST /en/api/IntegrationApi/WarehouseOrderStatusReportSearch` — status-focused search.
- `POST /en/api/IntegrationApi/WarehouseOrderDetailSearch` — line-level detail.
- `POST /en/api/IntegrationApi/WarehouseOrderGetID` — resolve a Logiwa order id.

**Prefer webhooks over polling.** Subscribe to `SO Creation Info`, `SO Status Update`,
`Order Shipment Info` and `Shipment Tracking Info` in the Logiwa UI. Logiwa recommends this
explicitly as the way to stay inside the rate limit. But Logiwa also states delivery is **not
guaranteed** and ordering is **not guaranteed across topics** — so keep a periodic reconciliation
search running as well, and never treat a missing webhook as a missing event.

## Step 3 — cancel, while you still can

`POST /en/api/IntegrationApi/CancelShipmentOrder` — up to **50** orders per call.

Logiwa states: *"If the order has started to be picked up or packed, the users will be notified of
the packing or shipping processes."* Treat the start of picking or packing as the close of the
cancellation window. Check status before you cancel, and handle the case where the API tells you
it is already too late.

**There is no reversal after shipment.** No un-ship, no void-shipment, no label-void operation is
documented. `ShipShipmentOrder` is a one-way door.

## Things Logiwa deliberately does not expose

Allocation, task creation, packing completion, job creation, transfers, picking completion and
carrier label creation are **published as unavailable via the API**. Do not plan a workflow that
needs them; they happen in the Logiwa UI or on the warehouse floor.

## Rules

- Read `Success` in the body on every call. HTTP 200 does not mean it worked.
- No idempotency key exists. After a timeout, search before you retry.
- 403 means throttled, not forbidden. Back off using the `{t}` milliseconds in the message.
- `PageSize` max 200, `SelectedPageIndex` starts at 1.
- Dates in: `MM.DD.YYYY hh:mm:ss`, US Pacific Time.

## Reference

- Shipment Orders — <https://developer.logiwa.com/?id=5df0dad1e6466c2eec992f49>
- Cancel Shipment Order — <https://developer.logiwa.com/?id=5e18596ce6466c20381289c3>
- Look-Up Values — <https://developer.logiwa.com/?id=650066ebe6466c1ed4776e45>
- Webhooks — `asyncapi/logiwa-webhooks.yml`
