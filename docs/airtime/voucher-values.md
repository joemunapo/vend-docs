# Voucher Values

This endpoint allows you to retrieve the available voucher values for a specific carrier.

**Method:** `GET`

**Endpoint:** `/api/v1/airtime/direct/{carrier}/values`

This endpoint returns the available voucher values for a specific carrier identified by `carrier`. It also indicates whether custom amount is allowed for the carrier.

**Headers:**

| Name          | Value            |
|---------------|------------------|
| Accept        | application/json |
| Authorization | Bearer {token}   |

**Parameters:**

| Name    | Type    | Description                       |
|---------|---------|-----------------------------------|
| carrier | string  | The name or identifier of the carrier |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Carrier voucher values",
    "allow_custom_amount": false,
    "data": [5, 10, 20, 50, 100]
  }
  ```

[Prev: Voucher Carriers](./voucher-carriers.md) | [Next: Buy Voucher Airtime](./buy-voucher-airtime.md)
