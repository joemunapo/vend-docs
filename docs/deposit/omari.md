# OMari Deposit

This endpoint initiates a deposit request using OMari. It triggers a prompt on the user's mobile device to authorize the transaction.

The initiate response returns a `transactionReference`. Keep this value because it is required when submitting the OTP in the confirmation step.

## Initiate Payment

**Method:** POST

**Endpoint:** `/api/v1/omari/pay`

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Parameters

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `amount` | Float | **Yes** | The amount to deposit (USD). Minimum `0.1`. |
| `omari_phone` | String | **Yes** | The OMari phone number to bill. Must be a valid Zimbabwean number. |
| `poll_url` | String | No | Optional webhook URL for server clients. If provided, we will forward deposit status updates to this URL. Include your reference as a query parameter in the URL (e.g. `?reference=ORDER_12345`). |

### Example Request

```json
{
  "amount": 10.0,
  "omari_phone": "0771234567",
  "poll_url": "https://client.example.com/webhooks/omari?reference=ORDER_12345"
}
```

### Response

If successful, the API returns `200 OK` with a message instructing the user to check their mobile device.

```json
{
  "success": true,
  "message": "Check mobile to complete payment.",
  "data": {
    "id": 210,
    "amount": "10.00",
    "currency": "USD",
    "status": "AWAITING_PAYMENT",
    "expires_at": "2026-05-29T21:54:32.118053Z",
    "created_at": "2026-05-29T21:39:32.000000Z",
    "poll_url": "https://api.xash.co.zw/api/v1/innbucks/poll/210",
    "transactionReference": "OMARI_REF_12345",
    "status_message": "Check mobile to complete payment."
  }
}
```

**Note:** OMari responses can currently return a `data.poll_url` under `/api/v1/innbucks/poll/{id}`. Use the `poll_url` exactly as returned by the API. If you build the URL manually, `/api/v1/omari/poll/{id}` is also accepted.

## Poll Status

**Method:** GET

**Endpoint:** Use the `data.poll_url` returned by the initiate response. Manual OMari polling is also available at `/api/v1/omari/poll/{payment}`.

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### URL Parameters

| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `payment` | Integer | **Yes** | The OMari payment ID. |

### Example Request

```http
GET /api/v1/innbucks/poll/210
```

### Response

The response includes the same fields as the payment initiation.

```json
{
  "success": true,
  "message": "Check mobile to complete payment.",
  "data": {
    "id": 210,
    "amount": "10.00",
    "currency": "USD",
    "status": "AWAITING_PAYMENT",
    "expires_at": "2026-05-29T21:54:32.118053Z",
    "created_at": "2026-05-29T21:39:32.000000Z",
    "poll_url": "https://api.xash.co.zw/api/v1/innbucks/poll/210",
    "transactionReference": "OMARI_REF_12345",
    "status_message": "Check mobile to complete payment."
  }
}
```

## Confirm Payment (OTP)

Use this endpoint after the customer receives the OMari OTP. The confirmation request sends the OTP and the first leg `transactionReference` back to Smile&Pay to finalize the payment.

**Method:** POST

**Endpoint:** `/api/v1/omari/confirm`

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Parameters

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `transactionReference` | String | **Yes** | Transaction reference returned by `/api/v1/omari/pay` as `data.transactionReference`. |
| `otp` | String | **Yes** | OTP sent to the customer's OMari mobile number. |
| `omariMobile` | String | **Yes** | OMari mobile number used for the payment. |

### Example Request

```json
{
  "transactionReference": "OMARI_REF_12345",
  "otp": "123456",
  "omariMobile": "0771234567"
}
```

### Response

```json
{
  "success": true,
  "message": "Confirmation processed",
  "data": {
    "responseMessage": "Payment confirmed",
    "responseCode": "00",
    "status": "PAID",
    "transactionReference": "OMARI_REF_12345"
  }
}
```

## Client Flow

1. Call `/api/v1/omari/pay`.
2. Store `data.transactionReference`.
3. Ask the customer for the OTP sent to their OMari mobile number.
4. Call `/api/v1/omari/confirm` with `transactionReference`, `otp`, and `omariMobile`.
5. Poll the returned `data.poll_url` from the first leg until the status changes from `AWAITING_PAYMENT`/`PENDING` to a final status such as `SUCCESS`, `FAILED`, or `EXPIRED`.
6. If you provided a request `poll_url`, listen for the webhook update on your own URL as well.
