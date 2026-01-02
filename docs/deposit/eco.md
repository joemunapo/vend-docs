# EcoCash Deposit

This endpoint initiates a deposit request using EcoCash. It triggers a USSD push to the user's mobile device to authorize the transaction.

**Method:** POST

**Endpoint:** `/api/v1/ecocash/pay`

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Parameters

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `amount` | Float | **Yes** | The amount to deposit (USD). Minimum `0.1`. |
| `ecocash_phone` | String | **Yes** | The Econet phone number to bill. Must be a valid Zimbabwean Econet number. |
| `poll_url` | String | No | Optional webhook URL for server clients. If provided, we will forward the deposit status updates to this URL. Include your reference as a query parameter in the URL (e.g. `?reference=ORDER_12345`). |

### Example Request

```json
{
    "amount": 10.00,
    "ecocash_phone": "0771234567",
    "poll_url": "https://client.example.com/webhooks/ecocash?reference=ORDER_12345"
}
````

### Response

If successful, the API returns `200 OK` with a message instructing the user to check their mobile device.

```json
{
    "success": true,
    "message": "Check mobile to complete",
    "data": {
        "id": 102,
        "reference": "DEP_ABC123XYZ",
        "amount": "10.00",
        "currency": "USD",
        "code": "ECOCASH",
        "status": "PENDING",
        "status_message": "Check mobile to complete payment.",
        "created_at": "2025-12-02T08:00:00.000000Z"
    }
}
```
