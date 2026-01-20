# OMari Deposit

This endpoint initiates a deposit request using OMari. It triggers a prompt on the user's mobile device to authorize the transaction.

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
| `poll_url` | String | No | Optional webhook URL for server clients. If provided, we will forward the deposit status updates to this URL. |

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
    "status": "PENDING",
    "status_message": "Check mobile to complete payment.",
    "poll_url": "https://api.xash.co.zw/api/v1/omari/poll/210",
    "expires_at": "2025-12-02T08:15:00.000000Z",
    "created_at": "2025-12-02T08:00:00.000000Z"
  }
}
```

**Note:** The API response `poll_url` is currently generated using a method mapping that only distinguishes EcoCash and InnBucks. If it returns an InnBucks `poll_url` for OMari, use the OMari poll endpoint below in your integrations.

## Poll Status

**Method:** GET

**Endpoint:** `/api/v1/omari/poll/{payment}`

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
GET /api/v1/omari/poll/210
```

### Response

The response includes the same fields as the payment initiation.

```json
{
  "success": true,
  "message": "Payment pending",
  "data": {
    "id": 210,
    "amount": "10.00",
    "currency": "USD",
    "status": "PENDING",
    "status_message": "Check mobile to complete payment.",
    "poll_url": "https://api.xash.co.zw/api/v1/omari/poll/210",
    "expires_at": "2025-12-02T08:15:00.000000Z",
    "created_at": "2025-12-02T08:00:00.000000Z"
  }
}
```

## Confirm Payment (OTP)

Use this endpoint when OMari returns an OTP confirmation step.

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
| `transactionReference` | String | **Yes** | Reference returned by OMari. |
| `otp` | String | **Yes** | One-time password provided by the user. |
| `omariMobile` | String | **Yes** | OMari mobile number. |

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
  "message": "Payment confirmed.",
  "data": {
    "id": 210,
    "status": "SUCCESS"
  }
}
```
