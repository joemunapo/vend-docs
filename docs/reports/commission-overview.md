# Commission Overview

Returns a simple summary of commission that is still on hold and the latest commission release batches.

## Endpoint

`GET /api/v1/reports/commission-overview/{currency}`

## Headers

| Name | Value |
| --- | --- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

## Path Parameters

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| currency | string | Yes | Wallet currency code, for example `USD` |

## Success Response

```json
{
  "success": true,
  "message": "Commission summary retrieved successfully",
  "data": {
    "currency": "USD",
    "pending": {
      "total": 3.75,
      "release_at": "2026-06-17T04:30:00+02:00",
      "is_due": false
    },
    "releases": [
      {
        "released_at": "2026-06-13T04:30:00+02:00",
        "amount": 10,
        "currency": "USD",
        "transaction_count": 2
      }
    ]
  }
}
```

## Response Fields

| Field | Type | Description |
| --- | --- | --- |
| data.currency | string | Currency requested in the URL |
| data.pending.total | number | Total commission currently pending release |
| data.pending.release_at | string or null | Earliest scheduled release date for pending commission |
| data.pending.is_due | boolean | Whether the pending commission release date has passed |
| data.releases | array | Latest release batches, newest first, limited to 10 batches |
| data.releases[].released_at | string | Date and time the batch was released |
| data.releases[].amount | number | Total amount released in that batch |
| data.releases[].currency | string | Currency released |
| data.releases[].transaction_count | integer | Number of commission transactions included in the batch |

## Notes

- This endpoint is intentionally summarized for app display.
- Individual commission cents and source transaction details are available from account history and transaction detail endpoints.
- Releases are grouped by release batch, so users can see how much was added to their wallet at each release.
