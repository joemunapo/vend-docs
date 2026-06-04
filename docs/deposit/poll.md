# Check Transaction Status (Polling)

Since mobile money, counter, card, and crypto payments are asynchronous, you should poll this endpoint to check if a transaction has been successfully completed.

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
| `method` | String | **Yes** | The payment method used. Allowed values: `ecocash`, `innbucks`, `omari`, `card`, `crypto`. |
| `id` | Integer | **Yes** | The unique ID of the payment transaction. |

### Example Request

```http
GET /api/v1/ecocash/poll/102
```

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
        "poll_url": "https://api.xash.co.zw/api/v1/ecocash/poll/102",
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
        "poll_url": "https://api.xash.co.zw/api/v1/innbucks/poll/105",
        "code": "123456789"
    }
}
```

#### 3\. Payment Successful

Once the provider update is received and the transaction is finalized.

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
        "poll_url": "https://api.xash.co.zw/api/v1/ecocash/poll/102",
        "status_message": "Payment successful"
    }
}
```

#### 4\. Payment Pending (Crypto Example)

Crypto responses include the address instructions and CryptoPay references.

```json
{
    "success": true,
    "message": "Payment pending",
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
        }
    }
}
```

#### 5\. Payment Pending (Card Example)

Card responses may include `redirect_html` during the initial checkout response. Polling returns the current payment status.

```json
{
    "success": true,
    "message": "Complete card authentication.",
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
        "status_message": "Complete card authentication."
    }
}
```

#### 6\. Payment Pending (ZWG EcoCash Example)

ZWG mobile-money deposits credit the USD wallet. The response keeps `amount` and `currency` as the wallet credit values and includes the ZWG provider charge metadata.

```json
{
    "success": true,
    "message": "Payment pending",
    "data": {
        "id": 102,
        "amount": "10.00",
        "currency": "USD",
        "payment_method": "ecocash",
        "status": "PENDING",
        "expires_at": "2026-06-04T12:15:00.000000Z",
        "created_at": "2026-06-04T12:00:00.000000Z",
        "poll_url": "https://api.xash.co.zw/api/v1/ecocash/poll/102",
        "charge_amount": "320.00",
        "charge_currency": "ZWG",
        "exchange_rate": 32,
        "status_message": "Check mobile to complete payment."
    }
}
```
