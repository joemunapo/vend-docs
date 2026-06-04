# Account History

This endpoint retrieves account history for a specific currency and supports server-side filtering.

**Method:** `GET`

**Endpoint:** `/api/v1/reports/history/{currency}`

### Headers

| Name          | Value            |
| ------------- | ---------------- |
| Accept        | application/json |
| Authorization | Bearer {token}   |

### Path Parameters

| Name     | Type   | Required | Description                  |
| -------- | ------ | -------- | ---------------------------- |
| currency | string | Yes      | Currency code, for example `USD` |

### Query Parameters

| Name            | Type            | Required | Description |
| --------------- | --------------- | -------- | ----------- |
| name            | string          | No       | Filter by a single transaction name as shown in history, for example `Deposit` |
| names           | string or array | No       | Filter by multiple transaction names |
| type            | string          | No       | Filter by a single transaction type |
| types           | string or array | No       | Filter by multiple transaction types |
| from_date       | string          | No       | Return transactions from this date onward in `YYYY-MM-DD` format |
| to_date         | string          | No       | Return transactions up to this date in `YYYY-MM-DD` format |
| search          | string          | No       | Search transactions by transaction ID / UUID text |
| per_page        | integer         | No       | Control the number of records returned per page |

### Example Requests

Fetch account history:

```http
GET /api/v1/reports/history/USD
```

Filter by one transaction name:

```http
GET /api/v1/reports/history/USD?name=deposit
```

Filter by multiple transaction names:

```http
GET /api/v1/reports/history/USD?names[]=deposit&names[]=transfer
```

Or:

```http
GET /api/v1/reports/history/USD?names=deposit,transfer
```

Filter by one transaction type:

```http
GET /api/v1/reports/history/USD?type=deposit
```

Filter by multiple transaction types:

```http
GET /api/v1/reports/history/USD?types[]=deposit&types[]=transfer
```

Or:

```http
GET /api/v1/reports/history/USD?types=deposit,transfer
```

Filter by date range:

```http
GET /api/v1/reports/history/USD?from_date=2026-03-01&to_date=2026-03-30
```

Search by reference:

```http
GET /api/v1/reports/history/USD?search=8d83d4d1
```

Control pagination:

```http
GET /api/v1/reports/history/USD?per_page=25
```

Combine filters:

```http
GET /api/v1/reports/history/USD?names[]=deposit&from_date=2026-03-01&to_date=2026-03-30&per_page=20
```

Or:

```http
GET /api/v1/reports/history/USD?types[]=transfer&search=abc123
```

### Success Response

```json
{
  "success": true,
  "message": "Transactions retrieved successfully",
  "data": [
    {
      "type": "deposit",
      "name": "Deposit",
      "id": "8d83d4d1-aaaa-bbbb-cccc-1234567890ab",
      "reference": "1234567890AB",
      "amount": "35.00",
      "success": true,
      "created_at": "2026-03-30T08:15:00.000000Z",
      "commission": "0.000",
      "receipt_footer": "Get airtime/bundle on your change from as little as 10 cents.",
      "currency": "USD",
      "attributes": {}
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

### Sample Error Response

```json
{
  "success": false,
  "message": "Invalid currency code",
  "error": "Invalid parameter"
}
```

### Notes

- `currency` is part of the URL path, for example `USD`.
- Use `name` when filtering by the label users already see in history.
- Use `names` or `types` when you need multiple values.
- Dates should be sent in `YYYY-MM-DD` format.
- ZWG mobile-money deposits still appear in `/api/v1/reports/history/USD` because the wallet is credited in USD. Their history name includes the charge currency, for example `Deposit via EcoCash (ZWG)`.
- Pagination information is returned in the `meta` object.
