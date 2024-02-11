### Airtime Purchase API

#### Description
This endpoint enables users to purchase direct airtime for specified mobile phone numbers from supported carriers. Users need to provide the mobile phone number, the amount of airtime to purchase, and the currency for the transaction. The system validates the carrier's support for direct airtime, checks the user's wallet balance, and processes the airtime purchase accordingly.

#### Route
- **Method:** POST
- **URL:** `/v1/airtime/direct`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<Your Access Token\>

#### Parameters
- **mobile_phone** (required): String. The mobile phone number to recharge. Must be valid and supported by the carriers offering direct airtime.
- **amount** (required): Numeric. The amount of airtime to purchase. Must be greater than 0.1.
- **currency** (required): String. The currency for the transaction. Valid options are "ZWL" or "USD".

#### Response Status Codes
- **200 OK**: The airtime purchase was successful. Includes details about the transaction.
- **400 Bad Request**: Indicates validation errors such as an unsupported carrier, inactive wallet, or insufficient balance.
- **500 Internal Server Error**: Represents an error in processing the request, such as an issue with deducting the balance or communicating with the airtime provider.

#### Example Response
```json
{
  "success": true,
  "message": "Recharge to <mobile_phone> was successful",
  "data": {
    "receiver": "<mobile_phone>"
  }
}
```

#### Notes
- The system first checks if the provided mobile phone's carrier supports direct airtime purchases.
- The user's wallet is verified for sufficient funds to cover the airtime purchase, including checking if the wallet is active.
- The purchase amount is deducted from the user's wallet, and the transaction is saved. In case of a transaction failure, an attempt is made to refund the deducted amount.
- Environmental variables or configuration settings may simulate the airtime purchase process for testing purposes.
- Transactions are tracked, and their status is updated based on the success or failure of the airtime recharge.