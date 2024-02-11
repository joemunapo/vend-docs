### Purchase Direct Bundle API

#### Description
This endpoint allows users to directly purchase bundles for a specified phone number. Users must provide details such as the mobile phone number, the network carrier, the name of the bundle, currency, and the bundle's value. The system validates the request, checks for sufficient wallet balance, and processes the bundle purchase directly to the phone number provided.

#### Route
- **Method:** POST
- **URL:** `/v1/bundles/buy`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<Your Access Token\>

#### Body Parameters
- **mobile_phone** (required): String. The phone number to which the bundle will be credited. Must be valid and supported by the specified network carrier.
- **network** (required): String. The network carrier for the bundle purchase. Must match the network of the provided phone number.
- **name** (required): String. The name of the bundle to be purchased.
- **currency** (required): String. The currency for the transaction. Valid options are "USD" or "ZWL".
- **value** (required): Numeric. The value or cost of the bundle to be purchased.

#### Response Status Codes
- **200 OK**: The bundle was successfully purchased. Includes details of the transaction.
- **400 Bad Request**: Indicates validation errors or issues such as an inactive wallet, insufficient balance, or an unsupported network.
- **500 Internal Server Error**: Represents an error in processing the request, such as an issue with the transaction or the inability to process the bundle purchase.

#### Example Response
```json
{
  "message": "Data Daily Bundle 500MB bundle purchased successfully",
  "data": {
    "name": "Data Daily Bundle 500MB",
    "amount": 5.00,
    "currency": "USD",
    "receiver": "+123456789",
    "commission": "$0.150",
    "vendor_balance": "$94.85"
  }
}
```

#### Notes
- The system first verifies if the selected bundle is available for the specified network and matches the provided currency and value.
- The user's wallet must have enough balance to cover the cost of the bundle. If the balance is insufficient, the request is declined.
- The currency and the amount of the bundle are validated against the current offerings to ensure the request can be fulfilled.
- Transactions are recorded, and upon successful deduction of the bundle cost, the bundle is credited to the specified mobile phone number.
- If the transaction fails after deducting the amount, an attempt is made to refund the deducted amount to the user's wallet.