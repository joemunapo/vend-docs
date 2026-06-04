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
| `amount` | Float | **Yes** | The USD wallet amount to credit after the payment succeeds. Minimum `0.1`. |
| `ecocash_phone` | String | **Yes** | The Econet phone number to bill. Must be a valid Zimbabwean Econet number. |
| `charge_currency` | String | No | Use `ZWG` to bill the customer in ZWG while crediting the USD wallet. Defaults to `USD`. |
| `callback_url` | String | No | Optional HTTP(S) callback URL for server clients. If provided, Xash will POST deposit status updates to this URL. Browser and mobile-only clients can omit it and use `data.poll_url` instead. |
| `poll_url` | String | No | Legacy alias for `callback_url`. New integrations should use `callback_url`. |

### Example Request

```json
{
    "amount": 10.00,
    "ecocash_phone": "0771234567",
    "callback_url": "https://client.example.com/webhooks/xash/ecocash?reference=ORDER_12345"
}
```

### ZWG EcoCash Request

To bill the customer in ZWG, send `charge_currency: "ZWG"`. The `amount` remains the USD amount that will be credited to the user's wallet.

```json
{
    "amount": 10.00,
    "charge_currency": "ZWG",
    "ecocash_phone": "0771234567",
    "callback_url": "https://client.example.com/webhooks/xash/ecocash?reference=ORDER_12345"
}
```

If the configured ZWG rate is `32`, this request credits `USD 10.00` after success and bills the provider charge as `ZWG 320.00`.

### Usage

**API Request**

```bash
curl -X POST https://your-api/v1/ecocash/pay \
  -H "Authorization: Bearer {token}" \
  -H "Content-Type: application/json" \
  -d '{
    "amount": 10.00,
    "ecocash_phone": "0771234567",
    "callback_url": "https://your-server.com/webhook?reference=ORDER_12345"
  }'
```

**Webhook Callback**

When the deposit status changes to `SUCCESS` or `FAILED`/`EXPIRED`, your `callback_url` will receive a POST request from Xash:

```json
{
  "id": 123,
  "reference": "DEP_ABC123XYZ",
  "method": "ecocash",
  "status": "SUCCESS",
  "amount": "10.00",
  "currency": "USD",
  "status_message": "Payment successful",
  "gateway_reference": null,
  "charge_amount": "320.00",
  "charge_currency": "ZWG",
  "exchange_rate": 32,
  "wallet_amount": "10.00",
  "wallet_currency": "USD",
  "updated_at": "2026-01-02T23:45:00.000000Z"
}
```

**Tip**

Put your order reference as a query parameter in `callback_url` (e.g., `?reference=ORDER_12345`) to correlate callbacks with your orders.

### Response

If successful, the API returns `200 OK` with a message instructing the user to check their mobile device.

```json
{
    "success": true,
    "message": "Check mobile to complete payment.",
    "data": {
        "id": 102,
        "amount": "10.00",
        "currency": "USD",
        "payment_method": "ecocash",
        "charge_amount": "320.00",
        "charge_currency": "ZWG",
        "exchange_rate": 32,
        "status": "PENDING",
        "status_message": "Check mobile to complete payment.",
        "poll_url": "https://api.xash.co.zw/api/v1/ecocash/poll/102",
        "created_at": "2025-12-02T08:00:00.000000Z"
    }
}
```
