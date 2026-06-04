# Card Deposit

This endpoint initiates a Visa or Mastercard deposit. Xash sends the card details to the payment gateway, returns the payment record, and includes `data.redirect_html` when the gateway requires 3D Secure authentication.

Card deposits currently charge and credit USD only.

**Method:** POST

**Endpoint:** `/api/v1/card/pay`

You can also use `/api/v1/payments/receive` with `"method": "card"` and the same card fields.

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Parameters

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `amount` | Float | **Yes** | The USD wallet amount to credit after the payment succeeds. Minimum `0.1`. |
| `pan` | String | **Yes** | Card number. Xash does not store this value. |
| `exp_month` | String | **Yes** | Expiry month, for example `01`. The alias `expMonth` is also accepted. |
| `exp_year` | String | **Yes** | Expiry year, for example `39` or `2039`. The alias `expYear` is also accepted. |
| `security_code` | String | **Yes** | CVV/security code. Xash does not store this value. The alias `securityCode` is also accepted. |
| `first_name` | String | No | Cardholder first name. |
| `last_name` | String | No | Cardholder last name. |
| `email` | String | No | Cardholder email address. |
| `return_url` | String | No | URL the gateway can return to after the 3D Secure flow. The alias `returnUrl` is also accepted. |
| `callback_url` | String | No | Optional HTTP(S) callback URL for server clients. If provided, Xash will POST deposit status updates to this URL. Browser and mobile-only clients can omit it and use `data.poll_url` instead. |
| `poll_url` | String | No | Legacy alias for `callback_url`. New integrations should use `callback_url`. |

Use a publicly reachable HTTPS URL for `callback_url`.

### Example Request

```json
{
  "amount": 10.00,
  "pan": "5123450000000008",
  "exp_month": "01",
  "exp_year": "39",
  "security_code": "100",
  "first_name": "Bill",
  "last_name": "Zinks",
  "email": "test@example.com",
  "return_url": "https://client.example.com/card/return",
  "callback_url": "https://client.example.com/webhooks/xash/card?reference=ORDER_12345"
}
```

### Response

If successful, the API returns `200 OK`. If the gateway requires 3D Secure authentication, inject and execute `data.redirect_html` in your checkout page.

```json
{
  "success": true,
  "message": "Payment initiated",
  "data": {
    "id": 410,
    "amount": "10.00",
    "currency": "USD",
    "payment_method": "card",
    "status": "PENDING",
    "expires_at": "2026-06-04T12:15:00.000000Z",
    "created_at": "2026-06-04T12:00:00.000000Z",
    "poll_url": "https://api.xash.co.zw/api/v1/card/poll/410",
    "charge_amount": "10.00",
    "charge_currency": "USD",
    "exchange_rate": null,
    "transactionReference": "CARD_REF_12345",
    "status_message": "Complete card authentication.",
    "redirect_html": "<form id=\"challenge\"></form><script>document.getElementById('challenge').submit()</script>"
  }
}
```

### 3D Secure Handling

When `data.redirect_html` is present, render it inside a controlled checkout container and allow its script to submit the challenge form. After the user completes the authentication flow, poll `data.poll_url` until the status becomes `SUCCESS`, `FAILED`, or `EXPIRED`.

### Callback Updates

When the deposit status changes to `SUCCESS` or `FAILED`/`EXPIRED`, your `callback_url` will receive a POST request from Xash:

```json
{
  "id": 410,
  "reference": "DEP_ABC123XYZ",
  "method": "card",
  "status": "SUCCESS",
  "amount": "10.00",
  "currency": "USD",
  "status_message": "Payment successful",
  "gateway_reference": null,
  "charge_amount": "10.00",
  "charge_currency": "USD",
  "exchange_rate": null,
  "wallet_amount": "10.00",
  "wallet_currency": "USD",
  "updated_at": "2026-06-04T12:06:30.000000Z"
}
```

### Security Notes

- Send card fields only from a secure checkout experience over HTTPS.
- Xash does not store the PAN, security code, or returned `redirect_html`.
- Do not log raw card details in your own application.
- `data.poll_url` is the Xash polling endpoint. It is separate from your optional `callback_url`.

### Client Flow

1. Call `/api/v1/card/pay`.
2. If `data.redirect_html` is present, render it and let the customer complete 3D Secure authentication.
3. Poll `data.poll_url` until the status becomes `SUCCESS`, `FAILED`, or `EXPIRED`.
4. If you provided `callback_url`, listen for the same status updates on your server.
