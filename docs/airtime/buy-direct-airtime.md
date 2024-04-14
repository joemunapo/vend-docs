# Buy Direct Airtime

This endpoint allows you to purchase direct airtime for a mobile phone number.

**Method:** `POST`

**Endpoint:** `/api/v1/airtime/direct`

This endpoint processes a direct airtime recharge request. It requires the mobile phone number, amount, and currency.

**Headers:**

| Name          | Value            |
|---------------|------------------|
| Accept        | application/json |
| Content-Type  | application/json |
| Authorization | Bearer {token}   |

**Body:**

| Name         | Type    | Description                           | Validation                           |
|--------------|---------|---------------------------------------|--------------------------------------|
| mobile_phone | string  | The mobile phone number               | Required, valid mobile phone number  |
| amount       | numeric | The amount of airtime to purchase     | Required, numeric                    |
| currency     | string  | The currency of the airtime purchase  | Required, valid currency             |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Recharge to +1234567890 was successful",
    "data": {
      "name": "Carrier Name",
      "amount": 10,
      "currency": "USD",
      "mobile_phone": "+1234567890",
      "status": "success",
      "balance": {
        "balance": 90,
        "currency": "USD",
        "profit_on_hold": 0
      },
      "commission": "USD0.5"
    }
  }
  ```

- 400 Bad Request:
  ```json
  {
    "success": false,
    "message": "You do not have enough balance to make this transaction."
  }
  ```

[Prev: Direct Carriers](/airtime/carriers.md) | [Next: Voucher Values](/airtime/voucher-values.md)
