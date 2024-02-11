### Purchase Bundle Voucher API

#### Description
This endpoint allows users to purchase vouchers for data or SMS bundles, which can be redeemed at a later time. Users need to specify the bundle name, network carrier, currency, value of the bundle, and the quantity of vouchers they wish to purchase. The system validates the request, checks for sufficient wallet balance, and generates the bundle vouchers accordingly.

#### Route
- **Method:** POST
- **URL:** `/v1/bundles/voucher/buy`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<Your Access Token\>

#### Body Parameters
- **network** (required): String. The network carrier for the bundle purchase. Currently, voucher purchases are limited to specific carriers (e.g., Econet).
- **name** (required): String. The name of the bundle for which the voucher is being purchased.
- **currency** (required): String. The currency for the transaction. Valid options are "USD" or "ZWL".
- **value** (required): Numeric. The value or cost of the bundle for which the voucher is being purchased.
- **quantity** (required): Integer. The number of vouchers to purchase.

#### Response Status Codes
- **200 OK**: The vouchers were successfully purchased. The response includes details of the vouchers, including their values and codes.
- **400 Bad Request**: Indicates validation errors or issues such as an inactive wallet, insufficient balance, unsupported network, or unavailable bundle.
- **500 Internal Server Error**: Represents an error in processing the request, such as an issue with generating the vouchers or deducting the amount from the wallet.

#### Example Response
```json
{
  "message": "Data Weekly Bundle 1GB purchase was successful",
  "data": {
    "voucher_value": "10.00",
    "vouchers": [
      "VoucherCode1",
      "VoucherCode2"
    ]
  }
}
```

#### Notes
- The request must specify an available bundle by name, network, and currency. The system checks if the selected bundle is available for voucher purchase.
- The total cost of the vouchers is calculated as the product of the `value` and `quantity`. The user's wallet must have enough balance to cover this cost.
- Vouchers are generated with unique codes, which can be used to redeem the specified bundle. The response includes these voucher codes.
- The implementation currently restricts voucher purchases to specific networks due to carrier limitations. This restriction is reflected in the validation rules and error responses.