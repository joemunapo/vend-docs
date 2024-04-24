# Account History

## Description

Retrieve a user's account history.

### Method

GET

### Endpoint

`/api/v1/reports/history/{currency}`

### Endpoint Short Description

Get account history for a specific currency.

### Headers

| Name          | Value            |
| ------------- | ---------------- |
| Accept        | application/json |
| Authorization | Bearer {token}   |

### Parameters

| Name     | Type   | Required | Short Description        |
| -------- | ------ | -------- | ------------------------ |
| currency | string | true     | Currency code (e.g. USD) |

### Body

None

### Example Response

```json
{
  "success": true,
  "message": "Transactions retrieved successfully",
  "data": [
    {
      "id": 1,
      "amount": 1000,
      "type": "deposit",
      "currency": "USD",
      "created_at": "2024-04-23T14:30:00+00:00"
    },
    {
      "id": 2,
      "amount": 35,
      "type": "deposit",
      "currency": "USD",
      "created_at": "2024-04-23T14:31:00+00:00"
    },
    ...
  ]
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
