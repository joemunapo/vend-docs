
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
| `amount` | Float | **Yes** | The USD wallet amount to credit after the payment succeeds. Minimum `0.1`. |
| `charge_currency` | String | No | Use `ZWG` to bill the customer in ZWG while crediting the USD wallet. Defaults to `USD`. |
| `callback_url` | String | No | Optional HTTP(S) callback URL for server clients. If provided, Xash will POST deposit status updates to this URL. Browser and mobile-only clients can omit it and use `data.poll_url` instead. |
| `poll_url` | String | No | Legacy alias for `callback_url`. New integrations should use `callback_url`. |

### Example Request

```json
{
    "amount": 25.00,
    "callback_url": "https://client.example.com/webhooks/xash/innbucks?reference=ORDER_12345"
}
```

### ZWG InnBucks Request

To bill the customer in ZWG, send `charge_currency: "ZWG"`. The `amount` remains the USD amount that will be credited to the user's wallet.

```json
{
    "amount": 10.00,
    "charge_currency": "ZWG",
    "callback_url": "https://client.example.com/webhooks/xash/innbucks?reference=ORDER_12345"
}
```

If the configured ZWG rate is `32`, this request credits `USD 10.00` after success and bills the provider charge as `ZWG 320.00`.

### Response

If successful, the API returns `200 OK`. The `data.code` field contains the reference required to make the payment.

```json
{
    "success": true,
    "message": "Payment initiated",
    "data": {
        "id": 105,
        "amount": "25.00",
        "currency": "USD",
        "payment_method": "innbucks",
        "charge_amount": "25.00",
        "charge_currency": "USD",
        "exchange_rate": null,
        "code": "123 456 789",
        "status": "PENDING",
        "status_message": null,
        "poll_url": "https://api.xash.co.zw/api/v1/innbucks/poll/105",
        "expires_at": "2025-12-02T08:15:00.000000Z",
        "created_at": "2025-12-02T08:00:00.000000Z"
    }
}
```

When the deposit is finalized, account history for the USD wallet will show the credited wallet amount. ZWG deposits include the charge currency in the transaction name, for example `Deposit via InnBucks (ZWG)`.
