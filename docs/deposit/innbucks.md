
# InnBucks Deposit

This endpoint generates a payment reference code for InnBucks. The user can use this code to pay at an InnBucks counter or via the InnBucks app.

**Method:** POST

**Endpoint:** `/api/v1/innbucks/pay`

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Parameters

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `amount` | Float | **Yes** | The amount to deposit (USD). Minimum `0.1`. |

### Example Request

```json
{
    "amount": 25.00
}
```

### Response

If successful, the API returns `200 OK`. The `data.code` field contains the reference required to make the payment.

```json
{
    "success": true,
    "message": "Payment initiated",
    "data": {
        "id": 105,
        "reference": "DEP_INN98765",
        "amount": "25.00",
        "currency": "USD",
        "code": "123 456 789",
        "status": "PENDING",
        "status_message": null,
        "expires_at": "2025-12-02T08:15:00.000000Z",
        "created_at": "2025-12-02T08:00:00.000000Z"
    }
}
```
