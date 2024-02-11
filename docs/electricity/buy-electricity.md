### Purchase Electricity Tokens API

#### Description
This endpoint facilitates the purchase of ZESA tokens, directly recharging the provided electricity meter number. Users must specify the meter number, the amount they wish to purchase, and the currency. The system validates the service availability, checks the user's wallet balance, and processes the token purchase.

#### Route
- **Method:** POST
- **URL:** `/v1/electricity/buy-tokens`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<Your Access Token\>

#### Body Parameters
- **currency** (required): String. The currency for the transaction. Valid options are "USD" or "ZWL".
- **amount** (required): Numeric. The amount of money to spend on purchasing electricity tokens.
- **meter_number** (required): String. The electricity meter number to which the tokens will be credited.

#### Response Status Codes
- **200 OK**: The tokens were successfully purchased. The response includes details of the transaction, including the amount of kWh purchased, any debt or charges applied, VAT, and the total amount tendered.
- **400 Bad Request**: Indicates validation errors or issues such as an inactive service or wallet, insufficient balance, or an invalid meter number.
- **422 Unprocessable Entity**: Failed to process the payment or the token purchase. This status may indicate a temporary issue, advising the user to wait a moment before retrying.
- **500 Internal Server Error**: Represents an error in processing the request, such as an issue with the external service provider or an unexpected server error.

#### Example Response
```json
{
  "success": true,
  "message": "ZESA tokens purchased successfully.",
  "data": {
    "reference": "123456789",
    "meter_number": "0123456789",
    "kwh": "50",
    "energy": "USD10.00",
    "debt": "USD0.00",
    "rea": "USD0.50",
    "vat": "USD1.50",
    "tendered_currency": "USD",
    "tendered": "USD12.00",
    "total_amt": "USD12.00",
    "date": "01/01/2023 12:00",
    "tokens": [
      {
        "token": "123456789012345",
        "units": "50",
        "formatted": "123-456-789-012-345",
        "rate": "1.0",
        "receipt": "ABC123",
        "tax_rate": "15%",
        "net_amount": "10.00",
        "tax_amount": "1.50",
        "position": 1
      }
    ]
  }
}
```

#### Notes
- The transaction involves a mandatory waiting period to ensure compliance with the external service provider's processing requirements.
- The `tokens` array in the response provides detailed information about each token purchased, including the token number, the units of electricity bought, and applicable charges.
- In cases where the token purchase fails after deducting the amount from the wallet, an attempt is made to refund the deducted amount to the user's wallet.
- Users are encouraged to verify the meter number and ensure sufficient wallet balance before initiating a token purchase to avoid transaction failures.