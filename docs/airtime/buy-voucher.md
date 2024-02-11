### Purchase Airtime Voucher API

#### Description
This endpoint allows users to purchase airtime vouchers from supported carriers. Users must specify the carrier, the amount per voucher, the currency, and the quantity of vouchers they wish to purchase.

#### Route
- **Method:** POST
- **URL:** `/v1/airtime/direct/voucher/{carrier}`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<Your Access Token\>

#### URL Parameters
- **carrier**: The carrier's ID returned from voucher/carriers route

#### Body Parameters
- **amount** (required): Numeric. The value of each airtime voucher to be purchased.
- **currency** (required): String. The currency for the transaction. Valid options are "ZWL" or "USD".
- **quantity** (required): Integer. The number of vouchers to purchase.

#### Response Status Codes
- **200 OK**: The vouchers were successfully purchased. The response includes details of the purchase and the voucher codes.
- **400 Bad Request**: Indicates validation errors or issues such as an unsupported carrier or inactive wallet.
- **500 Internal Server Error**: Represents an error in processing the request, such as an issue with generating the vouchers.

#### Example Response
```json
{
  "success": true,
  "message": "<Carrier Name> purchase was successful",
  "data": {
    "voucher_amount": "10.00",
    "vouchers": [
      "1234567890",
      "0987654321"
    ]
  }
}
```

#### Notes
- Before processing the voucher purchase, the system checks if the selected carrier supports voucher sales.
- The user's wallet is verified for sufficient funds to cover the total cost of the vouchers being purchased. The total amount is calculated as the product of the `amount` and `quantity` parameters.
- In case of failure during the voucher generation or any part of the transaction, an attempt is made to refund the user's account.
- The response includes the voucher amount and the generated voucher codes. The number of voucher codes in the response matches the `quantity` specified in the request.
- This endpoint is designed to be flexible, supporting multiple carriers with the capability to generate and provide vouchers directly to the user upon purchase.