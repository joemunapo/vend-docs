# Initiate Transfer

**Method:** POST

**Endpoint:** `/api/v1/transfer`

This endpoint initiates a transfer request. It validates the recipient's existence and checks if the sender has sufficient balance to make the transfer.

#### Headers
| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |
| Content-Type  | application/json |

#### Request Body
| Parameter | Type   | Description                                  | Validation                        |
|-----------|--------|----------------------------------------------|-----------------------------------|
| currency  | string | The currency of the transfer                 | Required, Valid currency          |
| amount    | number | The amount to transfer                       | Required, Numeric                 |
| recipient | string | The user number of the recipient             | Required, Exists in profiles table |
| reference | string | Optional reference or note for the transfer  | Nullable, Max 50 characters       |

#### Success Response
```json
{
  "success": true,
  "message": "Transfer initiated successfully.",
  "data": {
    "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "sender": "2637xxxxxxxx",
    "recipient": "2637xxxxxxxx",
    "first_name": "John",
    "last_name": "Doe",
    "amount": "100.00",
    "currency": "USD",
    "reference": "Rent payment"
  }
}
```

#### Error Responses
- If the sender tries to transfer to themselves:
  ```json
  {
    "success": false,
    "message": "You cannot transfer to yourself."
  }
  ```
- If the sender has insufficient balance:
  ```json
  {
    "success": false,
    "message": "You do not have enough balance to make this transaction."
  }
  ```
- If the recipient is not found:
  ```json
  {
    "success": false,
    "message": "Recipient not found."
  }
  ```
