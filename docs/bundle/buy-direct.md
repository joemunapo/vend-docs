## Buy Direct Bundle

This endpoint allows purchasing a bundle directly for a mobile number.

**Method:** POST

**Endpoint:** `/api/v1/bundles/buy/{bundle}`

Purchases the specified bundle and applies it directly to the provided mobile number. Requires sufficient balance in the user's wallet. On success, returns details of the purchased bundle along with updated wallet balance and earned commission.

### Headers

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |

### Parameters

| Name        | Type    | Description                                   | Validation                |
|-------------|---------|-----------------------------------------------|---------------------------|
| bundle      | integer | The ID of the bundle to purchase              | Required, valid bundle ID |
| mobile_phone| string  | The mobile number to apply the bundle to      | Required, valid mobile number for supported carriers |

### Responses

#### Success Response:
```json
{
  "success": true,
  "message": "{Bundle Name} bundle purchased successfully",
  "data": {
    "name": "Daily Bundle",
    "amount": 1,
    "currency": "USD",
    "mobile_phone": "0775123456",
    "status": "success",
    "balance": {
      "balance": 99,
      "currency": "USD",
      "profit_on_hold": 0
    },
    "commission": "USD0.05"
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

[Previous](/bundle/available-bundles.md) | [Next](/bundle/buy-voucher.md)
