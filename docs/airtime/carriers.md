# Supported Carriers

This endpoint allows you to retrieve a list of supported carriers for various services such as direct airtime recharge, voucher purchases, and bundle purchases.

**Method:** `GET`

**Endpoint:** `/api/v1/airtime/carriers`

This endpoint returns a detailed list of supported carriers, including essential information such as the carrier's ID, name, and commission rate. Additionally, it provides flags that indicate the specific services supported by each carrier. For example, `has_voucher: true` signifies that the carrier supports voucher purchases, while `has_direct_airtime: true` indicates that the carrier allows direct airtime recharge.

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
    "message": "Supported carriers",
    "data": [
      {
        "id": 1,
        "name": "Carrier 1",
        "commission": 0.05,
        "has_direct_airtime": true,
        "has_voucher": true,
        "has_bundle": false
      },
      {
        "id": 2,
        "name": "Carrier 2",
        "commission": 0.03,
        "has_direct_airtime": true,
        "has_voucher": false,
        "has_bundle": true
      }
    ]
  }
  ```

The response provides a comprehensive overview of each supported carrier, including the following details:

- `id`: The unique identifier of the carrier.
- `name`: The name of the carrier.
- `commission`: The commission rate associated with the carrier.
- `has_direct_airtime`: A boolean flag indicating whether the carrier supports direct airtime recharge.
- `has_voucher`: A boolean flag indicating whether the carrier supports voucher purchases.
- `has_bundle`: A boolean flag indicating whether the carrier supports bundle purchases.

By leveraging this information, you can dynamically adapt your application's functionality based on the capabilities of each carrier, providing a seamless and tailored experience for your users.

[Next: Buy Direct Airtime](/airtime/buy-direct-airtime.md)