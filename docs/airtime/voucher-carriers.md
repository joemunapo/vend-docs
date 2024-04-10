# Voucher Carriers

This endpoint allows you to retrieve a list of carriers that support voucher airtime.

**Method:** `GET`

**Endpoint:** `/api/v1/airtime/direct/voucher/carriers`

This endpoint returns a list of carriers that support voucher airtime along with their details such as ID, name, and commission.

**Headers:**

| Name          | Value            |
|---------------|------------------|
| Accept        | application/json |
| Authorization | Bearer {token}   |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Voucher airtime carriers",
    "data": [
      {
        "id": 1,
        "name": "Carrier 1",
        "commission": 0.05
      },
      {
        "id": 2,
        "name": "Carrier 2",
        "commission": 0.03
      }
    ]
  }
  ```

[Prev: Buy Direct Airtime](./buy-direct-airtime.md) | [Next: Voucher Values](./voucher-values.md)
