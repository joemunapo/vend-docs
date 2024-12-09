## Buy Wifi Voucher

This endpoint allows purchasing wifi vouchers.

**Method:** POST

**Endpoint:** `/api/v1/mobile-payment`

Purchases the specified quantity of wifi vouchers. Requires sufficient balance in the user's wallet. On success, returns details of the purchased vouchers along with updated wallet balance and earned commission.

### Headers

| Name          | Value          |
| ------------- | -------------- |
| Authorization | Bearer {token} |

### JSON Example Parameters

```json
{
  "reference": "Test12321",
  "phone": "0771111111",
  "method": "ecocash",
  "items": [
    {
      "data_limit": "2GB",
      "amount": 5.0,
      "duration": 3,
      "quantity": 2
    }
  ]
}
```

### Responses

#### Success Response:

```json
{
  "message": "Payment initiated successfully. Use the payment_id to check status.7",
  "payment_id": "payment_xxxxx"
}
```

#### Error Response:

```json
{
  "error": "PayNow mobile payment failed"
}
```

### Check Payment Status

**Method:** POST

**Endpoint:** `api/v1/mobile-payment/status`

### Json sample data

```json
{
  "payment_id": "payment_xxxxx"
}
```

### Responses

#### Success Response:

```json
{
  "payment_id": "payment_xxxx",
  "status": "paid",
  "pins": ["12121212", "23244555"]
}
```

[Previous](/wifi/buy-direct.md)
