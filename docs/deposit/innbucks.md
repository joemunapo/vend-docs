# InnBucks API Documentation

## Pay (Generate Code)

### Description
Generate a payment code for a specified amount to make a deposit using InnBucks.

### Method
POST

### Endpoint
`/v1/innbucks/pay`

### Headers
| Name         | Value                |
|--------------|----------------------|
| Accept       | application/json     |
| Authorization| Bearer {accessToken} |

### Parameters
| Name   | Type   | Required | Description               |
|--------|--------|----------|---------------------------|
| amount | number | Yes      | Deposit amount (in dollars) |

### Example Response
```json
{
  "success": true,
  "message": "Payment code generated successfully. Scan the QR code to complete payment.",
  "data": {
    "id": 1,
    "code": "1234567890",
    "amount": 20,
    "currency": "USD",
    "qr_code": "https://example.com/qr/1234567890",
    "status": "PENDING",
    "status_message": null,
    "expires_at": "2024-06-09T11:30:00Z",
    "created_at": "2024-06-09T10:30:00Z"
  }
}
```

### Sample Error Response
```json
{
  "success": false,
  "message": "Failed to generate InnBucks code, try again"
}
```

## Poll Payment

### Description
Check the status of a deposit payment.

### Method
GET

### Endpoint
`/v1/innbucks/poll/{id}`

### Headers
| Name         | Value                |
|--------------|----------------------|
| Accept       | application/json     |
| Authorization| Bearer {accessToken} |

### Parameters
| Name | Type    | In   | Description                    |
|------|---------|------|--------------------------------|
| id   | integer | path | The ID of the payment to poll  |

### Example Response
```json
{
  "success": true,
  "message": "Payment pending. Scan the QR code to complete payment.",
  "data": {
    "id": 1,
    "code": "1234567890",
    "amount": 20,
    "currency": "USD",
    "qr_code": "https://example.com/qr/1234567890",
    "status": "PENDING",
    "status_message": null,
    "expires_at": "2024-06-09T11:30:00Z",
    "created_at": "2024-06-09T10:30:00Z"
  }
}
```

In the `poll` endpoint, the `{id}` parameter in the URL represents the ID of the payment that needs to be polled. The user should provide the `id` value from the `data` object returned by the `pay` endpoint.

The response of both endpoints includes a `data` object that contains relevant information about the payment, such as the payment code, amount, currency, QR code, status, and timestamps. The user can utilize this information to track the status and details of their deposit payment.