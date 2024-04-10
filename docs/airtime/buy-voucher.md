# Buy Voucher Airtime

This endpoint allows you to purchase voucher airtime for a specific carrier.

**Method:** `POST`

**Endpoint:** `/api/v1/airtime/direct/voucher/{carrier}`

This endpoint processes a voucher airtime purchase request for a specific carrier identified by `carrier`. It requires the amount, currency, and quantity of vouchers.

**Headers:**

| Name          | Value            |
|---------------|------------------|
| Accept        | application/json |
| Content-Type  | application/json |
| Authorization | Bearer {token}   |

**Parameters:**

| Name    | Type    | Description                       |
|---------|---------|-----------------------------------|
| carrier | string  | The name or identifier of the carrier |

**Body:**

| Name     | Type    | Description                             | Validation                   |
|----------|---------|-----------------------------------------|------------------------------|
| amount   | numeric | The amount of each voucher              | Required, numeric            |
| currency | string  | The currency of the voucher purchase    | Required, valid currency     |
| quantity | integer | The number of vouchers to purchase      | Required, integer            |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Carrier Name purchase was successful",
    "data": {
      "status": "success",
      "name": "Carrier Name",
      "amount": 20,
      "voucher_value": 10,
      "currency": "USD",
      "balance": {
        "balance": 80,
        "currency": "USD",
        "profit_on_hold": 0
      },
      "vouchers": [
        "1234567890",
        "0987654321"
      ],
      "commission": "USD1"
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

[Prev: Voucher Values](voucher-values.md)