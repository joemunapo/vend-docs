## Buy Wifi Voucher

This endpoint allows purchasing wifi vouchers.

**Method:** POST

**Endpoint:** `/api/v1/wifi/vouchers/buy`

Purchases the specified quantity of wifi vouchers. Requires sufficient balance in the user's wallet. On success, returns details of the purchased vouchers along with updated wallet balance and earned commission.

### Headers

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |

### Parameters

| Name     | Type    | Description                           | Validation                |
|----------|---------|---------------------------------------|---------------------------|
| service   | integer | The ID of the bundle to purchase vouchers for | Required, valid bundle ID |
| amount | integer | The amount of voucher to purchase    | Required, integer |
| quantity | integer | The number of vouchers to purchase    | Required, integer, min: 1 |
| currency | string | The currency of vouchers to purchase    | Required, string, USD:ZIG |
| duration | integer | The time duration of vouchers to purchase    | Required, integer, min: 1 |
| duration_in | string | The number of vouchers to purchase    | Required, integer, : days, hours, minutes |

### Responses

#### Success Response:
```json
{
    "success": true,
    "message": "Equal WiFi Voucher purchase was successful",
    "data": {
        "status": "success",
        "type": "equal_voucher",
        "id": "9d8158b0-ee16-4bd2-91c5-c5433ed45d14",
        "reference": "C5433ED45D14",
        "name": "Equal WiFi Voucher",
        "amount": "5.00",
        "voucher_value": "5.00",
        "currency": "USD",
        "balance": {
            "currency": "USD",
            "name": "US Dollar",
            "profit_on_hold": "8.830",
            "balance": "{Profile Balance}"
        },
        "vouchers": [
            {
                "pin": "{Voucher Pin}",
                "data_limit": "25GB",
                "amount": "5.00",
                "duration": 15,
                "duration_in": "days"
            }
        ],
        "commission": "{Commission}",
        "receipt_footer": "Get airtime/bundle on your change from as little as 10 cents.",
        "created_at": "2024-11-16T20:24:03.000000Z",
        "recharge_instructions": "1. Connect to \"Equal WiFi\".\n2. Click on \"Sign In\" to access network\n3. Enter your voucher & press connect."
    }
}
```

#### Error Response:
```json
{
  "success": false,
  "message": "You do not have enough balance to make this transaction."
}
```

[Previous](/wifi/buy-direct.md)
