### Confirm Transfer

**Method:** POST

**Endpoint:** `/api/v1/transfer/confirm/{transfer}`

This endpoint confirms and completes a previously initiated transfer. It checks the sender's balance again and transfers the funds to the recipient if successful.

#### Headers
| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |

#### URL Parameters
| Parameter | Type   | Description                        |
|-----------|--------|------------------------------------|
| transfer  | string | The UUID of the initiated transfer |

#### Success Response
```json
{
  "success": true,
  "message": "Transfer completed successfully.",
  "data": {
    "balance": {
      "currency": "USD",
      "name": "US Dollar",
      "profit_on_hold": "0.00",
      "balance": "900.00"
    },
    "transaction_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "recipient": "2637xxxxxxxx",
    "amount": "100.00",
    "currency": "USD",
    "reference": "Rent payment",
    "first_name": "John",
    "last_name": "Doe"
  }
}
```

#### Error Response
- If the sender has insufficient balance:
  ```json
  {
    "success": false,
    "message": "You do not have enough balance to make this transaction."
  }
  ```
