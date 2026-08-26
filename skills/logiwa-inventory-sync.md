---
name: logiwa-inventory-sync
description: Keep an external storefront, ERP or marketplace listing in step with Logiwa stock levels using the inventory reports, available-to-promise, and the Inventory Change webhook.
api: Logiwa Integration API
base_url: https://{environment}.logiwa.com/en/api/IntegrationApi
operations:
  - LookUp
  - ListingInventoryReport
  - GetAvailableStockInfo
  - StockDamagedUndamagedReportSearch
  - AvailableToPromiseReportSearch
  - AvailableToPromiseSnapshot
  - GetInventorySnapshot
  - KitInventoryReport
  - InventoryAdjustment
generated: '2026-08-25'
method: generated
source: https://developer.logiwa.com/?id=5df0db66e6466c2eec992f53
---

# Sync stock with Logiwa

## Pick the right read

| You need | Operation |
|---|---|
| Sellable quantity per item, per warehouse/client | `ListingInventoryReport` |
| Quantity broken down by location | `GetAvailableStockInfo` |
| Damaged vs undamaged split | `StockDamagedUndamagedReportSearch` |
| What you can actually promise a customer | `AvailableToPromiseReportSearch` |
| Kit / bundle availability from components | `KitInventoryReport` |
| A point-in-time file for a warehouse + client | `GetInventorySnapshot`, `AvailableToPromiseSnapshot` |

Resolve `WarehouseList` and `DepositorList` ids from `LookUp` once and cache them.

## Prefer events to polling

Subscribe to the **Inventory Change** webhook. Its payload carries `LogiwaInventoryItemId`,
`LogiwaInventoryItemCode`, `Client`, `Warehouse`, `WarehouseId`, `TotalInventoryQuantity` and
`AvailableQuantity` — usually enough to update a listing without a follow-up read.

Two published caveats that must shape your design:

- **Delivery is not guaranteed.** Logiwa says so plainly and tells you to run reconciliation jobs.
  Schedule a periodic full `ListingInventoryReport` sweep regardless of webhook health.
- **One callback per warehouse + client + event type.** If another integration already subscribed
  to Inventory Change for that scope, yours will never fire. Confirm the subscription is yours.

## Snapshots for bulk

`GetInventorySnapshot` and `AvailableToPromiseSnapshot` return a document URL
(`https://yourApp.logiwa.com/CustomerBase/Documents/...json`) rather than inline rows. Use these
for periodic full syncs instead of paging a report 200 rows at a time — it is the difference
between one request and hundreds against a 60/minute budget.

## Writing back

`POST /en/api/IntegrationApi/InventoryAdjustment` changes stock levels.

**There is no undo.** A wrong adjustment is corrected by posting a compensating adjustment, which
lands as a new transaction in the movement ledger — the original is not removed. Get the sign and
quantity right before you send it, and log what you sent, because there is no idempotency key and
no request id to trace with.

`InventoryPropertyUpdate` / `InventoryPropertyBulkUpdate` change stock properties (for example
quarantine state) without moving quantity.

## Rules

- `Success: false` arrives with HTTP 200. Check the body every time.
- Bulk item creation (`InsertInventoryItem`) caps at 50 per call.
- 403 = throttled. Parse `{t}` from the message and back off.
- `PageSize` max 200. Use snapshots for anything larger.

## Reference

- Inventory — <https://developer.logiwa.com/?id=5df0db66e6466c2eec992f53>
- Inventory Change webhook — <https://developer.logiwa.com/?id=64142d6de6466c4dc01efb32>
- Rate limits — `rate-limits/logiwa-rate-limits.yml`
