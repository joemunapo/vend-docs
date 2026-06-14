# Commissions

> Deprecated: use [Commission Overview](commission-overview.md) for new app versions.

Returns the legacy paginated list of individual commission payout transactions. This endpoint remains available for older app versions that still display commission transaction rows.

## Endpoint

`GET /api/v1/reports/commission/{currency}/{range?}`

## Headers

| Name | Value |
| --- | --- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

Successful responses include the `Deprecation: true` response header.

## Path Parameters

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| currency | string | Yes | Wallet currency code, for example `USD` |
| range | string | No | Legacy period filter such as `today`, `yesterday`, `this_month`, or a month name |

## Query Parameters

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| per_page | integer | No | Number of commission transaction rows per page |

## Success Response

```json
{
  "success": true,
  "message": "Transactions retrieved successfully",
  "data": [
    {
      "name": "Commission payout",
      "type": "commission",
      "id": "8d83d4d1-aaaa-bbbb-cccc-1234567890ab",
      "reference": "1234567890AB",
      "for_transaction": "sale-transaction-id",
      "amount": "0.25",
      "currency": "USD",
      "payout_date": "17 Jun 2026",
      "payout_status": "pending",
      "status": "PENDING",
      "parent": null,
      "created_at": "2026-06-14T08:15:00.000000Z"
    }
  ],
  "meta": {
    "total": 1,
    "per_page": 15,
    "current_page": 1,
    "last_page": 1,
    "from": 1,
    "to": 1
  }
}
```

## Notes

- This endpoint is maintained for older app versions.
- New app versions should use `/api/v1/reports/commission-overview/{currency}`.
- Use transaction history or transaction detail when a user needs to inspect the individual cents and source transaction.
