## Buy Wifi Voucher

This endpoint allows purchasing wifi vouchers.

**Method:** POST

**Endpoint:** `/api/v1/paynow/initiate-mobile`

Purchases the specified quantity of wifi vouchers. Requires sufficient balance in the user's wallet. On success, returns details of the purchased vouchers along with updated wallet balance and earned commission.

### Headers

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |

### JSON Example Parameters

```json
{
    "reference": "Invoice 1253",
    "phone": "0771111111",
    "method": "ecocash",
    "items": [
        {          
    "amount": 5.00,
    "quantity": 1,
    "currency": "USD",
    "data_limit": "25GB",
    "duration": 15,
    "duration_in": "days"
        }
    ]
}
```


### Responses

#### Success Response:
```json
{
    "poll_url": "https://www.paynow.co.zw/Interface/CheckPayment/?guid=507eac5d-1a68-4fb9-92eb-446254aa5117",
    "instructions": "This is a test transaction. Test Case: Success",
    "pins": [
        "71 4900"
    ]
}
```

#### Error Response:
```json
{
  "success": false,
  "message": "You do not have enough balance to make this transaction."
}
```

### Check Payment Status
 
**Method:** POST

**Endpoint:**  `api/v1/paynow/status`
### Json sample data
```json
{
  "poll_url": "https://www.paynow.co.zw/Interface/CheckPayment/?guid=507eac5d-1a68-4fb9-92eb-446254aa5117"
}
```

### Responses

#### Success Response:

```json
{
    "status": "paid"
}
```

[Previous](/wifi/buy-direct.md)
