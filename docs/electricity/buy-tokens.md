# Buy Tokens

This endpoint allows purchasing ZESA tokens.

**Method:** POST

**Endpoint:** `/api/v1/electricity/buy-tokens`

Purchases ZESA tokens based on the provided meter number, amount, and payment currency. Requires sufficient balance in the vendor's wallet. On success, returns the generated tokens along with token details for printing the receipt.

### Headers

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |

### Parameters

| Name        | Type    | Description                                   | Validation                |
|-------------|---------|-----------------------------------------------|---------------------------|
| meter_number| string  | The ZESA meter number                         | Required, valid meter number |
| amount      | float   | The purchase amount                           | Required, greater than 0 |
| currency    | string  | The payment currency (ZiG or USD)             | Required, valid currency |

### Responses

#### Success Response:
```json
{
  "success": true,
  "message": "ZESA tokens purchased successfully.",
  "data": {
    "customer_name": "John Doe",
    "customer_address": "123 Main St, Harare",
    "meter_number": "12345678",
    "meter_currency": "ZIG",
    "kwh": "106.0",
    "energy": "ZIG127.92",
    "debt": "ZIG0.00",
    "rea": "ZIG7.68",
    "vat": "ZIG0.00",
    "tendered_currency": "USD",
    "tendered": "USD10.00",
    "total_amt": "ZIG135.60",
    "date": "13/04/24 22:40",
    "tokens": [
      {
        "token": "56499328826779434026",
        "units": "106.0",
        "formatted": "5649 9328 8267 7943 4026",
        "rate": "50.0@1.08: 50.0@1.22: 6.0@2.17: ",
        "receipt": "00001240413224051057",
        "tax_rate": "0.00",
        "net_amount": "127.92",
        "tax_amount": "0.00",
        "position": 1
      }
    ],
    "balance": {
      "currency": "USD",
      "name": "US Dollar",
      "profit_on_hold": "0.25",
      "balance": "15"
    },
    "commission": "USD0.25"
  }
}
```

The response includes:
- `customer_name`: A generic random customer name (e.g., John Doe)
- `customer_address`: A generic random customer address (e.g., 123 Main St, Harare)
- `meter_number`: A generic random meter number (e.g., 12345678)
- `meter_currency`: The meter currency (e.g., ZIG)
- `kwh`: The purchased kilowatt-hours
- `energy`: The energy amount and currency
- `debt`: The debt amount and currency
- `rea`: The REA amount and currency
- `vat`: The VAT amount and currency
- `tendered_currency`: The tendered (payment) currency
- `tendered`: The tendered (payment) amount
- `total_amt`: The total amount and currency
- `date`: The date and time of the purchase
- `tokens`: An array of purchased tokens, including token number, units, formatted token, rate, receipt number, tax rate, net amount, tax amount, and position
- `balance`: The vendor's updated wallet balance and currency
- `commission`: The earned commission amount and currency

The client should use this response data to generate the receipt, displaying all the required fields as per the UAT document.

#### Error Response:
```json
{
  "success": false,
  "message": "Insufficient balance"
}
```

[Previous](./verify-account.md)