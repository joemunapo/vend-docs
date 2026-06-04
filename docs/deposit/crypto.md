# Crypto Deposit

This endpoint creates a CryptoPay deposit address for USDT on BEP20. Show the returned instructions to the customer and poll `data.poll_url` until the deposit reaches a final status.

Crypto deposits are credited to the USD wallet after CryptoPay confirms the payment.

**Method:** POST

**Endpoint:** `/api/v1/crypto/pay`

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Parameters

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `amount` | Float | **Yes** | The amount to deposit in USD. Minimum `0.1`. |
| `reference` | String | No | Your optional customer, order, or sub-user reference. Xash sends CryptoPay a vendor reference in the format `{user_number}` or `{user_number}{reference}`. |
| `callback_url` | String | No | Optional HTTP(S) callback URL for server clients. If provided, Xash will POST status updates to this URL after receiving provider updates. Browser and mobile-only clients can omit it and use `data.poll_url` instead. |
| `poll_url` | String | No | Legacy alias for `callback_url`. New integrations should use `callback_url`. |

`callback_url` must be an HTTP(S) URL without credentials or local/private IP hosts.

### Example Request

```json
{
  "amount": 25.0,
  "reference": "ORDER_12345",
  "callback_url": "https://client.example.com/webhooks/xash/crypto"
}
```

### Usage

```bash
curl -X POST https://api.xash.co.zw/api/v1/crypto/pay \
  -H "Authorization: Bearer {token}" \
  -H "Content-Type: application/json" \
  -d '{
    "amount": 25.0,
    "reference": "ORDER_12345",
    "callback_url": "https://client.example.com/webhooks/xash/crypto"
  }'
```

### Response

If successful, the API returns the payment record, Xash polling URL, and CryptoPay payment instructions.

```json
{
  "success": true,
  "message": "Payment initiated",
  "data": {
    "id": 301,
    "amount": "25.00",
    "currency": "USD",
    "status": "PENDING",
    "expires_at": "2026-05-31T12:15:00.000000Z",
    "created_at": "2026-05-31T12:00:00.000000Z",
    "poll_url": "https://api.xash.co.zw/api/v1/crypto/poll/301",
    "status_message": "Send USDT BEP20 to the provided address.",
    "gateway_reference": "ADDR_9Z7Y6X",
    "vendor_reference": "1000123ORDER_12345",
    "instructions": {
      "address": "0x1234567890abcdef1234567890abcdef12345678",
      "token": "USDT",
      "chain": "BSC",
      "network": "BEP20",
      "amount": "25.00"
    },
    "payment": {
      "gateway_reference": "PAY_ABC123",
      "vendor_reference": "1000123ORDER_12345",
      "status": "pending",
      "amount": "25.00",
      "token": "USDT",
      "chain": "BSC",
      "network": "BEP20"
    }
  }
}
```

### Callback Updates

If you provide `callback_url`, Xash will POST a sanitized status update to your server after CryptoPay sends Xash a provider update. CryptoPay never calls your server directly.

```json
{
  "id": 301,
  "reference": "1000123ORDER_12345",
  "method": "crypto",
  "status": "SUCCESS",
  "amount": "25.00",
  "currency": "USD",
  "status_message": "Crypto payment confirmed",
  "gateway_reference": "ADDR_9Z7Y6X",
  "updated_at": "2026-05-31T12:06:30.000000Z",
  "crypto": {
    "vendor_reference": "1000123ORDER_12345",
    "gateway_reference": "PAY_ABC123",
    "status": "confirmed",
    "amount": "25.00",
    "token": "USDT",
    "chain": "BSC",
    "network": "BEP20",
    "deposit_tx_hash": "0xabc...",
    "sweep_tx_hash": "0xdef...",
    "confirmations": 15
  }
}
```

### Status Flow

| Status | Meaning |
| :--- | :--- |
| `PENDING` | Address created and waiting for payment. |
| `DETECTED`, `READY_TO_SWEEP`, `SWEEPING`, `SWEPT` | Payment is being processed. Continue polling. |
| `SUCCESS` | Payment confirmed and the USD wallet has been credited. |
| `FAILED` | Payment failed and the wallet was not credited. |
| `MANUAL_REVIEW` | Payment needs review. The wallet is not credited automatically. |

### Client Flow

1. Call `/api/v1/crypto/pay`.
2. Show `data.instructions.address`, `data.instructions.network`, `data.instructions.token`, and `data.instructions.amount` to the customer.
3. Poll `data.poll_url` until the status becomes `SUCCESS`, `FAILED`, or `MANUAL_REVIEW`.
4. If you provided `callback_url`, listen for the same status updates on your server.
