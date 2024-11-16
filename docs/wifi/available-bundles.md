 ## Available WIFI Vouchers

This endpoint retrieves a list of wifi vouchers.

**Method:** GET

### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<User's Access Token\>

**Endpoint:** `/api/v1/wifi/vouchers` 

Retrieves a list of available wifi vouchers grouped by amount, duration and data limit. The #### 

### Responses

#### Success Response:
```json
{
    "success": true,
    "message": "Available Equal voucher values",
    "data": [
        {
            "amount": "5.00",
            "duration": 3,
            "duration_in": "days",
            "data_limit": "2GB",
            "currency": "USD"
        },
        {
            "amount": "5.00",
            "duration": 15,
            "duration_in": "days",
            "data_limit": "25GB",
            "currency": "USD"
        }
    ]
}
```

#### Error Response:
```json
{
  "success": false,
  "message": "Error message"
}
```

[Previous](/bundle/index.md) | [Next](/bundle/buy-direct.md)
