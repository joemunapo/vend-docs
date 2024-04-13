# Check User Account
This endpoint allows verifying a ZESA account by providing the meter number and currency.

**Method:** POST

**Endpoint:** `/api/v1/electricity/check-account`

Verifies the ZESA account associated with the provided meter number and currency. Returns the customer details if the account is valid.

### Headers

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |

### Parameters

| Name        | Type    | Description                                   | Validation                |
|-------------|---------|-----------------------------------------------|---------------------------|
| meter_number| string  | The ZESA meter number                         | Required, valid meter number |
| currency    | string  | The meter currency (ZWL or USD)               | Required, valid currency |

### Responses

#### Success Response:
```json
{
  "success": true,
  "message": "Account verified successfully.",
  "data": {
    "customer_name": "John Doe",
    "customer_address": "123 Main St, Harare",
    "meter_number": "12345678",
    "meter_currency": "ZIG",
    "success": true
  }
}
```

The response includes:
- `customer_name`: The customer's name associated with the meter number
- `customer_address`: The customer's address associated with the meter number
- `meter_number`: The provided meter number
- `meter_currency`: The meter currency (e.g., ZIG)
- `success`: Indicates if the account verification was successful

#### Error Response:
```json
{
  "success": false,
  "message": "Invalid meter number"
}
```

[Previous](/electricity/index.md) | [Next](/electricity/buy-tokens.md)