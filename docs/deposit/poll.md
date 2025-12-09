# Check Transaction Status (Polling)

Since mobile money and counter payments are asynchronous, you should poll this endpoint to check if a transaction has been successfully completed.

**Method:** GET

**Endpoint:** `/api/v1/{method}/poll/{id}`

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### URL Parameters

| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `method` | String | **Yes** | The payment method used. Allowed values: `ecocash`, `innbucks`, `omari`. |
| `id` | Integer | **Yes** | The unique ID of the payment transaction. |

### Example Request

```http
GET /api/v1/ecocash/poll/102
````

### Responses

#### 1\. Payment Pending (EcoCash Example)

If the user has not yet authorized the payment on their phone.

```json
{
    "success": true,
    "message": "Payment pending",
    "data": {
        "id": 102,
        "amount": "10.00",
        "currency": "USD",
        "status": "PENDING",
        "expires_at": "2025-12-02T08:15:00.000000Z",
        "created_at": "2025-12-02T08:00:00.000000Z",
        "poll_url": "[https://api.xash.co.zw/api/v1/ecocash/poll/102](https://api.xash.co.zw/api/v1/ecocash/poll/102)",
        "status_message": "Check mobile to complete payment."
    }
}
```

#### 2\. Payment Pending (InnBucks Example)

Includes the payment code required for the teller.

```json
{
    "success": true,
    "message": "Payment pending",
    "data": {
        "id": 105,
        "amount": "25.00",
        "currency": "USD",
        "status": "PENDING",
        "expires_at": "2025-12-02T08:15:00.000000Z",
        "created_at": "2025-12-02T08:00:00.000000Z",
        "poll_url": "[https://api.xash.co.zw/api/v1/innbucks/poll/105](https://api.xash.co.zw/api/v1/innbucks/poll/105)",
        "code": "123456789"
    }
}
```

#### 3\. Payment Successful

Once the callback is received and the transaction is finalized.

```json
{
    "success": true,
    "message": "Payment successful",
    "data": {
        "id": 102,
        "amount": "10.00",
        "currency": "USD",
        "status": "SUCCESS",
        "expires_at": "2025-12-02T08:15:00.000000Z",
        "created_at": "2025-12-02T08:00:00.000000Z",
        "poll_url": "[https://api.xash.co.zw/api/v1/ecocash/poll/102](https://api.xash.co.zw/api/v1/ecocash/poll/102)",
        "status_message": "Payment successful"
    }
}
```