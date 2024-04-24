# Mini Statement API

Retrieves a mini statement for a specified currency and period.

## Endpoint

`GET /api/v1/reports/mini/{currency}/{period}`

## Description

This endpoint returns a summary of transactions for a given currency and period. The summary includes the opening balance, closing balance, total debits, total credits, total profit, and a breakdown of transactions by type.

## Headers

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |
| Content-Type  | application/json |

## Parameters

| Name     | Type   | Required | Description                                                    |
|----------|--------|----------|----------------------------------------------------------------|
| currency | string | Yes      | The currency code (e.g., "USD")                                |
| period   | string | Yes      | The period for the mini statement ("today", "yesterday", "this_month", "last_month", or a specific month like "april") |

## Response

### Success Response

```json
{
  "success": true,
  "message": "Mini-statement for April 2024 fetched successfully",
  "data": {
    "currency": "USD",
    "start": "2024-04-01 00:00:00",
    "end": "2024-04-30 23:59:59",
    "period": "April 2024",
    "opening_balance": "0.00",
    "closing_balance": "1,023.40",
    "sales": [
      {
        "name": "Voucher Bundle",
        "total": "0.45",
        "profit": "0.027",
        "count": "1"
      },
      {
        "name": "Direct Bundle",
        "total": "0.15",
        "profit": "0.009",
        "count": "1"
      },
      {
        "name": "Voucher",
        "total": "1.00",
        "profit": "0.060",
        "count": "1"
      },
      {
        "name": "Direct Airtime",
        "total": "5.00",
        "profit": "0.300",
        "count": "1"
      }
    ],
    "transactions": [
      {
        "name": "Transfer",
        "in_total": "5.000",
        "out_total": "10.000",
        "count": "2"
      },
      {
        "name": "Sales",
        "in_total": "0.000",
        "out_total": "6.600",
        "count": "4"
      },
      {
        "name": "Profit",
        "in_total": "0.396",
        "out_total": "0.000",
        "count": "4"
      },
      {
        "name": "Deposit",
        "in_total": "1,035.000",
        "out_total": "0.000",
        "count": "2"
      }
    ],
    "debit_total": "16.600",
    "credit_total": "1,040.000",
    "profit_total": "0.396",
    "transactions_count": "12"
  }
}
```

### Error Response

```json
{
  "success": false,
  "message": "Invalid period provided",
  "data": null
}
```

## Sample Error Responses

- `400 Bad Request` - Returned when an invalid period is provided
  ```json
  {
    "success": false,
    "message": "Invalid period provided",
    "data": null
  }
  ```