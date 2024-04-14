## Buy Bundle Voucher

This endpoint allows purchasing bundle vouchers.

**Method:** POST

**Endpoint:** `/api/v1/bundles/voucher/buy/{bundle}`

Purchases the specified quantity of bundle vouchers. Requires sufficient balance in the user's wallet. On success, returns details of the purchased vouchers along with updated wallet balance and earned commission.

### Headers

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |

### Parameters

| Name     | Type    | Description                           | Validation                |
|----------|---------|---------------------------------------|---------------------------|
| bundle   | integer | The ID of the bundle to purchase vouchers for | Required, valid bundle ID |
| quantity | integer | The number of vouchers to purchase    | Required, integer, min: 1 |

### Responses

#### Success Response:
```json
{
  "success": true,
  "message": "{Bundle Name} purchase was successful",
  "data": {
    "name": "Daily Bundle",
    "amount": 10,
    "voucher_value": 1,
    "currency": "USD",
    "status": "success",
    "vouchers": [
      "1234567890",
      "0987654321"
    ],
    "balance": {
      "balance": 90,
      "currency": "USD",
      "profit_on_hold": 0
    },
    "commission": "USD0.5"
  }
}
```

#### Error Response:
```json
{
  "success": false,
  "message": "You do not have enough balance to make this transaction."
}
```

[Previous](/bundle/buy-direct.md)
